# Guia de Express.js — Criação de servidores e aplicações básicas

## 1. O que é Express?

O **Express.js** é um framework para Node.js que facilita a criação de servidores HTTP e APIs utilizando JavaScript.

Com ele, podemos criar aplicações capazes de:

- Receber requisições de páginas HTML, CSS e JavaScript.
- Receber e enviar informações em formato JSON.
- Processar dados enviados por formulários.
- Criar APIs para comunicação entre frontend e backend.
- Consultar, cadastrar, alterar e excluir informações.
- Criar rotas para diferentes funcionalidades.
- Implementar sistemas de login e cadastro.
- Conectar aplicações a bancos de dados.
- Disponibilizar arquivos para outros dispositivos.
- Construir aplicações web completas.

### Como funciona um servidor Express?

O servidor permanece aguardando requisições. Quando recebe uma, verifica o endereço solicitado, o método HTTP e os dados enviados. Em seguida, executa a lógica correspondente e devolve uma resposta.

Exemplo de comunicação:

```text
Frontend (HTML, CSS e JavaScript)
              |
              | Requisição HTTP
              v
        Servidor Express
              |
              | Processamento
              v
       Banco de dados (opcional)
              |
              | Resultado
              v
        Servidor Express
              |
              | Resposta HTTP
              v
            Frontend
```

O Express não é um banco de dados e tampouco substitui o Node.js. Ele utiliza o Node.js para executar o código JavaScript no servidor e oferece ferramentas para organizar a comunicação HTTP.

---

## 2. Preparando o ambiente

Antes de começar, instale o Node.js em seu computador.

Site oficial:

https://nodejs.org/

Depois, abra o terminal na pasta em que deseja criar o projeto.

### 2.1. Criando o projeto

Execute:

```bash
npm init -y
```

Esse comando cria o arquivo `package.json`, responsável por armazenar informações sobre o projeto, suas dependências e seus comandos.

### 2.2. Instalando o Express

Execute:

```bash
npm install express
```

O npm instalará o Express e registrará a dependência no projeto.

### 2.3. Estrutura inicial

Uma organização simples pode ser:

```text
meu-servidor/
│
├── node_modules/
├── package.json
├── package-lock.json
├── server.js
│
└── public/
    ├── index.html
    ├── style.css
    └── script.js
```

Descrição dos arquivos:

| Arquivo ou pasta | Função |
|---|---|
| `node_modules/` | Armazena as dependências instaladas. |
| `package.json` | Registra as configurações e dependências do projeto. |
| `package-lock.json` | Registra versões específicas das dependências. |
| `server.js` | Contém o código principal do servidor. |
| `public/` | Armazena arquivos públicos do frontend. |
| `index.html` | Estrutura da página. |
| `style.css` | Estilos visuais. |
| `script.js` | Comportamentos executados no navegador. |

A pasta `node_modules` não precisa ser enviada ao GitHub: normalmente, ela é ignorada pelo Git e recriada com `npm install`.

---

## 3. Criando o primeiro servidor

Crie um arquivo chamado `server.js`.

```javascript
const express = require("express");

const app = express();

const port = 3000;

app.get("/", (req, res) => {
    res.send("Meu servidor está funcionando!");
});

app.listen(port, () => {
    console.log(`Servidor iniciado na porta ${port}`);
});
```

### Entendendo o código

**1. Importando o Express**

```javascript
const express = require("express");
```

Importa o módulo instalado pelo npm.

**2. Criando a aplicação**

```javascript
const app = express();
```

A variável `app` representa a aplicação Express. É por meio dela que definimos rotas, configurações e middlewares.

**3. Definindo a porta**

```javascript
const port = 3000;
```

A porta identifica o ponto de comunicação em que o servidor receberá conexões.

**4. Criando uma rota**

```javascript
app.get("/", (req, res) => {
    res.send("Meu servidor está funcionando!");
});
```

Essa rota responde às requisições HTTP do tipo `GET` feitas para `/`.

**5. Iniciando o servidor**

```javascript
app.listen(port, () => {
    console.log(`Servidor iniciado na porta ${port}`);
});
```

