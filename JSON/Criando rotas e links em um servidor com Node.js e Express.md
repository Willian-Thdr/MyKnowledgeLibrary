# Criando rotas e links em um servidor com Node.js e Express

## 1. O que é uma rota?

Uma **rota** define como o servidor responde quando recebe uma requisição para determinado caminho e método HTTP.

Por exemplo:

```javascript
app.get("/myarchive", (req, res) => {
    res.send("Minha página");
});
```

Nesse caso:

- `app.get()` registra uma rota para requisições GET.
- `"/myarchive"` é o caminho da rota.
- `req` representa a requisição recebida.
- `res` representa a resposta que o servidor enviará.
- `res.send()` envia o conteúdo da resposta.

Se o servidor estiver funcionando em `http://localhost:3000`, o endereço completo será:

```text
http://localhost:3000/myarchive
```

### Estrutura geral

```javascript
app.METODO("/caminho", (req, res) => {
    // Processamento da requisição

    // Envio da resposta
});
```

O método HTTP, o caminho e a função de resposta determinam como o servidor tratará a solicitação.

---

## 2. Como criar um link para carregar uma janela HTML

Se você deseja abrir uma página HTML através do servidor, pode utilizar `res.sendFile()`.

### Exemplo

```javascript
const path = require("path");

app.get("/myarchive", (req, res) => {
    res.sendFile(
        path.join(__dirname, "..", "view", "profile_window", "profile_window.html")
    );
});
```

Nesse exemplo, o servidor responde a uma requisição GET enviando o arquivo HTML indicado.

### Entendendo `path.join()`

```javascript
path.join(__dirname, "..", "view", "profile_window", "profile_window.html");
```

- `__dirname`: diretório onde está o arquivo JavaScript atual.
- `".."`: sobe um nível na estrutura de diretórios.
- `"view"`: entra na pasta `view`.
- `"profile_window"`: entra na pasta `profile_window`.
- `"profile_window.html"`: identifica o arquivo que será enviado.

O caminho resultante depende da localização real do arquivo JavaScript.

### Acessando a página

Se o servidor estiver na porta `3000`:

```text
http://localhost:3000/myarchive
```

O navegador receberá o HTML e poderá renderizá-lo.

**Importante:** `res.sendFile()` envia o arquivo HTML. Os arquivos CSS, JavaScript, imagens e fontes utilizados pela página também precisam estar acessíveis por seus próprios caminhos.

### Abrindo em uma nova janela pelo JavaScript

No frontend:

```javascript
function abrirJanela() {
    window.open(
        "/myarchive",
        "MinhaJanela",
        "width=600,height=700"
    );
}
```

A URL `"/myarchive"` aponta para uma rota do mesmo servidor e da mesma origem da página atual.

O navegador pode bloquear a abertura se ela não ocorrer em resposta a uma ação do usuário, como um clique.

---

## 3. Como criar uma rota que retorna JSON

Se você deseja enviar informações para o frontend, utilize `res.json()`.

### Exemplo

```javascript
app.get("/api/userdata", (req, res) => {
    res.json({
        nome: "Ana",
        idade: 20,
        status: "active"
    });
});
```

Acessando:

```text
http://localhost:3000/api/userdata
```

O servidor responderá com:

```json
{
    "nome": "Ana",
    "idade": 20,
    "status": "active"
}
```

O método `res.json()` converte o valor JavaScript em JSON, define o tipo de conteúdo apropriado e envia a resposta.

### Recebendo o JSON no frontend

```javascript
async function buscarDados() {
    const resposta = await fetch("/api/userdata");

    if (!resposta.ok) {
        throw new Error(`Erro HTTP: ${resposta.status}`);
    }

    const dados = await resposta.json();

    console.log(dados.nome);
    console.log(dados.status);
}

buscarDados();
```

O `fetch()` faz a requisição, e `resposta.json()` interpreta o corpo recebido como dados JSON.

**Observação:** uma rota que retorna JSON não precisa enviar um arquivo `.json`. O Express gera a resposta a partir do objeto JavaScript.

---

## 4. Como criar uma rota que recebe informações do frontend

Para enviar informações ao servidor, normalmente utilizamos POST.

### Backend

