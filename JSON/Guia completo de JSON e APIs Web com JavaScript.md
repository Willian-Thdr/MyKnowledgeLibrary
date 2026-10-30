# JSON e APIs na Web — Guia de Estudos

## 1. O que é JSON?

**JSON** (*JavaScript Object Notation*) é um formato textual usado para representar e transmitir informações entre sistemas.

É muito utilizado na comunicação entre frontend, backend, APIs e bancos de dados.

### Exemplo de JSON

```json
{
    "nome": "Willian",
    "idade": 17,
    "ativo": true,
    "interesses": ["JavaScript", "Python", "CSS"],
    "endereco": {
        "cidade": "São Paulo",
        "pais": "Brasil"
    }
}
```

### Tipos de dados aceitos

| Tipo | Exemplo |
|---|---|
| String | `"texto"` |
| Number | `25`, `3.14` |
| Boolean | `true`, `false` |
| Array | `[1, 2, 3]` |
| Object | `{"nome": "Ana"}` |
| Null | `null` |

**Atenção:** JSON não aceita funções, comentários, `undefined` ou vírgulas extras no final de objetos e arrays.

Além disso, as chaves e as strings precisam utilizar aspas duplas.

---

## 2. JSON e objetos JavaScript

Embora sejam parecidos, JSON e objetos JavaScript não são a mesma coisa.

### Objeto JavaScript

```javascript
const usuario = {
    nome: "Ana",
    idade: 20
};
```

### Texto JSON

```javascript
const usuarioJSON = '{"nome":"Ana","idade":20}';
```

O primeiro é um objeto que o JavaScript pode manipular diretamente. O segundo é uma string que segue a sintaxe JSON.

Para converter entre eles, usamos dois métodos principais.

### `JSON.stringify()`

Converte um valor JavaScript em uma string JSON.

```javascript
const usuario = {
    nome: "Ana",
    idade: 20
};

const texto = JSON.stringify(usuario);

console.log(texto);
```

Resultado:

```json
{"nome":"Ana","idade":20}
```

É útil para transmitir dados e armazenar informações em formatos textuais.

### `JSON.parse()`

Converte uma string JSON válida em um valor JavaScript.

```javascript
const texto = '{"nome":"Ana","idade":20}';

const usuario = JSON.parse(texto);

console.log(usuario.nome);
console.log(usuario.idade);
```

Resultado:

```text
Ana
20
```

Se a string tiver JSON inválido, o método lançará um erro. Quando os dados vêm de uma fonte externa, é importante tratar essa possibilidade.

---

## 3. O que é uma API?

**API** (*Application Programming Interface*) é uma interface que permite que sistemas ou componentes de software se comuniquem.

Na Web, uma API frequentemente permite que um frontend envie solicitações a um backend e receba informações como resposta.

Exemplos de aplicações:

- Enviar os dados de um formulário.
- Consultar informações de um usuário.
- Realizar uma pesquisa em um servidor.
- Atualizar as configurações de uma conta.
- Solicitar dados de um serviço externo.
- Enviar informações para processamento.
- Receber notificações ou resultados de operações.

### Como funciona a comunicação?

```text
Frontend
   |
   | Requisição HTTP
   | Dados em JSON
   v
Backend / API
   |
   | Processa a solicitação
   | Valida os dados
   | Consulta ou modifica informações
   v
Banco de dados ou serviço
   |
   | Resultado
   v
Backend / API
   |
   | Resposta HTTP
   | JSON
   v
Frontend
```

Nem toda API utiliza JSON, mas esse formato é bastante comum em APIs Web.

---

## 4. O que é HTTP?

**HTTP** (*Hypertext Transfer Protocol*) é um protocolo utilizado na comunicação entre clientes e servidores na Web.

Quando um navegador solicita uma página ou quando o JavaScript envia dados para um servidor, a comunicação pode ocorrer por HTTP ou HTTPS.

O HTTPS adiciona uma camada de segurança por meio de criptografia TLS.

### Métodos HTTP mais utilizados

| Método | Finalidade comum |
|---|---|
| `GET` | Consultar informações |
| `POST` | Enviar dados ou solicitar a criação de um recurso |
| `PUT` | Substituir um recurso |
| `PATCH` | Modificar parte de um recurso |
| `DELETE` | Excluir um recurso |

