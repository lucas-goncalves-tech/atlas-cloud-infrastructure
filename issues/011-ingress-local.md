# [011] Expor o Bookstore por Ingress local

## Objetivo
Permitir acesso ao backend a partir da máquina host usando um hostname local e um Ingress Controller.

## Contexto
Ingress define regras HTTP/HTTPS para encaminhar requisições a Services do cluster. O Ingress Controller implementa essas regras. Neste laboratório será utilizado NGINX Ingress Controller.

O acesso será local; não será necessário comprar domínio ou publicar o serviço na internet.

## Pré-requisitos
- [ ] Issue 003 concluída com mapeamento de portas planejado.
- [ ] Issue 009 concluída.
- [ ] Issue 010 concluída.

## Tarefas

### 1. Ingress Controller
- [ ] Instalar NGINX Ingress Controller compatível com K3d.
- [ ] Configurar o acesso do host às portas HTTP do controller.
- [ ] Aguardar os Pods do controller ficarem Ready.

### 2. Regra Ingress
- [ ] Criar recurso Ingress no namespace `bookstore`.
- [ ] Definir hostname local para a aplicação.
- [ ] Encaminhar requisições ao Service do backend.
- [ ] Utilizar a porta definida no Service.
- [ ] Configurar a classe de Ingress correspondente ao controller instalado.

### 3. Acesso local
- [ ] Configurar resolução do hostname na máquina host, por exemplo via arquivo hosts.
- [ ] Fazer uma requisição HTTP com curl.
- [ ] Abrir o endereço no navegador.
- [ ] Confirmar que a resposta vem do backend.

## Critérios de aceitação
- NGINX Ingress Controller está Ready.
- Regra Ingress aponta para o Service correto.
- Hostname local resolve para o endereço local apropriado.
- Backend responde por HTTP através do Ingress.

## Entrega
- Manifestos ou instruções de instalação do Ingress Controller.
- Manifesto Ingress do Bookstore.

## Definition of Done
A Issue está concluída quando o Bookstore pode ser acessado pela máquina host através do hostname local e do Ingress.