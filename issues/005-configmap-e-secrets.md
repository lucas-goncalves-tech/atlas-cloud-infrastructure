# [005] Configurar ConfigMaps e Secrets

## Objetivo
Separar configurações não sensíveis das credenciais utilizadas pelo PostgreSQL e pelo backend.

## Contexto
ConfigMaps armazenam configurações não confidenciais. Secrets armazenam dados sensíveis e podem ser injetados em containers como variáveis de ambiente ou arquivos.

Um Secret Kubernetes não deve ser tratado como cofre criptográfico por padrão. O objetivo desta etapa é evitar credenciais hardcoded nos manifestos e impedir que valores reais sejam versionados.

## Pré-requisitos
- [ ] Issue 002 concluída: variáveis reais do Bookstore identificadas.
- [ ] Issue 004 concluída: namespace `bookstore` criado.

## Tarefas

### 1. ConfigMap
- [ ] Criar ConfigMap para as configurações não sensíveis necessárias.
- [ ] Incluir somente variáveis que a aplicação realmente utiliza.
- [ ] Evitar incluir senhas ou tokens.

### 2. Secret
- [ ] Definir credenciais locais do PostgreSQL.
- [ ] Criar Secret no namespace `bookstore`.
- [ ] Definir como o Secret será criado localmente sem armazenar valores reais no Git.
- [ ] Confirmar que os nomes das chaves correspondem ao modo como o container receberá as variáveis.

### 3. Validação
- [ ] Consultar os metadados do ConfigMap e do Secret.
- [ ] Confirmar que os recursos estão no namespace correto.
- [ ] Verificar que arquivos versionados não contêm senhas reais.

## Critérios de aceitação
- Configurações não sensíveis estão separadas em ConfigMap.
- Credenciais estão em Secret.
- Os nomes das variáveis correspondem à aplicação e à imagem do PostgreSQL.
- Nenhuma credencial real está commitada.

## Entrega
- Manifestos ou instruções reproduzíveis para criar ConfigMap e Secret.
- Arquivo de exemplo sem valores sensíveis, se necessário.

## Definition of Done
A Issue está concluída quando os recursos de configuração existem no namespace e podem ser consumidos pelos workloads sem expor credenciais no Git.