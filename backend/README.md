# Bookstore API (backend)

Backend do Bookstore usado como aplicação-base do laboratório Atlas. Express 5 + TypeScript, injeção de dependências com `tsyringe`, Prisma 6 e PostgreSQL.

Este README registra o comportamento **real** da aplicação (porta, comandos, variáveis, migrations e health check) para que os manifestos Kubernetes das issues não precisem adivinhar nada.

## Stack e execução

| Item | Valor confirmado no código |
| --- | --- |
| Runtime | Node 24 (imagem Docker `node:24-alpine`) |
| Servidor | Express 5, iniciado em `src/core/server.ts` |
| Porta | `PORT` (padrão no `.env.example`: `3333`) |
| Interface | `0.0.0.0` (explícito no `app.listen`) — acessível de dentro e de fora do Pod |
| Health check | `GET /health` → `200 {"message":"OK"}` (não consulta o banco) |
| API | `GET /api/v1/...` (ex.: `/api/v1/books`) |
| Documentação | `GET /api-docs` (Scalar/OpenAPI) |
| Banco | PostgreSQL (Compose usa `postgres:15-alpine`; validado também com PostgreSQL 17) |
| Prisma | Client 6.19.2, `binaryTargets`: `native` e `linux-musl-openssl-3.0.x` (Alpine) |

### Scripts

| Comando | O que faz |
| --- | --- |
| `npm ci` | Instala dependências a partir do `package-lock.json` |
| `npm run dev` | `tsx --watch src/core/server.ts` (desenvolvimento) |
| `npm run build` | `tsc` → gera `dist/` |
| `npm start` | `node dist/core/server.js` (produção; requer build anterior) |
| `npm test` | `vitest run` (testes de integração; requer Postgres de teste) |
| `npm run test:watch` | Vitest em modo watch |
| `npm run lint` / `npm run lint:fix` | ESLint |
| `npm run db:generate` | `prisma generate` |
| `npm run db:migrate` | `prisma migrate dev` (somente desenvolvimento local) |
| `npm run db:migrate:deploy` | `prisma migrate deploy` (produção/Kubernetes) |
| `npm run db:seed` | `prisma db seed` → `src/database/seed.ts` |

Os scripts exigem as variáveis de ambiente. O módulo `src/core/config/env.ts` carrega `.env` automaticamente via `dotenv/config`; variáveis já definidas no ambiente (ConfigMap/Secret do Kubernetes, por exemplo) têm precedência e não são sobrescritas.

Dentro do Compose, os equivalentes são `docker compose exec api npm test`, `docker compose exec api npm run lint`, etc.

## Variáveis de ambiente

Copie `.env.example` para `.env` e ajuste os valores. `.env` é ignorado pelo Git (`backend/.gitignore`) e pelo Docker (`backend/.dockerignore`) — nenhuma credencial entra na imagem.

| Variável | Origem sugerida no K8s | Obrigatória | Observação |
| --- | --- | --- | --- |
| `DB_USER`, `DB_PASS`, `DB_NAME` | — | apenas Compose | Usadas pelo serviço `db` do `compose.yaml` |
| `DATABASE_URL` | Secret | sim | `postgresql://usuario:senha@host:5432/bookstore`; no cluster use o DNS do Service do Postgres (ex.: `postgres:5432`) |
| `DATABASE_TEST_URL` | — | apenas testes | Fora do Compose aponte para `localhost:5434`; dentro dele, `db_test:5432` |
| `NODE_ENV` | ConfigMap | sim | `development`, `test` ou `production` |
| `PORT` | ConfigMap | sim | Porta HTTP do container (`3333`) |
| `ALLOWED_ORIGINS` | ConfigMap | sim | Array JSON, ex.: `["http://localhost:3000"]`; em produção define o CORS |
| `JWT_SECRET`, `JWT_REFRESH_SECRET` | Secret | sim | Mínimo de 32 caracteres cada |
| `JWT_EXPIRES`, `JWT_REFRESH_EXPIRES` | ConfigMap | sim | Ex.: `10m` e `7d` |
| `SALT` | ConfigMap | não | Custo do bcrypt; padrão `10` |
| `ADMIN_EMAIL`, `ADMIN_PASSWORD`, `ADMIN_NAME` | Secret | sim | Usados apenas pelo seed |
| `CLOUDINARY_CLOUD_NAME` | ConfigMap | sim | Cloud name do Cloudinary |
| `CLOUDINARY_API_KEY`, `CLOUDINARY_API_SECRET` | Secret | sim | Usados no upload de capas |
| `OPENAPI_URL` | ConfigMap | não | Ex.: `/api/v1` |

## Banco de dados, migrations e seed

