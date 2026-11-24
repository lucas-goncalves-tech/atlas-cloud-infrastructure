# [010] Configurar Services e DNS interno

## Objetivo
Fornecer endereços estáveis para comunicação entre os componentes do Bookstore dentro do cluster.

## Contexto
Pods podem ser recriados e receber novos endereços IP. Services oferecem um ponto de acesso estável e o DNS do Kubernetes permite que workloads localizem outros Services por nome.

O banco deve permanecer acessível somente pela rede interna do cluster.

## Pré-requisitos
- [ ] Issue 006 concluída.
- [ ] Issue 009 concluída.

## Tarefas

### 1. Service do backend
- [ ] Criar Service ClusterIP para o backend.
- [ ] Configurar `port` e `targetPort` conforme a porta real identificada na Issue 002.
- [ ] Confirmar que os selectors correspondem aos labels do Deployment.

### 2. Service do PostgreSQL
- [ ] Confirmar o Service ClusterIP do PostgreSQL.
- [ ] Verificar se o Service seleciona o Pod correto.
- [ ] Manter o banco sem exposição externa.

### 3. DNS e conectividade
- [ ] Executar um Pod temporário de diagnóstico no namespace.
- [ ] Resolver o nome DNS do Service PostgreSQL.
- [ ] Testar a conectividade na porta 5432.
- [ ] Confirmar que o backend utiliza o DNS do Service, não IP de Pod.

## Critérios de aceitação
- Service do backend encaminha tráfego para os Pods corretos.
- Service PostgreSQL resolve por DNS.
- Backend conecta ao banco pelo nome do Service.
- PostgreSQL não está publicado externamente.

## Entrega
- Manifestos dos Services.
- Configuração do backend usando o DNS interno.

## Definition of Done
A Issue está concluída quando os componentes se comunicam por Services e nomes DNS estáveis, sem depender de IPs individuais dos Pods.