O servidor começa a escutar na porta definida.

### Executando

No terminal:

```bash
node server.js
```

Acesse no navegador:

http://localhost:3000/

Se tudo estiver correto, a mensagem aparecerá na página.

`localhost` representa o próprio computador. A porta `3000` é a utilizada pelo servidor nesse exemplo.

---

## 4. O que são `req` e `res`?

Esses dois parâmetros aparecem frequentemente nas rotas do Express.

```javascript
app.get("/exemplo", (req, res) => {
    // Código da rota
});
```

- `req`: representa a requisição recebida.
- `res`: representa a resposta que o servidor enviará.

A requisição pode conter o endereço acessado, parâmetros, cabeçalhos e dados enviados pelo cliente.

A resposta pode conter texto, HTML, JSON, arquivos, códigos de status HTTP e outras informações.

Os nomes `req` e `res` são convencionais. Você pode escolher outros nomes, embora seja recomendável manter essa convenção.

---

## 5. Criando diferentes rotas

Uma rota associa um método HTTP e um caminho a determinada funcionalidade.

### 5.1. Rota GET

Utilizada principalmente para consultar ou obter informações.

```javascript
app.get("/usuario", (req, res) => {
    res.send("Página do usuário");
});
```

Acesse:

```text
http://localhost:3000/usuario
```

### 5.2. Rota POST

Utilizada normalmente para enviar dados e criar registros.

```javascript
app.post("/usuario", (req, res) => {
    res.send("Requisição de cadastro recebida");
});
```

Essa rota não será executada simplesmente ao abrir o endereço no navegador, pois a navegação comum utiliza `GET`.

Para testar `POST`, utilize o `fetch()` no frontend ou uma ferramenta de testes de APIs.

### 5.3. Rota PUT

Utilizada normalmente para substituir ou atualizar um recurso existente.

```javascript
app.put("/usuario", (req, res) => {
    res.send("Requisição de atualização recebida");
});
```

### 5.4. Rota PATCH

Utilizada normalmente para atualizar parcialmente um recurso.

```javascript
app.patch("/usuario", (req, res) => {
    res.send("Requisição de atualização parcial recebida");
});
```

### 5.5. Rota DELETE

Utilizada normalmente para solicitar a exclusão de um recurso.

```javascript
app.delete("/usuario", (req, res) => {
    res.send("Requisição de exclusão recebida");
});
```

**Importante:** criar essas rotas não faz com que dados sejam realmente cadastrados, atualizados ou excluídos. Para isso, é necessário implementar a lógica correspondente e, geralmente, armazenar os dados em algum lugar.

---

## 6. Enviando respostas ao cliente

O Express possui diferentes métodos para construir respostas.

### 6.1. Enviar texto

```javascript
app.get("/texto", (req, res) => {
    res.send("Olá, mundo!");
});
```

### 6.2. Enviar JSON

```javascript
app.get("/dados", (req, res) => {
    res.json({
        nome: "Willian",
        idade: 16,
        ativo: true
    });
});
```

O objeto JavaScript será serializado para JSON e enviado ao cliente.

JSON é útil para transmitir informações entre o frontend e o backend, pois pode representar textos, números, valores booleanos, listas e objetos.

### 6.3. Definir o código de status HTTP

```javascript
app.get("/nao-encontrado", (req, res) => {
    res.status(404).json({
        erro: "Recurso não encontrado"
    });
});
```

Alguns códigos importantes:

| Código | Significado |
|---|---|
| `200` | Requisição concluída com sucesso. |
| `201` | Recurso criado com sucesso. |
| `204` | Sucesso sem conteúdo na resposta. |
| `400` | Requisição inválida. |
| `401` | Autenticação necessária ou inválida. |
| `403` | Acesso proibido. |
| `404` | Recurso não encontrado. |
| `500` | Erro interno do servidor. |

Exemplo de resposta de criação:

```javascript
res.status(201).json({
    mensagem: "Cadastro realizado"
});
```

O código de status informa ao cliente o resultado da operação. Não é necessário utilizar sempre `200`.

---

## 7. Recebendo dados JSON

