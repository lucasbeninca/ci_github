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


# Como Ativar o Dependabot em um Repositório

O **Dependabot** é uma ferramenta integrada ao GitHub que monitora as dependências do seu projeto e abre Pull Requests automáticos para atualizar versões vulneráveis ou desatualizadas.


### 1. Adicione o arquivo de configuração do Dependabot

1. No seu repositório, clique em **Add file > Create new file**.
2. No campo de nome do arquivo, digite: `.github/dependabot.yml`

3. Cole o exemplo de configuração abaixo para monitorar dependências do Node.js (ajuste conforme sua stack):

 ```
 version: 2
 updates:
   - package-ecosystem: "npm"
     directory: "/"
     schedule:
       interval: "weekly"
 ```

4. Desça até o final da página, adicione uma mensagem de commit e clique em **Commit new file**.

> O Dependabot agora irá monitorar as dependências do seu projeto e abrir Pull Requests automaticamente quando encontrar atualizações.

# Como Configurar o Dependabot para Verificar Dependências Automaticamente

O **Dependabot** pode ser configurado para monitorar e atualizar automaticamente as dependências do seu projeto em intervalos definidos por você. Veja abaixo como fazer isso usando o exemplo de configuração fornecido.

### 1. Crie o arquivo de configuração do Dependabot

1. No seu repositório, clique em **Add file > Create new file**.
2. No campo de nome do arquivo, digite: `.github/dependabot.yml`

3. Cole o conteúdo abaixo no editor:

 ```
 version: 2
 updates:
   - package-ecosystem: "npm" # Veja a documentação para outros valores possíveis
     directory: "/"           # Localização do package.json
     schedule:
       interval: "yearly"     # Pode ser "daily", "weekly" ou "monthly"
 ```

4. Desça até o final da página, adicione uma mensagem de commit e clique em **Commit new file**.

### 2. Personalize o Intervalo de Atualização

- **interval:** define com que frequência o Dependabot irá checar por novas versões das dependências.
- `"daily"`: diariamente
- `"weekly"`: semanalmente
- `"monthly"`: mensalmente
- `"yearly"`: anualmente (como no exemplo acima)

Você pode ajustar o valor conforme a necessidade do seu projeto.

### 3. Como Funciona

- O Dependabot irá monitorar o arquivo `package.json` (ou outro manifest indicado) na raiz do projeto.
- Quando encontrar atualizações disponíveis, ele abrirá automaticamente um Pull Request para sugerir a atualização da dependência.
- Você pode revisar, testar e aprovar a atualização diretamente pelo GitHub.

### 4. Exemplo de Configuração Completa

```
.github/dependabot.yml
version: 2
updates:

package-ecosystem: "npm"
directory: "/"
schedule:
interval: "yearly"

```

> Para mais opções de configuração, consulte a [documentação oficial do Dependabot](https://docs.github.com/code-security/dependabot/dependabot-version-updates/configuration-options-for-the-dependabot.yml-file).

---

Com essa configuração, o Dependabot irá verificar automaticamente as dependências do seu projeto conforme o intervalo definido, ajudando a manter seu projeto seguro e atualizado.



---

## Como Exigir Pull Request para Alterações na Main

Para garantir que nenhum código seja inserido diretamente na branch `main`, é necessário configurar uma **Branch Protection Rule**.

### 1. Acesse as configurações do repositório

1. No repositório, clique em **Settings**.
2. No menu lateral, clique em **Branches**.

### 2. Crie uma regra de proteção para a branch `main`

1. Em **Branch protection rules**, clique em **Add rule**.
2. No campo **Branch name pattern**, digite: `main`

3. Marque a opção:
- **Require a pull request before merging** (Exigir um pull request antes de mesclar)

4. (Opcional) Ative outras opções para reforçar a segurança, como:
- **Require status checks to pass before merging**
- **Require review from Code Owners**

5. Clique em **Create** ou **Save changes**.

> A partir de agora, não será possível fazer push direto na `main`. Toda alteração deverá ser feita via Pull Request.

---

## Resumo dos Arquivos e Configurações

- `.github/dependabot.yml` — Ativa o Dependabot para monitorar dependências.
- **Branch Protection Rule** — Exige Pull Request para qualquer alteração na `main`.

Esses passos ajudam a manter seu projeto mais seguro e organizado, automatizando atualizações e garantindo revisão de código antes de qualquer merge na branch principal.

