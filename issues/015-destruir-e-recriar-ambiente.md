# [015] Destruir e reconstruir o ambiente

## Objetivo
Garantir que o laboratório possa ser recriado de maneira previsível e compreender quais dados são preservados ou descartados.

## Contexto
Infraestrutura declarativa deve poder ser reconstruída sem depender de comandos esquecidos no histórico do terminal. Ao mesmo tempo, remover um cluster pode apagar volumes locais dependendo de como o K3d e o Docker foram configurados.

Esta etapa valida o ciclo de vida completo do ambiente.

## Pré-requisitos
- [ ] Issues essenciais concluídas.
- [ ] Manifestos Kubernetes disponíveis.
- [ ] Bookstore acessível pelo Ingress.

## Tarefas

### 1. Procedimento de implantação
- [ ] Organizar os manifestos em uma ordem de aplicação compreensível.
- [ ] Definir como o namespace e os recursos de configuração serão criados.
- [ ] Definir como Secrets serão recriados sem versionar credenciais.
- [ ] Documentar a ordem necessária para banco, backend e Ingress.
- [ ] Confirmar que o README contém os comandos essenciais para subir o ambiente.

### 2. Reconstrução de workloads
- [ ] Remover os workloads sem apagar intencionalmente o PVC.
- [ ] Aplicar novamente os manifestos.
- [ ] Aguardar PostgreSQL e backend ficarem Ready.
- [ ] Confirmar acesso ao Bookstore pelo hostname local.
- [ ] Confirmar que os dados persistentes continuam disponíveis.

### 3. Remoção completa
- [ ] Identificar quais dados serão perdidos ao remover o cluster.
- [ ] Fazer backup dos dados que deseja preservar.
- [ ] Excluir o cluster K3d.
- [ ] Recriar o cluster e reaplicar a infraestrutura.
- [ ] Restaurar dados somente se o procedimento de backup/restore tiver sido preparado.

## Critérios de aceitação
- O ambiente pode ser implantado seguindo os arquivos do projeto.
- Secrets podem ser recriados sem valores sensíveis no Git.
- A remoção de workloads não apaga inadvertidamente os dados persistentes.
- O impacto da remoção completa do cluster está compreendido.
- A aplicação volta a responder após a reconstrução.

## Entrega
- Manifestos organizados.
- Instruções curtas para criação, implantação e remoção do ambiente.
- Procedimento de backup/restore somente se implementado.

## Definition of Done
A Issue está concluída quando o ambiente pode ser reconstruído de forma previsível e o ciclo de vida dos dados persistentes está compreendido.