```javascript
app.use(express.json());

app.post("/api/userdata", (req, res) => {
    const dados = req.body;

    console.log(dados);

    res.status(200).json({
        recebido: true
    });
});
```

O middleware `express.json()` deve ser registrado antes das rotas que precisam interpretar corpos JSON.

### Frontend

```javascript
async function enviarDados() {
    const dados = {
        nome: "Ana",
        idade: 20
    };

    const resposta = await fetch("/api/userdata", {
        method: "POST",
        headers: {
            "Content-Type": "application/json"
        },
        body: JSON.stringify(dados)
    });

    if (!resposta.ok) {
        throw new Error(`Erro HTTP: ${resposta.status}`);
    }

    const resultado = await resposta.json();

    console.log(resultado);
}
```

O fluxo é:

1. O frontend cria um objeto JavaScript.
2. `JSON.stringify()` transforma o objeto em texto JSON.
3. `fetch()` envia o texto ao servidor.
4. `express.json()` interpreta o corpo recebido.
5. `req.body` disponibiliza os dados para a rota.
6. `res.json()` envia uma resposta ao cliente.

Uma rota POST não é um link comum para navegação. Ela é um endpoint destinado a receber uma requisição com os dados necessários.

---

## 5. Como disponibilizar arquivos diretamente pelo servidor

O Express também permite disponibilizar arquivos estáticos, como HTML, CSS, JavaScript, imagens e documentos públicos.

### Usando `express.static()`

```javascript
const express = require("express");
const path = require("path");

const app = express();

app.use(express.static(path.join(__dirname, "public")));
```

Considere esta estrutura:

```text
projeto/
├── server.js
└── public/
    ├── index.html
    ├── style.css
    ├── script.js
    └── images/
        └── logo.png
```

O arquivo `index.html` poderá ser acessado em:

```text
http://localhost:3000/index.html
```

O CSS poderá ser acessado em:

```text
http://localhost:3000/style.css
```

E a imagem em:

```text
http://localhost:3000/images/logo.png
```

Se a pasta pública contiver um `index.html`, o Express normalmente também o disponibilizará na raiz:

```text
http://localhost:3000/
```

### Quando utilizar cada método?

| Método | Aplicação |
|---|---|
| `res.sendFile()` | Enviar um arquivo específico por uma rota |
| `res.json()` | Enviar dados estruturados em JSON |
| `res.send()` | Enviar texto ou outro conteúdo de resposta |
| `express.static()` | Disponibilizar uma pasta de arquivos públicos |

Não exponha pastas que contenham arquivos privados, credenciais, configurações internas ou dados que não devam ser acessados diretamente.

---

## 6. Como redirecionar o usuário para outro endereço

Se você deseja que o navegador navegue para outra URL, utilize `res.redirect()`.

### Exemplo

```javascript
app.get("/inicio", (req, res) => {
    res.redirect("/");
});
```

Ao acessar:

```text
http://localhost:3000/inicio
```

O servidor envia uma resposta de redirecionamento, e o navegador navega para a raiz do site.

### Redirecionamento para outro endereço

```javascript
app.get("/documentacao", (req, res) => {
    res.redirect("https://expressjs.com/");
});
```

Esse recurso é útil para direcionar usuários a páginas de login, páginas iniciais, documentação ou outros destinos.

**Atenção:** não crie redirecionamentos que aceitem qualquer URL externa sem validação. Isso pode permitir que terceiros utilizem seu servidor para redirecionar usuários a páginas maliciosas.

---

## 7. Como criar rotas com parâmetros

Você pode criar caminhos que recebem valores variáveis.

### Exemplo

```javascript
app.get("/api/usuarios/:id", (req, res) => {
    const id = req.params.id;

    res.json({
        usuarioId: id
    });
});
```

Acessando:

```text
http://localhost:3000/api/usuarios/15
```

O resultado será:

```json
{
    "usuarioId": "15"
}
```

O valor de `req.params.id` será uma string, mesmo que contenha apenas números.

Se precisar de um número, converta e valide:

```javascript
const id = Number(req.params.id);

if (!Number.isInteger(id) || id <= 0) {
    return res.status(400).json({
        erro: "ID inválido"
    });
}
```

### Parâmetros de consulta

Você também pode utilizar parâmetros após `?`.