O comportamento exato depende da API. Por exemplo, `POST` não serve exclusivamente para criar recursos: também pode iniciar um processamento ou executar uma operação.

### Códigos de status HTTP

| Código | Significado |
|---|---|
| `200 OK` | Solicitação concluída |
| `201 Created` | Recurso criado |
| `204 No Content` | Solicitação concluída sem conteúdo na resposta |
| `400 Bad Request` | Solicitação inválida |
| `401 Unauthorized` | Autenticação necessária ou inválida |
| `403 Forbidden` | Acesso proibido |
| `404 Not Found` | Recurso não encontrado |
| `500 Internal Server Error` | Erro interno no servidor |

Esses códigos ajudam o cliente a entender o resultado da solicitação.

---

## 5. Como enviar informações do frontend para o backend

No JavaScript do navegador, podemos utilizar `fetch()` para fazer requisições HTTP.

### Estrutura básica

```javascript
fetch("https://exemplo.com/api/dados", {
    method: "POST",
    headers: {
        "Content-Type": "application/json"
    },
    body: JSON.stringify({
        nome: "Ana",
        idade: 20
    })
});
```

Nesse exemplo:

- `fetch()` inicia a requisição.
- A URL indica o endereço do serviço.
- `method` define o método HTTP.
- `headers` informa o formato dos dados enviados.
- `JSON.stringify()` converte o objeto JavaScript em texto JSON.
- `body` contém o corpo da requisição.

A URL é ilustrativa. Para executar o exemplo, é necessário que exista um servidor configurado para receber a solicitação.

### Enviando informações de um formulário

HTML:

```html
<form id="formulario">
    <input id="nome" type="text" placeholder="Nome" required>
    <input id="email" type="email" placeholder="E-mail" required>

    <button type="submit">Enviar</button>
</form>
```

JavaScript:

```javascript
const formulario = document.querySelector("#formulario");

formulario.addEventListener("submit", async (evento) => {
    evento.preventDefault();

    const nome = document.querySelector("#nome").value;
    const email = document.querySelector("#email").value;

    const dados = {
        nome: nome,
        email: email
    };

    try {
        const resposta = await fetch("/api/usuarios", {
            method: "POST",
            headers: {
                "Content-Type": "application/json"
            },
            body: JSON.stringify(dados)
        });

        if (!resposta.ok) {
            throw new Error(`Erro HTTP: ${resposta.status}`);
        }

        console.log("Informações enviadas com sucesso.");
    } catch (erro) {
        console.error("Não foi possível enviar os dados:", erro);
    }
});
```

O exemplo pressupõe que o servidor tenha uma rota `POST /api/usuarios` e que ela aceite esses campos.

O método `preventDefault()` impede que o formulário execute seu comportamento padrão, que normalmente enviaria os dados e recarregaria a página.

**Importante:** enviar os dados não significa que eles foram salvos. O backend precisa recebê-los, validá-los e executar a operação necessária.

---

## 6. Como receber informações de uma API

Para consultar informações, normalmente usamos `GET`.

```javascript
async function buscarDados() {
    try {
        const resposta = await fetch("/api/dados");

        if (!resposta.ok) {
            throw new Error(`Erro HTTP: ${resposta.status}`);
        }

        const dados = await resposta.json();

        console.log(dados);
    } catch (erro) {
        console.error("Erro ao consultar os dados:", erro);
    }
}

buscarDados();
```

### Entendendo o processo

1. `fetch()` faz a requisição.
2. O servidor responde com um status HTTP e, possivelmente, um corpo.
3. `resposta.ok` verifica se o status está na faixa de sucesso, de 200 a 299.
4. `resposta.json()` lê o corpo e tenta interpretar seu conteúdo como JSON.
5. O resultado pode ser utilizado pelo JavaScript.

`resposta.json()` é assíncrono e retorna uma Promise. Por isso, usamos `await` dentro de uma função `async`.

O endereço `/api/dados` também é ilustrativo e precisa corresponder a uma rota real.

---

## 7. Como enviar informações usando parâmetros na URL

Nem toda informação precisa ser enviada no corpo de uma requisição.

Em consultas `GET`, podemos utilizar parâmetros de URL.

Exemplo:

```javascript
const parametros = new URLSearchParams({
    nome: "Ana",
    idade: "20"
});

fetch(`/api/usuarios?${parametros}`);
```