Uma das aplicações mais úteis do Express é receber informações enviadas pelo frontend.

Para isso, precisamos configurar um middleware que interprete o corpo das requisições JSON.

### 7.1. Configurando o middleware

Adicione ao `server.js`:

```javascript
app.use(express.json());
```

Coloque essa configuração antes das rotas que precisam acessar `req.body`.

O `express.json()` interpreta corpos de requisições cujo formato é JSON e disponibiliza o resultado em `req.body`.

### 7.2. Criando uma rota que recebe informações

```javascript
app.post("/api/usuario", (req, res) => {
    const dados = req.body;

    console.log(dados);

    res.json({
        mensagem: "Dados recebidos",
        usuario: dados
    });
});
```

Imagine que o cliente envie:

```json
{
    "nome": "Willian",
    "idade": 16
}
```

No servidor, podemos acessar:

```javascript
req.body.nome
req.body.idade
```

O resultado será:

```text
Willian
16
```

**Atenção:** não confie automaticamente nos dados recebidos. O cliente pode enviar campos ausentes, tipos inesperados ou informações maliciosas. Valide os dados antes de utilizá-los.

---

## 8. Enviando dados do frontend com `fetch()`

O `fetch()` permite que o JavaScript executado no navegador faça requisições HTTP ao servidor.

Exemplo de envio:

```javascript
async function enviarDados() {
    try {
        const resposta = await fetch("/api/usuario", {
            method: "POST",

            headers: {
                "Content-Type": "application/json",
                "Accept": "application/json"
            },

            body: JSON.stringify({
                nome: "Willian",
                idade: 16
            })
        });

        const dados = await resposta.json();

        if (!resposta.ok) {
            throw new Error(
                dados.erro ?? `Erro HTTP: ${resposta.status}`
            );
        }

        console.log(dados);

    } catch (erro) {
        console.error("Falha na requisição:", erro);
    }
}
```

Para executar a função, por exemplo:

```javascript
enviarDados();
```

### Como ocorre a comunicação?

1. O frontend cria um objeto JavaScript.
2. `JSON.stringify()` transforma esse objeto em uma string JSON.
3. `fetch()` envia a requisição ao servidor.
4. O Express interpreta o JSON por meio de `express.json()`.
5. A rota acessa os dados em `req.body`.
6. O servidor devolve uma resposta JSON.
7. O frontend interpreta a resposta com `resposta.json()`.

### Por que utilizar `JSON.stringify()`?

O `body` de uma requisição `fetch()` não aceita um objeto JavaScript comum como corpo de uma requisição HTTP. Ao enviar JSON, transformamos o objeto em texto e informamos seu formato por meio do cabeçalho `Content-Type`.

### Por que verificar `resposta.ok`?

O `fetch()` não rejeita automaticamente a promessa quando o servidor responde com códigos como `400` ou `500`.

Por isso, a aplicação precisa verificar o status HTTP quando deseja tratar essas respostas como erros.

---

## 9. Servindo arquivos HTML, CSS e JavaScript

O Express também pode disponibilizar arquivos estáticos para o navegador.

Imagine esta estrutura:

```text
meu-servidor/
│
├── server.js
│
└── public/
    ├── index.html
    ├── style.css
    └── script.js
```

Adicione ao servidor:

```javascript
app.use(express.static("public"));
```

Agora, o conteúdo da pasta `public` poderá ser acessado pelo navegador.

Por exemplo:

```text
http://localhost:3000/index.html
http://localhost:3000/style.css
http://localhost:3000/script.js
```

A página HTML poderá importar o CSS e o JavaScript normalmente:

```html
<link rel="stylesheet" href="/style.css">

<script src="/script.js" defer></script>
```

Como o diretório `public` é servido como raiz dos arquivos estáticos, não é necessário incluir `public` nos endereços.

### Servindo a página inicial em `/`

O Express normalmente disponibiliza `index.html` quando a raiz do diretório estático é solicitada. Portanto, com a configuração acima, você também poderá acessar:

```text
http://localhost:3000/
```

### Usando caminhos absolutos no servidor

