# [007] Validar persistência do PostgreSQL

## Objetivo
Verificar, na prática, que os dados armazenados pelo PostgreSQL não dependem do ciclo de vida de um Pod.

## Contexto
Pods são recursos substituíveis. O volume persistente deve manter os dados mesmo quando o Pod é removido e recriado pelo StatefulSet.

Esta etapa diferencia persistência de armazenamento efêmero do container.

## Pré-requisitos
- [ ] Issue 006 concluída.
- [ ] PostgreSQL Ready.
- [ ] PVC Bound.

## Tarefas

### 1. Criar dado de teste
- [ ] Conectar ao banco usando um cliente executado dentro do cluster.
- [ ] Criar uma tabela ou utilizar uma tabela de teste isolada.
- [ ] Inserir um registro identificável.
- [ ] Consultar o registro para confirmar que foi gravado.

### 2. Recriar o Pod
- [ ] Excluir somente o Pod gerenciado pelo StatefulSet.
- [ ] Aguardar a recriação automática.
- [ ] Verificar que o Pod voltou a ficar Ready.
- [ ] Confirmar que o PVC continua associado.

### 3. Conferir os dados
- [ ] Conectar novamente ao PostgreSQL.
- [ ] Consultar o registro inserido antes da exclusão do Pod.
- [ ] Confirmar que o dado continua presente.
- [ ] Não excluir o PVC durante este teste.

## Critérios de aceitação
- O StatefulSet recria o Pod após sua exclusão.
- O PVC permanece Bound.
- O registro de teste continua disponível após a recriação.
- O teste não depende de manter o mesmo container em execução.

## Entrega
- PVC e StatefulSet configurados para preservar os dados.
- Procedimento de validação reproduzível.

## Definition of Done
A Issue está concluída quando a recriação do Pod não causa perda dos dados armazenados no volume persistente.