A URL resultante será semelhante a:

```text
/api/usuarios?nome=Ana&idade=20
```

O backend poderá interpretar esses parâmetros e realizar a consulta.

### Quando usar parâmetros?

- Pesquisar por um termo.
- Filtrar resultados.
- Definir uma página de resultados.
- Ordenar uma listagem.
- Informar critérios de consulta.

Não utilize parâmetros de URL para senhas, tokens secretos ou outras informações confidenciais, pois URLs podem aparecer em históricos, logs e registros de requisições.

---

## 8. Como criar uma API com Node.js e Express

O **Node.js** permite executar JavaScript fora do navegador. O **Express** é uma biblioteca que facilita a criação de servidores e rotas HTTP.

### Instalação

É necessário ter o Node.js instalado.

No terminal, crie uma pasta para o projeto e execute:

```bash
npm init -y
npm install express
```

Crie um arquivo chamado `server.js`.

### Criando o servidor

```javascript
const express = require("express");

const app = express();
const PORT = 3000;

app.use(express.json());

app.get("/api/dados", (req, res) => {
    res.json({
        mensagem: "Dados enviados pelo servidor",
        sucesso: true
    });
});

app.post("/api/dados", (req, res) => {
    const dadosRecebidos = req.body;

    console.log(dadosRecebidos);

    res.status(200).json({
        mensagem: "Dados recebidos",
        dados: dadosRecebidos
    });
});

app.listen(PORT, () => {
    console.log(`Servidor iniciado na porta ${PORT}`);
});
```

### Entendendo a estrutura

- `require("express")`: importa o Express.
- `express()`: cria a aplicação.
- `app.use(express.json())`: permite interpretar corpos de requisições JSON.
- `app.get()`: registra uma rota para requisições `GET`.
- `app.post()`: registra uma rota para requisições `POST`.
- `req`: representa a requisição recebida.
- `req.body`: contém os dados enviados no corpo, após a interpretação pelo middleware.
- `res`: permite construir e enviar a resposta.
- `res.json()`: envia uma resposta JSON.
- `app.listen()`: inicia o servidor.

### Executando

No terminal:

```bash
node server.js
```

Depois, abra:

```text
http://localhost:3000/api/dados
```

O navegador deverá exibir a resposta da rota `GET`.

A rota `POST` pode ser testada com `fetch()` a partir de uma página servida adequadamente, ou com uma ferramenta de testes HTTP.

**Atenção:** esse exemplo apenas devolve os dados recebidos. Ele não autentica usuários nem salva informações permanentemente.

---

## 9. O que são rotas e endpoints?

Uma **rota** define como o servidor responde a determinado método HTTP e caminho.

Um **endpoint** é um ponto de acesso da API, geralmente identificado pela combinação de método e caminho.

Exemplo:

| Método | Caminho | Finalidade |
|---|---|---|
| `GET` | `/api/usuarios` | Consultar usuários |
| `GET` | `/api/usuarios/15` | Consultar um usuário específico |
| `POST` | `/api/usuarios` | Enviar dados para criar um usuário |
| `PATCH` | `/api/usuarios/15` | Atualizar parte dos dados |
| `DELETE` | `/api/usuarios/15` | Solicitar a exclusão |

Os caminhos são exemplos de convenções. Cada API define seus próprios endpoints e regras.

---

## 10. Enviando e recebendo dados: ciclo completo

Considere o seguinte exemplo genérico.

### Frontend