Em projetos que podem ser executados a partir de diferentes diretórios, é mais seguro construir o caminho dos arquivos a partir da localização do próprio código.

```javascript
const path = require("path");

app.use(
    express.static(path.join(__dirname, "public"))
);
```

`__dirname` representa o diretório do arquivo JavaScript atual no sistema de módulos CommonJS.

Essa abordagem evita depender do diretório em que o comando `node` foi executado.

---

## 10. Trabalhando com parâmetros nas rotas

O Express permite que parte do endereço seja variável.

### 10.1. Parâmetros de rota

```javascript
app.get("/usuario/:id", (req, res) => {
    const id = req.params.id;

    res.json({
        id: id
    });
});
```

Ao acessar:

```text
http://localhost:3000/usuario/25
```

O servidor receberá:

```javascript
req.params.id
```

Resultado:

```text
"25"
```

Observe que o valor é uma string, mesmo que represente um número.

Se precisar utilizá-lo como número, converta-o e valide-o:

```javascript
const id = Number(req.params.id);

if (!Number.isInteger(id) || id <= 0) {
    return res.status(400).json({
        erro: "ID inválido"
    });
}
```

### 10.2. Parâmetros de consulta

Também podemos receber informações pela query string.

```javascript
app.get("/pesquisar", (req, res) => {
    const termo = req.query.termo;

    res.json({
        pesquisa: termo
    });
});
```

Acesse:

```text
http://localhost:3000/pesquisar?termo=programacao
```

O resultado será semelhante a:

```json
{
    "pesquisa": "programacao"
}
```

A query string começa após `?`. Diferentes parâmetros podem ser separados por `&`.

Exemplo:

```text
/pesquisar?termo=programacao&pagina=2
```

Nesse caso:

```javascript
req.query.termo
req.query.pagina
```

### 10.3. Diferenças entre os três locais de dados

| Origem | Como acessar | Exemplo |
|---|---|---|
| Parâmetro de rota | `req.params` | `/usuario/25` |
| Parâmetro de consulta | `req.query` | `/pesquisar?termo=Python` |
| Corpo da requisição | `req.body` | JSON enviado por `POST` |

Essas três formas resolvem necessidades diferentes. Não é necessário enviar todos os dados sempre pelo corpo da requisição.

---

## 11. Criando uma API simples de tarefas

Uma API pode administrar uma coleção de informações sem precisar, inicialmente, de um banco de dados.

O exemplo abaixo mantém tarefas em memória.

```javascript
const express = require("express");

const app = express();
const port = 3000;

app.use(express.json());

let proximoId = 1;
const tarefas = [];

// Listar todas as tarefas
app.get("/api/tarefas", (req, res) => {
    res.json(tarefas);
});

// Criar uma tarefa
app.post("/api/tarefas", (req, res) => {
    const { titulo } = req.body;

    if (typeof titulo !== "string" || !titulo.trim()) {
        return res.status(400).json({
            erro: "Informe um título válido"
        });
    }

    const tarefa = {
        id: proximoId++,
        titulo: titulo.trim(),
        concluida: false
    };

    tarefas.push(tarefa);

    res.status(201).json(tarefa);
});

// Buscar uma tarefa específica
app.get("/api/tarefas/:id", (req, res) => {
    const id = Number(req.params.id);

    const tarefa = tarefas.find(
        item => item.id === id
    );

    if (!tarefa) {
        return res.status(404).json({
            erro: "Tarefa não encontrada"
        });
    }

    res.json(tarefa);
});

// Excluir uma tarefa
app.delete("/api/tarefas/:id", (req, res) => {
    const id = Number(req.params.id);

    const indice = tarefas.findIndex(
        item => item.id === id
    );

    if (indice === -1) {
        return res.status(404).json({
            erro: "Tarefa não encontrada"
        });
    }

    tarefas.splice(indice, 1);

    res.status(204).end();
});

app.listen(port, () => {
    console.log(`Servidor disponível na porta ${port}`);
});
```

### O que essa API permite fazer?

