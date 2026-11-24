# [003] Criar o cluster Kubernetes com K3d

## Objetivo
Criar um cluster Kubernetes local chamado `atlas` para hospedar os componentes do Bookstore.

## Contexto
K3d executa nodes K3s como containers Docker. Isso permite praticar recursos Kubernetes sem provisionar máquinas virtuais em um provedor cloud.

O cluster deve ser criado com uma configuração simples, suficiente para executar o backend, o banco e o Ingress.

## Pré-requisitos
- [ ] Issue 001 concluída.
- [ ] Docker funcional.
- [ ] `k3d` e `kubectl` instalados.

## Tarefas

### 1. Criação
- [ ] Definir nome do cluster como `atlas`.
- [ ] Criar o cluster com pelo menos um server node.
- [ ] Planejar o mapeamento de portas do host necessário para o Ingress.
- [ ] Evitar publicar portas do PostgreSQL no host.

### 2. Acesso ao cluster
- [ ] Confirmar que o contexto Kubernetes do cluster foi criado.
- [ ] Selecionar o contexto correto.
- [ ] Consultar os nodes com `kubectl get nodes`.
- [ ] Consultar os namespaces padrão.

### 3. Verificação
- [ ] Confirmar que o node está `Ready`.
- [ ] Consultar os Pods do namespace `kube-system`.
- [ ] Excluir e recriar o cluster uma vez para validar o procedimento de criação.

## Critérios de aceitação
- Cluster `atlas` criado e acessível.
- `kubectl get nodes` mostra os nodes como `Ready`.
- Contexto correto selecionado.
- Porta de entrada planejada sem exposição desnecessária do banco.

## Entrega
- Cluster local funcional.
- Comando ou instrução reproduzível de criação do cluster.

## Definition of Done
A Issue está concluída quando o cluster pode ser criado e administrado localmente e todos os nodes ficam `Ready`.