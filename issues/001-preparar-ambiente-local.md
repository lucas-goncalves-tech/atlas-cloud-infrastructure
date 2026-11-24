# [001] Preparar o ambiente local

## Objetivo
Preparar as ferramentas necessárias para criar e administrar um cluster Kubernetes local.

## Contexto
O laboratório será executado em containers por meio do K3d, que utiliza K3s para disponibilizar um cluster Kubernetes leve. Docker será a camada de execução dos nodes. `kubectl` será utilizado para consultar e administrar os recursos do cluster.

Esta etapa valida a máquina antes de introduzir os componentes do Bookstore.

## Pré-requisitos
- Docker instalado ou possibilidade de instalá-lo.
- Acesso ao terminal com permissões para executar Docker.
- Git disponível para obter o repositório Bookstore.

## Tarefas

### 1. Docker
- [ ] Instalar Docker Engine ou Docker Desktop.
- [ ] Iniciar o serviço Docker.
- [ ] Executar um container simples para confirmar que o daemon está funcional.
- [ ] Confirmar que o usuário consegue executar Docker sem erros de permissão.

### 2. Ferramentas Kubernetes
- [ ] Instalar `kubectl`.
- [ ] Instalar `k3d`.
- [ ] Consultar as versões instaladas.
- [ ] Confirmar que não há um contexto Kubernetes antigo causando confusão.

### 3. Preparação do repositório
- [ ] Clonar ou atualizar o repositório Bookstore.
- [ ] Identificar o diretório do backend e localizar sua documentação inicial.

## Critérios de aceitação
- Docker consegue iniciar e encerrar containers.
- `kubectl` e `k3d` respondem no terminal.
- Repositório Bookstore está disponível localmente.
- Não há dependência de uma conta ou recurso pago de cloud.

## Entrega
- Ferramentas instaladas e funcionais.
- Repositório Bookstore disponível para inspeção.

## Definition of Done
A Issue está concluída quando todas as ferramentas necessárias estão funcionais e o ambiente está pronto para a criação do cluster.