| Método | Endereço | Operação |
|---|---|---|
| `GET` | `/api/tarefas` | Lista as tarefas. |
| `POST` | `/api/tarefas` | Cria uma tarefa. |
| `GET` | `/api/tarefas/1` | Busca a tarefa de ID 1. |
| `DELETE` | `/api/tarefas/1` | Exclui a tarefa de ID 1. |

Para criar uma tarefa, envie um `POST` com este corpo JSON:

```json
{
    "titulo": "Estudar Express"
}
```

A resposta será semelhante a:

```json
{
    "id": 1,
    "titulo": "Estudar Express",
    "concluida": false
}
```

### Limitação importante

A lista `tarefas` existe somente na memória do processo. Se o servidor for reiniciado, todas as tarefas serão perdidas.

Além disso, cada instância do servidor mantém sua própria lista. Para conservar os dados entre reinicializações, utilize armazenamento persistente, como SQLite, PostgreSQL ou outro banco de dados.

---

## 12. Recebendo dados de formulários HTML

Um formulário HTML tradicional pode enviar dados no formato `application/x-www-form-urlencoded`.

Para interpretar esse formato, configure:

```javascript
app.use(express.urlencoded({ extended: true }));
```

Exemplo de formulário:

```html
<form action="/cadastro" method="POST">
    <input
        type="text"
        name="nome"
        placeholder="Seu nome"
        required
    >

    <button type="submit">
        Cadastrar
    </button>
</form>
```

No servidor:

```javascript
app.post("/cadastro", (req, res) => {
    const nome = req.body.nome;

    res.send(`Cadastro recebido para: ${nome}`);
});
```

O atributo `name` identifica o campo enviado pelo formulário.

Sem ele, um campo comum não será incluído na submissão tradicional do formulário.

O middleware `express.urlencoded()` e o middleware `express.json()` tratam formatos diferentes. Utilize aquele que corresponde ao formato enviado pelo cliente.

---

## 13. Criando um middleware personalizado

Um **middleware** é uma função que participa do processamento da requisição e pode executar tarefas antes de a rota enviar a resposta.

Ele pode, por exemplo:

- Registrar acessos.
- Verificar autenticação.
- Validar determinadas informações.
- Medir o tempo de processamento.
- Aplicar controles de acesso.

Exemplo de middleware para registrar requisições:

```javascript
function registrarAcesso(req, res, next) {
    console.log(
        `${req.method} ${req.originalUrl}`
    );

    next();
}

app.use(registrarAcesso);
```

Ao receber uma requisição, o middleware registra o método HTTP e o endereço solicitado.

### O que é `next()`?

O parâmetro `next` é uma função que permite transferir o controle para o próximo middleware ou para o processamento seguinte.

Se um middleware não enviar uma resposta e também não chamar `next()`, a requisição poderá ficar aguardando indefinidamente.

**Atenção:** um middleware pode interromper o processamento enviando uma resposta ou encaminhando um erro. Não chame `next()` indiscriminadamente depois de já ter encerrado a resposta.

---

## 14. Tratando erros no servidor

Erros inesperados podem ocorrer durante o processamento de uma requisição.

Uma rota assíncrona pode utilizar `try/catch`:

```javascript
app.get("/api/exemplo", async (req, res, next) => {
    try {
        // Operação assíncrona
        const resultado = await algumaOperacao();

        res.json(resultado);

    } catch (erro) {
        next(erro);
    }
});
```

`algumaOperacao()` é apenas um nome ilustrativo: substitua-o por uma função real que retorne uma Promise.

O `next(erro)` encaminha o erro para o middleware de tratamento de erros.

### Middleware de erros

Adicione-o depois das rotas:

```javascript
app.use((erro, req, res, next) => {
    console.error(erro);

    if (res.headersSent) {
        return next(erro);
    }

    res.status(500).json({
        erro: "Erro interno do servidor"
    });
});
```

O middleware de erros do Express possui quatro parâmetros: `erro`, `req`, `res` e `next`.

Evite enviar detalhes internos, caminhos privados, credenciais ou rastreamentos de pilha para o cliente em produção. Registre os detalhes necessários no ambiente controlado do servidor.

