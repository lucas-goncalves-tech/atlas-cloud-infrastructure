# [004] Criar namespace e configurar recursos

## Objetivo
Isolar os recursos do laboratório em um namespace e estabelecer limites básicos de consumo.

## Contexto
Namespaces organizam recursos dentro do cluster. ResourceQuota e LimitRange permitem controlar o consumo e definir padrões, evitando que um workload utilize recursos sem limites.

Os valores devem considerar a capacidade real da máquina local, não uma configuração de produção presumida.

## Pré-requisitos
- [ ] Issue 003 concluída.
- [ ] Cluster `atlas` acessível.

## Tarefas

### 1. Namespace
- [ ] Criar o namespace `bookstore`.
- [ ] Verificar sua existência.
- [ ] Configurar o contexto `kubectl` para facilitar comandos nesse namespace, se desejado.

### 2. Limites
- [ ] Consultar CPU e memória disponíveis para Docker/K3d.
- [ ] Criar um LimitRange com valores iniciais razoáveis para containers.
- [ ] Criar ResourceQuota compatível com o orçamento de recursos do laboratório.
- [ ] Verificar como a quota afeta a criação de Pods e PVCs.

### 3. Organização
- [ ] Definir um padrão de labels para os componentes `backend` e `postgres`.
- [ ] Utilizar o namespace `bookstore` nos próximos manifestos.

## Critérios de aceitação
- Namespace `bookstore` existe.
- LimitRange e ResourceQuota estão aplicados.
- Os limites permitem executar os componentes previstos na máquina.
- Há um padrão consistente de labels para selecionar os workloads.

## Entrega
- Manifestos YAML do namespace e dos limites.

## Definition of Done
A Issue está concluída quando o namespace está pronto e os limites aplicados não impedem a implantação planejada.