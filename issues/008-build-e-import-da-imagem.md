# [008] Construir e importar a imagem do Bookstore

## Objetivo
Construir a imagem Docker do backend e disponibilizá-la ao cluster K3d sem depender de um registry remoto.

## Contexto
O node Kubernetes precisa conseguir obter a imagem especificada no Deployment. Em um laboratório local, a imagem pode ser construída na máquina e importada diretamente para o cluster K3d.

A imagem deve refletir o modo de execução real do Bookstore identificado na Issue 002.

## Pré-requisitos
- [ ] Issue 001 concluída.
- [ ] Issue 002 concluída.
- [ ] Issue 003 concluída.
- [ ] Backend consegue ser iniciado seguindo as instruções do repositório.

## Tarefas

### 1. Dockerfile
- [ ] Verificar se o Dockerfile existente atende ao modo de execução de produção.
- [ ] Se necessário, ajustar o Dockerfile sem alterar regras de negócio.
- [ ] Garantir que dependências e etapa de build estejam corretas.
- [ ] Evitar copiar arquivos locais desnecessários para a imagem.
- [ ] Evitar incluir arquivos `.env` ou credenciais na imagem.

### 2. Build e teste
- [ ] Construir a imagem com uma tag local explícita.
- [ ] Executar a imagem fora do Kubernetes.
- [ ] Fornecer as configurações necessárias por ambiente.
- [ ] Confirmar que o processo inicia e escuta na interface de rede apropriada.

### 3. Importação no K3d
- [ ] Importar a imagem para o cluster `atlas`.
- [ ] Confirmar que a imagem está disponível para os nodes.
- [ ] Definir a política de pull adequada para imagem local no Deployment.

## Critérios de aceitação
- Imagem construída sem erro.
- Container inicia fora do Kubernetes.
- Imagem está disponível no cluster K3d.
- Nenhum segredo foi embutido na imagem.

## Entrega
- Dockerfile funcional.
- Instrução de build e importação da imagem.

## Definition of Done
A Issue está concluída quando o cluster consegue iniciar um container a partir da imagem local construída para o Bookstore.