No Express 5, erros e rejeições de Promises não tratadas em handlers que retornam Promises são encaminhados automaticamente ao tratamento de erros. O padrão com `try/catch` continua útil quando você precisa controlar explicitamente o fluxo.

---

## 15. Permitindo o acesso de outros dispositivos

Por padrão, um servidor pode estar acessível apenas pelo próprio computador, dependendo de como foi iniciado.

Para aceitar conexões de outros dispositivos da rede local, você pode especificar o endereço de escuta:

```javascript
app.listen(3000, "0.0.0.0", () => {
    console.log("Servidor iniciado");
});
```

O endereço `0.0.0.0` faz o servidor escutar nas interfaces IPv4 disponíveis, respeitando as configurações de rede e firewall.

Em outro dispositivo conectado à mesma rede, acesse o endereço IPv4 do computador servidor, por exemplo:

```text
http://192.168.1.10:3000/
```

O endereço acima é apenas um exemplo. Utilize o IPv4 real do computador em que o servidor está executando.

Para funcionar, o firewall, a rede e as configurações do dispositivo precisam permitir a conexão.

**Importante:** disponibilizar um servidor na rede local não significa que ele estará acessível pela internet. Também não é recomendável expor um servidor de desenvolvimento sem configurar controles de segurança adequados.

---

## 16. Aplicações práticas de um servidor Express

A seguir estão algumas funcionalidades que podem ser construídas com os conceitos apresentados.

### 16.1. API para uma aplicação web

O frontend envia requisições ao servidor e recebe respostas JSON.

Exemplos:

- Carregar dados de um perfil.
- Buscar informações.
- Enviar configurações.
- Atualizar preferências do usuário.

### 16.2. Sistema de cadastro

O servidor recebe os dados de um formulário, valida as informações e salva os registros em um banco de dados.

Em um sistema real, é necessário considerar validação, proteção contra abusos, armazenamento seguro de senhas e autenticação.

### 16.3. Sistema de login

O backend verifica as credenciais e estabelece uma sessão ou emite um mecanismo de autenticação apropriado.

Não armazene senhas em texto puro. Utilize técnicas adequadas de hash de senhas e configure corretamente a proteção das sessões ou dos tokens.

### 16.4. Sistema de pesquisa

O frontend envia um termo de pesquisa:

```text
/api/pesquisar?termo=JavaScript
```

O servidor utiliza esse termo para consultar uma coleção ou um banco de dados e retorna os resultados.

### 16.5. Armazenamento de textos

Uma aplicação de escrita pode enviar o conteúdo de um texto para o servidor.

Exemplo de corpo JSON:

```json
{
    "titulo": "Minha história",
    "conteudo": "Era uma vez..."
}
```

O backend pode validar os campos, salvar o texto e devolvê-lo posteriormente.

### 16.6. Upload de arquivos

O servidor pode receber imagens, documentos e outros arquivos por meio de requisições multipart.

Para isso, normalmente é necessário utilizar um middleware ou uma biblioteca específica de upload. Também é importante limitar o tamanho dos arquivos, validar o tipo de conteúdo e impedir acessos indevidos.

### 16.7. Comunicação com banco de dados

O Express pode executar consultas por meio de bibliotecas ou drivers de banco de dados.

Por exemplo, com SQLite, a aplicação pode armazenar usuários, textos e configurações de forma persistente.

O Express recebe a requisição e coordena o processamento; o banco de dados é responsável pelo armazenamento e pela consulta dos registros.

---

## 17. Boas práticas

Ao desenvolver servidores Express, adote algumas práticas desde o início.

