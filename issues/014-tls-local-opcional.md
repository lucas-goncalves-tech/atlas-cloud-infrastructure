# [014] Habilitar TLS local no Ingress (opcional)

## Objetivo
Configurar HTTPS local para compreender terminação TLS no Ingress Controller.

## Contexto
O Ingress Controller pode terminar TLS e encaminhar tráfego HTTP para o Service interno. Para um laboratório local, pode ser utilizado um certificado de desenvolvimento autoassinado ou uma autoridade certificadora local.

Este exercício não exige domínio público nem certificado emitido por uma autoridade pública.

## Pré-requisitos
- [ ] Issue 011 concluída.
- [ ] Hostname local do Bookstore configurado.

## Tarefas

### 1. Certificado
- [ ] Gerar certificado e chave para o hostname local.
- [ ] Incluir o hostname correto no Subject Alternative Name (SAN).
- [ ] Proteger a chave privada e não versioná-la no Git.

### 2. Secret e Ingress
- [ ] Criar Secret do tipo TLS no namespace `bookstore`.
- [ ] Configurar a seção TLS do recurso Ingress.
- [ ] Confirmar que o controller reconhece o certificado.

### 3. Validação
- [ ] Acessar o hostname por HTTPS.
- [ ] Inspecionar o certificado apresentado.
- [ ] Entender o aviso de confiança quando a CA/certificado não está confiável no sistema.
- [ ] Confirmar que o encaminhamento ao backend continua funcionando.

## Critérios de aceitação
- Secret TLS contém certificado e chave correspondentes.
- Ingress utiliza o Secret correto.
- HTTPS funciona no hostname local.
- Chave privada não está versionada.

## Entrega
- Instruções para gerar o certificado local.
- Configuração TLS do Ingress sem material privado commitado.

## Definition of Done
A Issue está concluída quando o Ingress termina TLS corretamente e o Bookstore responde por HTTPS local.

> Issue opcional: pode ser deixada para depois das etapas essenciais.