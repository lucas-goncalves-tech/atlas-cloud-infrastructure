# [002] Inspecionar a aplicação Bookstore

## Objetivo
Descobrir como o backend Bookstore é construído, configurado e executado antes de criar os manifestos Kubernetes.

## Contexto
O Kubernetes precisa receber uma imagem executável e as configurações que a aplicação realmente utiliza. Não devemos inventar porta, comando de inicialização, endpoint de health check ou nome de variável de ambiente.

O Bookstore é a aplicação-base deste laboratório. Esta Issue conecta o projeto de aplicação ao trabalho de infraestrutura sem exigir mudanças na regra de negócio.

## Pré-requisitos
- [ ] Issue 001 concluída.
- [ ] Repositório Bookstore clonado localmente.

## Tarefas

### 1. Estrutura e execução
- [ ] Localizar o `package.json` do backend.
- [ ] Identificar os scripts reais de instalação, build, desenvolvimento e produção.
- [ ] Identificar o comando que inicia o servidor em produção.
- [ ] Identificar a porta configurada e se o servidor escuta em `0.0.0.0` ou somente em `localhost`.
- [ ] Localizar o Dockerfile e o arquivo Compose, caso existam.

### 2. Configuração e banco
- [ ] Identificar todas as variáveis de ambiente necessárias.
- [ ] Identificar como a aplicação recebe a conexão PostgreSQL.
- [ ] Identificar a versão/compatibilidade do PostgreSQL, se documentada.
- [ ] Identificar como o Prisma executa migrations.
- [ ] Verificar se existe seed obrigatório para inicialização.

### 3. Validação local
- [ ] Seguir as instruções oficiais do repositório para iniciar o backend.
- [ ] Confirmar que o backend consegue conectar ao banco no fluxo local documentado.
- [ ] Identificar uma rota existente que possa ser usada para validar uma resposta HTTP.
- [ ] Confirmar se já existe endpoint de health check; não criar uma rota fictícia para satisfazer o Kubernetes.

## Critérios de aceitação
- O comando de build e o comando de inicialização de produção estão identificados.
- Porta, variáveis e conexão com PostgreSQL foram confirmadas no código ou documentação.
- O procedimento de migration do Prisma está identificado.
- Existe uma forma conhecida de verificar se a aplicação responde.
- Nenhum valor foi presumido sem conferir o repositório.

## Entrega
- Informações técnicas necessárias para construir a imagem e o Deployment.
- Se necessário, anotações curtas no README do projeto sobre particularidades reais da aplicação.

## Definition of Done
A Issue está concluída quando outra pessoa consegue determinar, a partir do repositório e das informações levantadas, como construir e iniciar o backend sem adivinhar configurações.