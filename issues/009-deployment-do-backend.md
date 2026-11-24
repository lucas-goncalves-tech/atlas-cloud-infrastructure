# [009] Implantar o backend com Deployment

## Objetivo
Executar o backend Bookstore dentro do cluster Kubernetes por meio de um Deployment.

## Contexto
Deployment gerencia réplicas de Pods e permite atualizar a versão da aplicação de maneira declarativa. Nesta etapa, o backend será conectado ao PostgreSQL interno.

O manifesto deve usar as informações reais levantadas na Issue 002.

## Pré-requisitos
- [ ] Issue 005 concluída.
- [ ] Issue 006 concluída.
- [ ] Issue 008 concluída.
- [ ] Configurações e comando de inicialização confirmados na Issue 002.

## Tarefas

### 1. Deployment
- [ ] Criar Deployment no namespace `bookstore`.
- [ ] Usar a imagem local construída na Issue 008.
- [ ] Configurar `imagePullPolicy` apropriada para imagem importada no K3d.
- [ ] Definir uma réplica inicial.
- [ ] Configurar labels e selectors consistentes.
- [ ] Definir requests e limits compatíveis com a máquina local.

### 2. Configuração da aplicação
- [ ] Injetar configurações não sensíveis do ConfigMap.
- [ ] Injetar credenciais por Secret quando aplicável.
- [ ] Configurar a conexão com PostgreSQL usando o DNS interno do Service.
- [ ] Garantir que a aplicação escute na interface de rede adequada ao container.
- [ ] Configurar o comando de inicialização confirmado na Issue 002.

### 3. Banco e migrations
- [ ] Definir uma execução segura e reproduzível das migrations do Prisma.
- [ ] Não executar migrations de forma concorrente em cada réplica.
- [ ] Aplicar migrations antes de considerar o backend pronto.
- [ ] Executar seed somente se for necessário ao funcionamento do ambiente.

## Critérios de aceitação
- Pod do backend inicia no namespace `bookstore`.
- Configurações são fornecidas pelo Kubernetes.
- Backend conecta ao PostgreSQL interno.
- Logs não apresentam erro de inicialização ou conexão.
- O Deployment mantém o número desejado de réplicas.

## Entrega
- Manifesto Kubernetes do Deployment.
- Ajustes estritamente necessários no Dockerfile ou na configuração de execução.

## Definition of Done
A Issue está concluída quando o Deployment mantém o backend em execução e a aplicação consegue utilizar o PostgreSQL do cluster.