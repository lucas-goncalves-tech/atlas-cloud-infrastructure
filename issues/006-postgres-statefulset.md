# [006] Provisionar PostgreSQL com StatefulSet

## Objetivo
Provisionar uma instância PostgreSQL dentro do cluster Kubernetes utilizando StatefulSet e armazenamento persistente.

O banco deverá permanecer disponível para o backend através de comunicação interna do cluster.

## Contexto
Diferentemente de um Deployment convencional, o StatefulSet oferece identidade estável aos Pods e é apropriado para workloads que necessitam de identidade e armazenamento persistentes.

O objetivo desta etapa é compreender como o Kubernetes gerencia aplicações stateful.

## Pré-requisitos
- [ ] Issue 003 concluída (Cluster K3d).
- [ ] Issue 004 concluída (Namespaces).
- [ ] Issue 005 concluída (ConfigMap e Secrets).

## Tarefas

### 1. Armazenamento
- [ ] Entender PersistentVolume (PV).
- [ ] Entender PersistentVolumeClaim (PVC).
- [ ] Identificar o StorageClass disponível no cluster.
- [ ] Criar um PVC para os dados do PostgreSQL.

### 2. StatefulSet
- [ ] Criar o manifesto do StatefulSet.
- [ ] Configurar uma versão explícita da imagem PostgreSQL.
- [ ] Configurar variáveis de ambiente utilizando Secrets.
- [ ] Montar o volume persistente no diretório de dados esperado pela imagem.
- [ ] Definir requests e limits de recursos adequados ao ambiente local.

### 3. Exposição interna
- [ ] Criar um Service do tipo ClusterIP.
- [ ] Configurar a porta 5432.
- [ ] Verificar a resolução DNS dentro do cluster.

### 4. Validação
- [ ] Verificar o estado do Pod.
- [ ] Verificar o estado do PVC.
- [ ] Acessar o PostgreSQL internamente.
- [ ] Criar um banco ou registro de teste.
- [ ] Reiniciar o Pod e verificar a persistência dos dados.

## Critérios de aceitação
- PostgreSQL executando no namespace `bookstore`.
- PVC vinculado corretamente.
- Dados preservados após reinicialização do Pod.
- Service acessível internamente.
- Credenciais não expostas diretamente no manifesto.
- PostgreSQL não publicado diretamente na rede externa.

## Entrega
- Manifestos Kubernetes do StatefulSet, PVC e Service.
- Configuração necessária para consumir o Secret.

## Definition of Done
A Issue somente será considerada concluída quando todos os critérios de aceitação forem atendidos e o banco puder ser acessado internamente com dados persistidos.