```javascript
async function enviarDados() {
    const dados = {
        mensagem: "Olá, servidor!",
        numero: 42
    };

    const resposta = await fetch("/api/mensagem", {
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

### Backend

```javascript
app.post("/api/mensagem", (req, res) => {
    const dados = req.body;

    res.json({
        recebido: true,
        mensagem: dados.mensagem,
        numero: dados.numero
    });
});
```

O fluxo é:

1. O frontend monta um objeto.
2. O objeto é convertido em texto JSON.
3. O texto é enviado por HTTP.
4. O backend interpreta o corpo da requisição.
5. O backend processa os dados.
6. O servidor envia uma resposta JSON.
7. O frontend interpreta a resposta e utiliza as informações.

Esse padrão é utilizado em muitas funcionalidades Web, como formulários, pesquisas, configurações e operações de conta.

---

## 11. Enviando informações para serviços externos

Uma API não precisa pertencer ao mesmo projeto do frontend. O JavaScript também pode consultar serviços externos.

```javascript
async function consultarServico() {
    const resposta = await fetch("https://api.exemplo.com/dados");

    if (!resposta.ok) {
        throw new Error(`Erro HTTP: ${resposta.status}`);
    }

    const dados = await resposta.json();

    console.log(dados);
}
```

Para funcionar, o endereço precisa existir e aceitar a requisição.

Também podem ser necessários:

- Uma chave de API.
- Um token de autenticação.
- Cabeçalhos específicos.
- Parâmetros de consulta.
- Permissão de acesso à origem do navegador.

### O que é CORS?

**CORS** (*Cross-Origin Resource Sharing*) é um mecanismo de segurança dos navegadores que controla quais origens podem acessar determinados recursos de outro servidor.

Se o frontend estiver em um domínio ou porta diferente do backend, pode ser necessário configurar o CORS no servidor.

Não é correto tentar resolver isso desativando as proteções do navegador. O servidor deve permitir somente as origens e operações necessárias.

---

## 12. JSON e armazenamento local

JSON também pode ser utilizado para armazenar informações no navegador, por exemplo, com `localStorage`.

### Salvando dados

```javascript
const configuracoes = {
    tema: "escuro",
    idioma: "pt-BR"
};

localStorage.setItem(
    "configuracoes",
    JSON.stringify(configuracoes)
);
```

### Lendo dados

```javascript
const texto = localStorage.getItem("configuracoes");

if (texto !== null) {
    try {
        const configuracoes = JSON.parse(texto);

        console.log(configuracoes.tema);
    } catch (erro) {
        console.error("As configurações armazenadas são inválidas.");
    }
}
```

O `localStorage` armazena strings. Por isso, utilizamos `JSON.stringify()` para salvar objetos e `JSON.parse()` para recuperá-los.

### Limitações do `localStorage`

- Os dados ficam no navegador do usuário.
- Não são automaticamente compartilhados com outros dispositivos.
- O usuário pode apagá-los ou modificá-los.
- Não devem ser tratados como informações confiáveis.
- Não são adequados para guardar senhas ou segredos.

Para armazenar dados compartilhados entre usuários e dispositivos, normalmente precisamos de um backend e de um sistema de persistência, como um banco de dados.

---

## 13. JSON e bancos de dados

JSON é um formato de representação e transmissão de dados. Não é, por si só, um banco de dados.

Um sistema pode receber informações em JSON, validá-las e armazená-las em um banco de dados relacional, como SQLite ou PostgreSQL, ou em um banco orientado a documentos.

O fluxo pode ser:

```text
Frontend
   ↓ JSON
API / Backend
   ↓ Validação e processamento
Banco de dados
   ↓ Resultado
API / Backend
   ↓ JSON