```javascript
app.get("/api/pesquisa", (req, res) => {
    const termo = req.query.termo;

    res.json({
        pesquisa: termo
    });
});
```

Exemplo de endereço:

```text
http://localhost:3000/api/pesquisa?termo=javascript
```

Nesse caso, `req.query.termo` terá o valor `"javascript"`.

Os parâmetros de rota identificam partes do caminho. Os parâmetros de consulta geralmente definem filtros, pesquisas ou opções.

---

## 8. Como criar uma rota que não retorna conteúdo

Algumas operações precisam apenas informar se foram concluídas.

Para isso, você pode utilizar `res.sendStatus()`.

```javascript
app.post("/api/confirmacao", (req, res) => {
    res.sendStatus(204);
});
```

O status `204 No Content` indica que a solicitação foi concluída, sem conteúdo na resposta.

Outro exemplo:

```javascript
app.post("/api/operacao", (req, res) => {
    res.sendStatus(200);
});
```

Nesse caso, a resposta informa sucesso com status `200 OK`.

Se precisar devolver dados ao frontend, utilize `res.json()` ou outro método que envie conteúdo.

**Importante:** não tente interpretar uma resposta `204` com `resposta.json()`, porque ela não contém um corpo JSON.

---

## 9. Diferença entre endereço, rota e endpoint

Esses conceitos estão relacionados, mas não são idênticos.

### URL

É o endereço utilizado para localizar um recurso.

```text
http://localhost:3000/api/userdata
```

### Caminho

É a parte da URL que identifica o recurso ou a rota.

```text
/api/userdata
```

### Rota

É a definição no servidor que determina como tratar uma requisição.

```javascript
app.get("/api/userdata", (req, res) => {
    res.json({ ativo: true });
});
```

### Endpoint

É o ponto de acesso da API, geralmente identificado pela combinação de método HTTP e caminho.

Por exemplo:

```text
GET  /api/userdata
POST /api/userdata
```

Embora compartilhem o mesmo caminho, esses dois endpoints podem executar operações diferentes.

---

## 10. Resumo: qual método utilizar?

| Objetivo | Solução |
|---|---|
| Abrir uma página HTML | `res.sendFile()` ou `express.static()` |
| Retornar informações JSON | `res.json()` |
| Receber informações do frontend | `app.post()` com `req.body` |
| Ler um ID no caminho | `req.params` |
| Ler filtros da URL | `req.query` |
| Redirecionar o navegador | `res.redirect()` |
| Enviar uma resposta textual | `res.send()` |
| Responder sem conteúdo | `res.sendStatus(204)` |
| Disponibilizar arquivos de uma pasta | `express.static()` |
| Definir um código HTTP | `res.status(codigo)` |

## 11. Exemplo de servidor com diferentes aplicações

```javascript
const express = require("express");
const path = require("path");

const app = express();
const PORT = 3000;

app.use(express.json());

app.get("/myarchive", (req, res) => {
    res.sendFile(
        path.join(__dirname, "view", "profile_window.html")
    );
});

app.get("/api/userdata", (req, res) => {
    res.json({
        status: "active"
    });
});

app.post("/api/userdata", (req, res) => {
    console.log(req.body);

    res.status(200).json({
        recebido: true
    });
});

app.get("/inicio", (req, res) => {
    res.redirect("/myarchive");
});

app.listen(PORT, () => {
    console.log(`Servidor disponível em http://localhost:${PORT}`);
});
```

Neste servidor, cada rota tem uma finalidade diferente:

- `/myarchive`: envia uma página HTML.
- `GET /api/userdata`: retorna JSON.
- `POST /api/userdata`: recebe JSON e responde ao cliente.
- `/inicio`: redireciona o navegador para `/myarchive`.

O caminho físico do arquivo HTML no exemplo deve ser ajustado à estrutura real do projeto.

---

## 12. Conceito final

Uma rota não é necessariamente um arquivo ou uma página. Ela é uma regra que determina como o servidor responderá a uma requisição.

O resultado pode ser uma página HTML, dados JSON, um arquivo, uma mensagem textual, um redirecionamento ou apenas um código de status.

A escolha depende do que o cliente precisa receber e de qual operação deseja realizar.