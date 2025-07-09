* Inicializa um novo repositório  
`git init`

* Clona um repositório remoto  
`git clone <url-do-repositorio>`

* Adiciona arquivos ao stage  
`git add <arquivo-ou-pasta>`

* Adiciona todos os arquivos ao stage  
`git add .`

* Faz commit das alterações  
`git commit -m "Mensagem do commit"`

* Mostra o status dos arquivos  
`git status`

* Mostra o histórico de commits  
`git log`

* Exibe diferenças entre arquivos  
`git diff`

* Remove arquivos do stage  
`git reset <arquivo>`

* Renomeia arquivos  
`git mv <arquivo-antigo> <arquivo-novo>`

* Cria uma nova branch e troca para ela  
`git checkout -b <nome-da-branch>`

* Troca para uma branch existente  
`git checkout <nome-da-branch>`

* Adiciona um repositório remoto  
`git remote add origin <url-do-repositorio>`

* Visualiza os remotos configurados  
`git remote -v`

* Envia alterações para o repositório remoto  
`git push origin <nome-da-branch>`

* Envia branch e define o upstream  
`git push --set-upstream origin <nome-da-branch>`

* Baixa alterações do repositório remoto  
`git pull origin <nome-da-branch>`

* Inicializa o gitflow no repositório  
`git flow init`

* Inicia uma nova feature  
`git flow feature`

# Criando workflwo

## Como Configurar CI com GitHub Actions Usando Apenas o GitHub Web

Abaixo está um guia **completo em Markdown** para adicionar Integração Contínua (CI) ao seu projeto Node.js usando o GitHub Actions, sem precisar sair do navegador.

### 1. Crie o Arquivo de Workflow no GitHub Web

1. No repositório do seu projeto, clique em **Add file > Create new file**.
2. No campo de nome do arquivo, digite: `.github/workflows/ci.yml`
3. Cole o conteúdo abaixo no editor:

 ```
 name: Workflow de Integração Contínua

 on:
   pull_request:
     branches: [ "main" ]

 jobs:
   tests:
     runs-on: ubuntu-latest
     steps:
       - uses: actions/checkout@v4
       - name: Use Node.js ${{ matrix.node-version }}
         uses: actions/setup-node@v4
         with:
           node-version: ${{ matrix.node-version }}
           cache: 'npm'
       - run: npm install
       - run: npm test
 ```

4. Desça até o final da página, adicione uma mensagem de commit e clique em **Commit new file**.

### 2. Explique o Workflow no README.md

Inclua um passo a passo no seu `README.md` para que outros desenvolvedores entendam como funciona a CI do projeto. Você pode copiar e colar o texto abaixo:

#### 🚀 Integração Contínua com GitHub Actions

Este projeto utiliza **GitHub Actions** para rodar testes automaticamente a cada pull request na branch `main`.

**Como funciona:**
- Ao abrir um pull request para a branch `main`, o workflow é acionado.
- O workflow faz checkout do código, instala as dependências do Node.js, utiliza cache para acelerar builds e executa os testes com `npm test`.

**Arquivo de workflow:**

```
name: Workflow de Integração Contínua

on:
pull_request:
branches: [ "main" ]

jobs:
tests:
runs-on: ubuntu-latest
steps:
- uses: actions/checkout@v4
- name: Use Node.js ${{ matrix.node-version }}
uses: actions/setup-node@v4
with:
node-version: ${{ matrix.node-version }}
cache: 'npm'
- run: npm install
- run: npm test

```

Para mais detalhes sobre personalização de workflows, consulte a [documentação oficial do GitHub Actions](https://docs.github.com/pt/actions).

### 3. Pronto!

Agora, toda vez que um pull request for aberto para a branch `main`, os testes serão executados automaticamente, ajudando a garantir a qualidade do seu projeto.

**Dica:** Todos esses passos podem ser feitos diretamente pelo GitHub Web, sem necessidade de comandos no terminal.