Frontend
```

É o backend que controla como os dados serão consultados, inseridos, atualizados e excluídos.

Uma resposta JSON também pode conter dados que vieram de um banco sem que o frontend precise conhecer a estrutura interna desse banco.

---

## 14. Segurança ao trabalhar com APIs

Enviar e receber dados exige cuidados.

### Validação

Não confie automaticamente nas informações enviadas pelo cliente.

```javascript
app.post("/api/dados", (req, res) => {
    const { nome, idade } = req.body;

    if (typeof nome !== "string" || nome.trim() === "") {
        return res.status(400).json({
            erro: "O nome é obrigatório."
        });
    }

    if (!Number.isInteger(idade) || idade < 0) {
        return res.status(400).json({
            erro: "A idade deve ser um número inteiro válido."
        });
    }

    res.json({
        mensagem: "Dados válidos."
    });
});
```

A validação do frontend melhora a experiência do usuário, mas a validação do backend é indispensável.

### Autenticação e autorização

- **Autenticação:** verifica quem está realizando a solicitação.
- **Autorização:** verifica quais ações essa pessoa pode executar.

Estar autenticado não significa ter permissão para acessar todos os dados.

### Outras práticas importantes

- Utilize HTTPS em produção.
- Não exponha senhas, chaves privadas ou segredos no frontend.
- Não confie em informações como `idUsuario` enviadas pelo cliente para decidir permissões.
- Limite o acesso às rotas conforme as permissões necessárias.
- Trate erros sem revelar detalhes internos do servidor.
- Use consultas parametrizadas ao trabalhar com SQL.
- Defina limites de tamanho e frequência das requisições.
- Evite retornar dados pessoais desnecessários.

---

## 15. Organização de um projeto com API

Um projeto simples pode começar com poucos arquivos:

```text
projeto/
│
├── public/
│   ├── index.html
│   ├── style.css
│   └── script.js
│
├── server.js
├── package.json
└── package-lock.json
```

### Responsabilidades

- `index.html`: estrutura da página.
- `style.css`: aparência visual.
- `script.js`: comportamento no navegador e requisições à API.
- `server.js`: servidor e rotas.
- `package.json`: informações do projeto e dependências.
- `package-lock.json`: registro das versões resolvidas das dependências.

À medida que o projeto cresce, é possível separar as rotas, os serviços, a validação e o acesso ao banco de dados em módulos diferentes.

---

## 16. Erros comuns

| Erro | Causa possível |
|---|---|
| `Unexpected token` no `JSON.parse()` | String que não contém JSON válido |
| `req.body` está indefinido | Middleware ausente ou corpo não enviado corretamente |
| Erro `404` | Caminho ou endpoint incorreto |
| Erro `500` | Falha no servidor |
| Erro de CORS | Configuração de origem do servidor |
| `fetch()` falha | Problema de rede, CORS ou outra falha de comunicação |
| `response.json()` falha | Resposta vazia ou conteúdo que não é JSON válido |
| Os dados não são salvos | O backend não implementa persistência |
| Os dados chegam como string | Conversão ou tipo enviado diferente do esperado |

Um status HTTP de erro, como `404` ou `500`, não faz necessariamente o `fetch()` rejeitar a Promise. Por isso, normalmente devemos verificar `resposta.ok`.

---

## 17. Exercícios práticos

### Nível 1 — JSON

1. Crie um objeto JavaScript com nome, idade, cidade e uma lista de interesses.
2. Converta o objeto em JSON com `JSON.stringify()`.
3. Converta a string de volta com `JSON.parse()`.
4. Acesse individualmente as propriedades do objeto recuperado.

### Nível 2 — Requisições

1. Crie uma página com um formulário de nome e mensagem.
2. Capture os valores usando JavaScript.
3. Monte um objeto com esses valores.
4. Converta o objeto para JSON.
5. Envie-o com `fetch()` e `POST`.
6. Trate possíveis erros da requisição.

### Nível 3 — Backend

1. Instale Node.js e Express.
2. Crie uma rota `GET` que retorne um JSON.
3. Crie uma rota `POST` que receba um JSON.
4. Valide os campos recebidos.
5. Retorne uma resposta com um status HTTP apropriado.
6. Conecte a página HTML ao servidor.

### Nível 4 — Persistência

1. Instale e configure um banco SQLite.
2. Crie uma tabela para armazenar informações.
3. Faça a API validar os dados recebidos.
4. Implemente a inserção no banco.
5. Implemente uma rota para consultar os dados.
6. Trate erros e valide permissões de acesso.

---

## 18. Documentação oficial

- JSON: https://www.json.org/json-en.html
- `JSON.stringify()`: https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify
- `JSON.parse()`: https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/JSON/parse
- `fetch()`: https://developer.mozilla.org/docs/Web/API/Fetch_API/Using_Fetch
- HTTP: https://developer.mozilla.org/docs/Web/HTTP
- CORS: https://developer.mozilla.org/docs/Web/HTTP/CORS
- Node.js: https://nodejs.org/docs/latest/api/
- Express: https://expressjs.com/
- SQLite: https://www.sqlite.org/docs.html

---

## 19. Ordem recomendada de estudo

1. Objetos e arrays JavaScript.
2. JSON: `stringify()` e `parse()`.
3. Promises, `async` e `await`.
4. HTTP, métodos e códigos de status.
5. `fetch()` para enviar e receber dados.
6. Node.js e Express.
7. Rotas, endpoints e validação.
8. Banco de dados e SQL.
9. Autenticação, autorização e segurança.

**Conceito central:** JSON define um formato para representar dados; HTTP transporta requisições e respostas; uma API define como um sistema pode ser acessado; e o backend executa as operações necessárias para processar as informações.