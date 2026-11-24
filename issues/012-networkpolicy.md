# [012] Restringir comunicação com NetworkPolicy

## Objetivo
Aplicar regras de tráfego entre os componentes para reduzir comunicação desnecessária dentro do namespace.

## Contexto
NetworkPolicy permite definir quais conexões de entrada e saída são permitidas para Pods selecionados. O comportamento depende do suporte do plugin de rede (CNI) do cluster.

A política deve permitir o funcionamento do Bookstore e bloquear acessos que não façam parte do fluxo esperado.

## Pré-requisitos
- [ ] Issues 006, 009, 010 e 011 concluídas.
- [ ] Confirmar suporte a NetworkPolicy no CNI utilizado pelo K3d.

## Tarefas

### 1. Verificação do ambiente
- [ ] Identificar o CNI ativo no cluster.
- [ ] Confirmar se ele aplica NetworkPolicy.
- [ ] Não considerar a política validada apenas porque o objeto YAML foi aceito pela API.

### 2. Políticas
- [ ] Definir quais Pods podem receber tráfego do Ingress Controller.
- [ ] Permitir que o backend acesse PostgreSQL na porta 5432.
- [ ] Restringir acesso ao PostgreSQL a workloads autorizados.
- [ ] Considerar DNS e demais dependências necessárias antes de aplicar políticas de egress.
- [ ] Usar labels consistentes nos seletores.

### 3. Testes
- [ ] Testar o fluxo permitido entre backend e PostgreSQL.
- [ ] Testar o fluxo de entrada pelo Ingress.
- [ ] Testar uma conexão que deve ser bloqueada.
- [ ] Corrigir regras que bloqueiem tráfego necessário.

## Critérios de aceitação
- CNI aplica efetivamente NetworkPolicy.
- Tráfego necessário ao Bookstore continua funcionando.
- Acesso não autorizado ao PostgreSQL é bloqueado.
- As políticas não dependem de seletores inexistentes.

## Entrega
- Manifestos NetworkPolicy aplicados ao namespace.

## Definition of Done
A Issue está concluída quando as políticas foram testadas na rede real do cluster e os fluxos permitidos e negados correspondem ao desenho definido.