- Os 16 arquivos de migration versionados em `prisma/migrations/` são a fonte da verdade.
- **Produção/Kubernetes:** `npm run db:migrate:deploy` (`prisma migrate deploy`). É idempotente e seguro para reexecutar.
- **Desenvolvimento local:** `npm run db:migrate` (`prisma migrate dev`), que pode criar novas migrations — não use no cluster.
- O seed é **opcional** para inicializar o processo, mas cria o admin, usuários, categorias, livros e reviews usados para validar a API. Rode-o como uma etapa separada (`npm run db:seed`), nunca em todas as réplicas.
- No deployment, as migrations devem rodar **uma única vez**, em um Job (ou init container) concluído antes de o backend receber tráfego. Não execute `migrate deploy` no `command` de cada réplica do Deployment. Um Job com `restartPolicy: OnFailure` e `backoffLimit` lida com o banco ainda não pronto.

## Execução local

```bash
npm ci
cp .env.example .env
# Ajuste DATABASE_URL para um PostgreSQL acessível da sua máquina.
npm run db:migrate:deploy
npm run db:seed          # opcional
npm run build
npm start
curl -i http://localhost:3333/health
```

Com Docker Compose (já sobe o PostgreSQL):

```bash
docker compose up -d --build
curl -i http://localhost:3333/health
```

Overlay de desenvolvimento (expõe o Postgres e sobe `db_test`):

```bash
docker compose -f compose.yaml -f compose.dev.yaml up -d --build
DATABASE_TEST_URL='postgresql://test:test@localhost:5434/bookstore_test' npm test
```

Os testes usam `DATABASE_TEST_URL` e criam os schemas `test_1` ... `test_4` com `prisma db push` no `global-setup`; cada teste limpa as tabelas antes de executar.

### Validação de referência

Com Node 24.22.0 e PostgreSQL 17 local: `npm run build` OK, `npm run lint` OK, `npm test` → 13 arquivos / 179 testes aprovados, `GET /health` → HTTP 200.

## Imagem Docker e K3d

```bash
docker build --target prod -t bookstore-api:local .
docker run --rm -p 3333:3333 --env-file .env bookstore-api:local
k3d image import bookstore-api:local -c atlas
```

- O alvo `prod` compila a aplicação e roda como usuário `node` (não root); o alvo `dev` mantém `tsx --watch`.
- `curl` está na imagem para o healthcheck do Compose; no Kubernetes use as probes descritas abaixo.
- Para imagem importada no K3d, use `imagePullPolicy: Never` (ou `IfNotPresent`) no Deployment.
- Não embuta `.env` na imagem: `.dockerignore` exclui `.env`, `.env.*`, `node_modules`, `dist` e `coverage`.

## Handoff para o Kubernetes

- **Deployment:** namespace `bookstore`, 1 réplica, `containerPort: 3333`, imagem local, env de ConfigMap + Secret, `imagePullPolicy: Never`.
- **ConfigMap:** `PORT`, `NODE_ENV`, `ALLOWED_ORIGINS`, `JWT_EXPIRES`, `JWT_REFRESH_EXPIRES`, `OPENAPI_URL`, `CLOUDINARY_CLOUD_NAME`.
- **Secret:** `DATABASE_URL`, `JWT_SECRET`, `JWT_REFRESH_SECRET`, `ADMIN_EMAIL`, `ADMIN_PASSWORD`, `ADMIN_NAME`, `CLOUDINARY_API_KEY`, `CLOUDINARY_API_SECRET`.
- **Migrations:** Job separado, comando `npm run db:migrate:deploy`, mesma imagem/env do backend, executado antes do Deployment.
- **Seed:** Job opcional separado, comando `npm run db:seed`.
- **Probes:** `GET /health` na porta 3333 para startup, readiness e liveness. É uma rota real da aplicação e não depende do banco; para validar a conexão com o PostgreSQL, use os logs e uma rota da API (por exemplo `GET /api/v1/books`).
- **Recursos sugeridos para o laboratório:** `requests` de `100m` CPU / `256Mi` memória e `limits` de `500m` CPU / `512Mi` memória.

## Estrutura relevante

```text
backend/
├── Dockerfile              # alvos dev e prod
├── compose.yaml            # db (Postgres 15) + api
├── compose.dev.yaml        # overlay com db_test e volume de código
├── .env.example            # todas as variáveis esperadas
├── prisma/
│   ├── schema.prisma
│   └── migrations/         # migrations versionadas
└── src/
    ├── core/server.ts      # listen em 0.0.0.0:PORT + shutdown gracioso
    ├── core/config/env.ts  # validação Zod + dotenv
    ├── app.ts              # /health, /api-docs, middlewares, rotas /api/v1
    ├── database/           # PrismaClient e seed
    └── tests/              # specs de integração e setup
```
