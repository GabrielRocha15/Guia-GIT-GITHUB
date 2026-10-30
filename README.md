# Git e GitHub — Guia de Estudos

Repositório dedicado ao estudo de **Git e GitHub**, ferramentas fundamentais para controle de versão, organização de projetos e colaboração no desenvolvimento de software.

Este material reúne conceitos, comandos e exemplos práticos estudados durante minha formação em tecnologia, servindo também como referência para projetos pessoais e profissionais.

## 📚 Conteúdo

1. [Introdução ao Git](#1-introdução-ao-git)
2. [Inicializando um repositório](#2-inicializando-um-repositório)
3. [Estados e estágios dos arquivos](#3-estados-e-estágios-dos-arquivos)
4. [Adicionando e registrando alterações](#4-adicionando-e-registrando-alterações)
5. [Visualizando alterações e histórico](#5-visualizando-alterações-e-histórico)
6. [Gerenciando arquivos](#6-gerenciando-arquivos)
7. [Alterando commits e histórico](#7-alterando-commits-e-histórico)
8. [Git Reset](#8-git-reset)
9. [Git Alias](#9-git-alias)
10. [Branches e Merge](#10-branches-e-merge)
11. [GitHub e repositórios remotos](#11-github-e-repositórios-remotos)
12. [Pull Requests](#12-pull-requests)
13. [Releases](#13-releases)
14. [Comandos de referência](#14-comandos-de-referência)

---

## 1. Introdução ao Git

O **Git** é um sistema de controle de versão distribuído que permite acompanhar as alterações realizadas em arquivos e projetos ao longo do tempo.

Com ele, é possível:

- Registrar diferentes versões de um projeto.
- Recuperar versões anteriores.
- Trabalhar em funcionalidades separadamente.
- Comparar alterações realizadas no código.
- Colaborar com outros desenvolvedores.

**Git x GitHub**

- **Git:** ferramenta responsável pelo controle de versão local.
- **GitHub:** plataforma online que hospeda repositórios Git e oferece recursos de colaboração.

## 2. Inicializando um repositório

Para iniciar o controle de versão dentro de um diretório de projeto, utilize:

```bash
git init
```

Esse comando inicializa um repositório Git e cria uma pasta oculta chamada `.git`, responsável por armazenar os metadados, configurações e histórico de versões do repositório.

Para verificar o estado atual do projeto:

```bash
git status
```

O comando apresenta informações como:

- Branch atual.
- Arquivos modificados.
- Arquivos não rastreados.
- Arquivos preparados para commit.

## 3. Estados e estágios dos arquivos

O Git trabalha com diferentes estados para acompanhar os arquivos do projeto.

**Untracked (não rastreado)**

Arquivo que ainda não está sendo acompanhado pelo Git.

**Tracked (rastreado)**

Arquivo que já está sob controle de versão do Git.

Um arquivo rastreado pode estar em diferentes situações:

- **Unmodified:** arquivo sem alterações em relação à última versão registrada.
- **Modified:** arquivo modificado desde o último commit.
- **Staged:** arquivo preparado para entrar no próximo commit.

### Os três estágios principais

O fluxo básico de trabalho do Git envolve três áreas:

| Estágio | Descrição |
|---|---|
| Working Directory | Diretório onde os arquivos são criados e modificados. |
| Staging Area | Área onde as alterações são preparadas para o commit. |
| Repository | Histórico de versões registradas por meio dos commits. |

Fluxo de versionamento:

```text
Working Directory
       |
       | git add
       v
  Staging Area
       |
       | git commit
       v
    Repository
```

## 4. Adicionando e registrando alterações

Para adicionar um arquivo à área de preparação:

```bash
git add nome_do_arquivo.py
```

Para adicionar todos os arquivos modificados e não rastreados:

```bash
git add .
```

Para verificar novamente o estado dos arquivos:

```bash
git status
```

Para registrar as alterações no histórico:

```bash
git commit -m "Descrição das alterações"
```

**Boas práticas para mensagens de commit:**

- `feat: adiciona nova funcionalidade`
- `fix: corrige erro no processamento`
- `docs: atualiza documentação`
- `refactor: melhora organização do código`
- `test: adiciona testes automatizados`

## 5. Visualizando alterações e histórico

Para visualizar as diferenças entre os arquivos modificados e a última versão registrada:

```bash
git diff
```

Para visualizar as alterações que já estão na Staging Area:

```bash
git diff --staged
```

Para visualizar o histórico completo de commits:

```bash
git log
```

Para visualizar o histórico de forma resumida:

```bash
git log --oneline
```

Para visualizar o histórico detalhado, incluindo as alterações realizadas em cada commit:

```bash
git log -p
```

## 6. Gerenciando arquivos

O Git também permite remover, restaurar e renomear arquivos.

**Remover um arquivo do repositório e do diretório de trabalho:**

```bash
git rm nome_do_arquivo.py
```

**Remover um arquivo somente do controle de versão, mantendo-o no computador:**

```bash
git rm --cached nome_do_arquivo.py
```

**Retirar um arquivo da Staging Area, mantendo suas alterações:**

```bash
git restore --staged nome_do_arquivo.py
```

**Descartar alterações locais de um arquivo e recuperar a versão presente na Staging Area:**

```bash
git restore nome_do_arquivo.py
```

Atenção: esse último comando descarta as modificações não preparadas para commit.

**Renomear um arquivo:**

```bash
git mv nome_antigo.py nome_novo.py
```

## 7. Alterando commits e histórico

O comando `git commit --amend` permite modificar o último commit.

É útil quando você esqueceu de adicionar algum arquivo ou deseja corrigir a mensagem do último commit.

Exemplo:

```bash
git add arquivo.py
git commit --amend -m "Nova mensagem do commit"
```

Também é possível alterar somente a mensagem:

```bash
git commit --amend -m "Mensagem corrigida"
```

**Atenção:** o amend substitui o último commit por outro, alterando seu identificador (hash). Evite utilizá-lo em commits que já foram compartilhados com outras pessoas, pois isso altera o histórico.

## 8. Git Reset

O `git reset` permite retornar o ponteiro HEAD para um commit anterior, com diferentes comportamentos dependendo da opção utilizada.

Existem três modalidades principais:

**--soft**

```bash
git reset --soft HASH_DO_COMMIT
```

- Retorna o HEAD para o commit selecionado.
- Mantém as alterações dos commits posteriores na Staging Area.
- Não descarta as alterações dos arquivos.

**--mixed**

```bash
git reset --mixed HASH_DO_COMMIT
```

- Retorna o HEAD para o commit selecionado.
- Mantém as alterações dos commits posteriores no Working Directory.
- Retira essas alterações da Staging Area.
- É o comportamento padrão do `git reset`.

**--hard**

```bash
git reset --hard HASH_DO_COMMIT
```

- Retorna o HEAD para o commit selecionado.
- Descarta as alterações posteriores do histórico atual.
- Descarta também as modificações não commitadas na Staging Area e no Working Directory.

Atenção: o `--hard` pode causar perda de trabalho. Utilize com cuidado.

## 9. Git Alias

Aliases são atalhos personalizados para comandos do Git.

Sintaxe:

```bash
git config --global alias.nome_do_atalho "comando"
```

Exemplo:

```bash
git config --global alias.s "status"
```

Agora, em vez de executar:

```bash
git status
```

Basta executar:

```bash
git s
```

O parâmetro `--global` faz com que o atalho fique disponível em todos os repositórios do usuário.

## 10. Branches e Merge

Uma **Branch** é uma ramificação do histórico do projeto que permite desenvolver funcionalidades ou corrigir problemas sem modificar diretamente a linha principal de desenvolvimento.

A branch `main` normalmente representa a linha principal do projeto.

Uma boa prática é desenvolver novas funcionalidades em branches separadas e integrá-las à `main` após revisão e testes.

### Criando uma branch

```bash
git branch nome_da_branch
```

### Listando branches

```bash
git branch
```

### Mudando de branch

```bash
git switch nome_da_branch
```

### Criando e acessando uma branch de uma só vez

```bash
git switch -c nome_da_branch
```

### Realizando Merge

Primeiro, volte para a branch que receberá as alterações:

```bash
git switch main
```

Depois, execute o merge:

```bash
git merge nome_da_branch
```

Para adicionar uma mensagem personalizada em um merge que gerar um novo commit:

```bash
git merge -m "Integra nova funcionalidade" nome_da_branch
```

O merge integra as alterações da branch selecionada à branch atual.

### Excluindo uma branch

Após integrar e validar as alterações:

```bash
git branch -d nome_da_branch
```

O parâmetro `-d` remove uma branch já integrada com segurança.

## 11. GitHub e repositórios remotos

O GitHub permite hospedar repositórios Git remotamente, facilitando o compartilhamento, backup e colaboração em projetos.

### 11.1 Criando um repositório no GitHub

1. Acesse o GitHub.
2. Clique em **New repository**.
3. Defina o nome do projeto.
4. Escolha a visibilidade pública ou privada.
5. Clique em **Create repository**.

Para facilitar a primeira sincronização, se o projeto já existe localmente, é interessante criar o repositório remoto sem README, `.gitignore` ou licença inicial.

### 11.2 Preparando o projeto local

Dentro do diretório do projeto:

```bash
git init
git add .
git commit -m "Initial commit"
git branch -M main
```

### 11.3 Configurando o repositório remoto

Para vincular o repositório local ao GitHub utilizando SSH:

```bash
git remote add origin git@github.com:USUARIO/REPOSITORIO.git
```

Caso o endereço remoto já exista e precise ser alterado:

```bash
git remote set-url origin git@github.com:USUARIO/REPOSITORIO.git
```

Para visualizar os endereços remotos configurados:

```bash
git remote -v
```

### 11.4 Configurando autenticação SSH

Para gerar uma chave SSH:

```bash
ssh-keygen -t ed25519 -C "seu-email@example.com"
```

Depois, adicione a chave pública ao GitHub em:

**Settings → SSH and GPG keys → New SSH key**

A chave pública normalmente fica em:

```text
~/.ssh/id_ed25519.pub
```

Para testar a conexão:

```bash
ssh -T git@github.com
```

### 11.5 Enviando arquivos para o GitHub

Para enviar os commits locais:

```bash
git push -u origin main
```

O parâmetro `-u` configura a branch remota como referência padrão para os próximos envios.

Nas próximas atualizações, basta utilizar:

```bash
git push
```

### 11.6 Atualizando o repositório local

Para baixar e integrar alterações do repositório remoto:

```bash
git pull origin main
```

O comando `git pull` realiza a busca das alterações remotas e tenta integrá-las à branch local.

**Observação:** se o repositório remoto já possuir commits independentes, como um README criado pelo GitHub, pode ser necessário integrar os históricos:

```bash
git pull origin main --allow-unrelated-histories
```

Utilize essa opção somente quando realmente existirem históricos independentes que precisam ser unidos.

## 12. Pull Requests

Um **Pull Request (PR)** é uma solicitação para integrar alterações de uma branch em outra.

É um dos principais recursos de colaboração do GitHub.

Fluxo básico:

1. Criar uma branch para desenvolver uma funcionalidade.
2. Realizar as alterações no código.
3. Criar commits.
4. Enviar a branch para o GitHub.
5. Abrir um Pull Request.
6. Revisar as alterações.
7. Executar testes e corrigir possíveis problemas.
8. Aprovar e realizar o merge.

Os Pull Requests permitem revisar códigos, discutir implementações e identificar problemas antes de integrar alterações à branch principal.

## 13. Releases

Uma **Release** representa uma versão publicada do projeto, geralmente associada a uma tag do Git.

É utilizada para organizar versões estáveis e disponibilizar entregas do software.

Exemplos de identificação:

- `v1.0.0` — primeira versão estável.
- `v1.1.0` — nova funcionalidade.
- `v1.1.1` — correção de problemas.

Para criar uma tag:

```bash
git tag v1.0.0
```

Para enviar a tag ao GitHub:

```bash
git push origin v1.0.0
```

Também é possível criar e publicar Releases diretamente pela interface do GitHub, adicionando descrição, notas de atualização e arquivos relacionados à versão.

## 14. Comandos de referência

| Comando | Finalidade |
|---|---|
| `git init` | Inicializa um repositório. |
| `git status` | Exibe o estado dos arquivos. |
| `git add .` | Adiciona alterações à Staging Area. |
| `git commit -m` | Registra um commit. |
| `git diff` | Compara alterações não preparadas. |
| `git diff --staged` | Compara alterações preparadas. |
| `git log` | Exibe o histórico. |
| `git log --oneline` | Exibe histórico resumido. |
| `git restore` | Restaura arquivos. |
| `git rm` | Remove arquivos. |
| `git mv` | Renomeia ou move arquivos. |
| `git reset` | Retorna o HEAD para outro commit. |
| `git branch` | Lista ou cria branches. |
| `git switch` | Alterna entre branches. |
| `git merge` | Integra branches. |
| `git push` | Envia commits ao repositório remoto. |
| `git pull` | Atualiza o repositório local. |
| `git clone` | Clona um repositório remoto. |
| `git remote -v` | Exibe os repositórios remotos. |
| `git tag` | Lista ou cria tags. |
| `git help` | Acessa a documentação de comandos. |

Para consultar a ajuda geral:

```bash
git -h
```

Para consultar a documentação de um comando específico:

```bash
git help commit
```

---

## 🎯 Objetivo de aprendizagem

Desenvolver domínio prático sobre controle de versão utilizando Git e GitHub, aplicando os conceitos em projetos pessoais e profissionais.

**Próximos conhecimentos a aprofundar:**

- Resolução de conflitos de merge.
- Rebase e reorganização de histórico.
- GitHub Actions e CI/CD.
- Proteção de branches.
- Issues e gerenciamento de projetos.
- Boas práticas de colaboração.

## 📌 Status de aprendizagem

- [x] Fundamentos do Git.
- [x] Inicialização e gerenciamento de repositórios.
- [x] Commits e histórico de versões.
- [x] Branches e Merge.
- [x] Integração com GitHub.
- [ ] Pull Requests na prática.
- [ ] Resolução de conflitos.
- [ ] Rebase.
- [ ] GitHub Actions e CI/CD.
- [ ] Proteção de branches e permissões.

---

**Tecnologias:** Git | GitHub | Git Bash | SSH

*Material desenvolvido durante os estudos de versionamento de código — Roadmap de Python e Engenharia de Dados.*
