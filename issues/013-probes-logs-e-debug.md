# [013] Configurar probes e praticar troubleshooting

## Objetivo
Utilizar mecanismos nativos do Kubernetes para verificar a saúde do backend e diagnosticar falhas comuns.

## Contexto
ReadinessProbe controla quando um Pod pode receber tráfego. LivenessProbe permite reiniciar um container que deixou de funcionar corretamente. StartupProbe protege aplicações que demoram para iniciar.

Essas verificações precisam corresponder ao comportamento real do Bookstore. Não configure uma rota de health check fictícia.

## Pré-requisitos
- [ ] Issue 009 concluída.
- [ ] Issue 010 concluída.
- [ ] Issue 011 concluída.
- [ ] Endpoint ou método de verificação identificado na Issue 002.

## Tarefas

### 1. Probes
- [ ] Verificar se a aplicação possui endpoint de health check.
- [ ] Configurar ReadinessProbe usando um endpoint ou comando válido.
- [ ] Configurar LivenessProbe somente com uma verificação adequada.
- [ ] Configurar StartupProbe se o tempo de inicialização justificar.
- [ ] Ajustar delays, timeouts e thresholds com base no tempo real de inicialização.

### 2. Logs e eventos
- [ ] Consultar logs do backend com `kubectl logs`.
- [ ] Consultar logs de um container anterior após reinício, quando aplicável.
- [ ] Consultar eventos do namespace.
- [ ] Inspecionar Pod com `kubectl describe`.
- [ ] Identificar diferença entre `Pending`, `CrashLoopBackOff`, `ImagePullBackOff` e `Running`.

### 3. Falha controlada
- [ ] Introduzir uma configuração inválida de forma controlada.
- [ ] Observar o estado do Pod e os eventos.
- [ ] Identificar a causa nos logs ou na descrição do recurso.
- [ ] Corrigir a configuração e confirmar a recuperação.

## Critérios de aceitação
- Probes correspondem a verificações reais.
- Pod só recebe tráfego quando está Ready.
- É possível consultar logs e eventos relevantes.
- Uma falha controlada foi diagnosticada e corrigida.

## Entrega
- Configuração de probes no manifesto do backend.
- Procedimento mínimo para consultar logs, eventos e estado dos Pods.

## Definition of Done
A Issue está concluída quando o estado de saúde do backend é monitorado por probes válidas e uma falha comum pode ser diagnosticada com ferramentas Kubernetes.