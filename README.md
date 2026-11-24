# Atlas — Cloud Infrastructure Lab

Projeto prático de infraestrutura local para executar e operar o backend existente do **Bookstore** em Kubernetes, sem depender de uma conta AWS ou de créditos de cloud.

## Objetivo

Construir um ambiente Kubernetes local com K3d, executar o Bookstore (Express + TypeScript) e seu PostgreSQL, configurar armazenamento persistente, rede, exposição HTTP, isolamento básico e mecanismos de diagnóstico.

O foco é infraestrutura e operação. Não é necessário reimplementar funcionalidades do Bookstore nem criar um segundo backend.

## Stack

- Docker
- K3d / K3s
- Kubernetes / kubectl
- Bookstore (Express + TypeScript)
- PostgreSQL / Prisma
- NGINX Ingress Controller
- YAML

## Escopo

- Cluster Kubernetes local.
- Namespace dedicado.
- ConfigMaps e Secrets.
- PostgreSQL com StatefulSet e armazenamento persistente.
- Backend em Deployment.
- Services e DNS interno.
- Ingress para acesso local.
- NetworkPolicy, probes e limites de recursos.
- TLS local opcional.
- Procedimento de reconstrução do ambiente.

Redis, Terraform, AWS e alterações de regra de negócio estão fora do escopo inicial.

## Estrutura

```text
.
├── README.md
└── issues/
    ├── 001-preparar-ambiente-local.md
    ├── 002-inspecionar-bookstore.md
    ├── 003-criar-cluster-k3d.md
    ├── 004-namespace-e-recursos.md
    ├── 005-configmap-e-secrets.md
    ├── 006-postgres-statefulset.md
    ├── 007-validar-persistencia-postgres.md
    ├── 008-build-e-import-da-imagem.md
    ├── 009-deployment-do-backend.md
    ├── 010-services-e-dns.md
    ├── 011-ingress-local.md
    ├── 012-networkpolicy.md
    ├── 013-probes-logs-e-debug.md
    ├── 014-tls-local-opcional.md
    └── 015-destruir-e-recriar-ambiente.md
```

## Ordem de execução

Conclua as Issues em ordem. A Issue 002 é especialmente importante: antes de escrever os manifestos do backend, confirme no repositório real os comandos de execução, a porta, as variáveis de ambiente, a configuração do Prisma e o processo de migrations.

Não presuma nomes de scripts, endpoints ou variáveis. Quando este projeto não especificar um valor, descubra-o no código do Bookstore e registre-o no manifesto apropriado.

## Requisitos locais

- Docker funcionando.
- `kubectl`.
- `k3d`.
- Git.
- Repositório Bookstore clonado localmente.
- Recursos de CPU e memória suficientes para executar o cluster e o banco na máquina.

## Segurança e dados

Não versione credenciais reais. Os Secrets devem ser criados localmente ou receber valores de arquivos ignorados pelo Git. O PostgreSQL deste laboratório não deve ser exposto diretamente à rede externa.

## Resultado esperado

Ao concluir, será possível criar o cluster, implantar o Bookstore, acessá-lo por um hostname local, conectar o backend ao PostgreSQL persistente, diagnosticar falhas e reconstruir o ambiente seguindo os manifestos e as instruções do projeto.