1. **Separe as responsabilidades.** Evite colocar todas as rotas e regras de negócio em um único arquivo quando o projeto crescer.
2. **Valide as entradas.** Nunca suponha que os dados enviados pelo cliente estão corretos.
3. **Utilize códigos HTTP apropriados.** Eles tornam o comportamento da API mais previsível.
4. **Trate erros.** Não deixe falhas inesperadas produzirem respostas confusas.
5. **Não exponha segredos.** Chaves de API, senhas e outras credenciais não devem ser publicadas no código ou no frontend.
6. **Utilize banco de dados quando necessário.** Variáveis em memória não substituem armazenamento persistente.
7. **Mantenha as dependências atualizadas.** Instale bibliotecas de fontes confiáveis e acompanhe vulnerabilidades.
8. **Configure a segurança.** Em aplicações reais, considere HTTPS, controle de acesso, limitação de requisições e outras medidas apropriadas.
9. **Use variáveis de ambiente.** Portas e configurações específicas do ambiente podem ser configuradas sem serem fixadas diretamente no código.
10. **Teste as rotas.** Verifique tanto as respostas bem-sucedidas quanto os casos inválidos e os erros.

---

## 18. Resumo dos principais recursos

| Recurso | Função |
|---|---|
| `express()` | Cria a aplicação Express. |
| `app.listen()` | Inicia o servidor HTTP. |
| `app.get()` | Define uma rota GET. |
| `app.post()` | Define uma rota POST. |
| `app.put()` | Define uma rota PUT. |
| `app.patch()` | Define uma rota PATCH. |
| `app.delete()` | Define uma rota DELETE. |
| `app.use()` | Registra middlewares. |
| `express.json()` | Interpreta corpos de requisição JSON. |
| `express.urlencoded()` | Interpreta formulários URL-encoded. |
| `express.static()` | Disponibiliza arquivos estáticos. |
| `req.params` | Acessa parâmetros de rota. |
| `req.query` | Acessa parâmetros de consulta. |
| `req.body` | Acessa o corpo interpretado da requisição. |
| `res.send()` | Envia uma resposta. |
| `res.json()` | Envia uma resposta JSON. |
| `res.status()` | Define o código de status HTTP. |
| `res.sendFile()` | Envia um arquivo específico. |
| `next()` | Transfere o controle ao próximo middleware ou encaminha um erro. |

---

## 19. Exercícios para praticar

Tente implementar estas aplicações sem copiar uma solução pronta.

### Nível 1 — Fundamentos

- [ ] Crie um servidor que responda `Olá, mundo!` na rota `/`.
- [ ] Crie uma rota `/sobre` que devolva uma descrição do projeto.
- [ ] Crie uma rota `/api/status` que retorne um objeto JSON com o estado do servidor.
- [ ] Crie uma rota que receba um nome pela query string e responda com uma mensagem personalizada.

### Nível 2 — Comunicação

- [ ] Crie uma rota POST que receba um objeto JSON com nome e idade.
- [ ] Valide se os campos enviados estão preenchidos e possuem tipos apropriados.
- [ ] Faça o frontend enviar os dados por meio de `fetch()`.
- [ ] Exiba no frontend a resposta retornada pelo servidor.
- [ ] Trate respostas com códigos de erro HTTP.

### Nível 3 — Aplicação completa

- [ ] Crie uma API de tarefas com listagem, cadastro, consulta individual e exclusão.
- [ ] Implemente uma rota de atualização.
- [ ] Organize os dados em uma estrutura apropriada.
- [ ] Separe as rotas em outro arquivo.
- [ ] Adicione persistência com SQLite.
- [ ] Crie uma interface HTML para utilizar a API.

---

## 20. Documentação oficial

Consulte a documentação para estudar os recursos em profundidade e verificar os detalhes específicos da versão utilizada.

- Express.js — documentação oficial: https://expressjs.com/
- Guia de roteamento: https://expressjs.com/en/guide/routing.html
- Guia de uso de middleware: https://expressjs.com/en/guide/using-middleware.html
- Guia de tratamento de erros: https://expressjs.com/en/guide/error-handling.html
- API do Express: https://expressjs.com/en/5x/api.html
- Node.js — documentação oficial: https://nodejs.org/docs/latest/api/
- MDN — métodos de requisição HTTP: https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Methods

**Recomendação de estudo:** domine primeiro rotas, requisições, respostas, `req.body`, JSON e `fetch()`. Em seguida, avance para persistência com banco de dados, organização de arquivos e autenticação. Esses fundamentos permitem construir uma grande variedade de aplicações web sem precisar aprender todas as ferramentas de backend simultaneamente.