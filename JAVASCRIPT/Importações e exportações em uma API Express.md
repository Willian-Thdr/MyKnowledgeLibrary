# Importações e exportações em uma API Express

## 1. CommonJS — `require()` e `module.exports`

Sistema de módulos tradicional do Node.js.

### 1.1. Exportar um único valor

**Arquivo: `utils.js`**

```javascript
function somar(a, b) {
    return a + b;
}

module.exports = somar;
```

**Arquivo: `api.js`**

```javascript
const somar = require("./utils");

console.log(somar(5, 3)); // 8
```

### 1.2. Exportar várias funções ou valores

**Arquivo: `utils.js`**

```javascript
function somar(a, b) {
    return a + b;
}

function subtrair(a, b) {
    return a - b;
}

module.exports = {
    somar,
    subtrair
};
```

**Arquivo: `api.js`**

```javascript
const utils = require("./utils");

console.log(utils.somar(5, 3));       // 8
console.log(utils.subtrair(5, 3));    // 2
```

Também podemos desestruturar os valores durante a importação:

```javascript
const { somar, subtrair } = require("./utils");

console.log(somar(5, 3));
console.log(subtrair(5, 3));
```

### 1.3. Exportar diretamente pelo objeto `exports`

**Arquivo: `utils.js`**

```javascript
exports.somar = (a, b) => a + b;
exports.subtrair = (a, b) => a - b;
```

**Arquivo: `api.js`**

```javascript
const { somar, subtrair } = require("./utils");
```

**Atenção:** `exports` é uma referência inicial a `module.exports`. Você pode adicionar propriedades a `exports`, mas substituir o objeto inteiro com `exports = ...` não funciona como exportação do módulo.

---

## 2. ES Modules — `import` e `export`

Sistema moderno de módulos JavaScript, também compatível com Node.js.

Para utilizar `import` e `export` em arquivos `.js`, adicione ao `package.json`:

```json
{
    "type": "module"
}
```

### 2.1. Exportação nomeada

**Arquivo: `utils.js`**

```javascript
export function somar(a, b) {
    return a + b;
}

export function subtrair(a, b) {
    return a - b;
}
```

**Arquivo: `api.js`**

```javascript
import { somar, subtrair } from "./utils.js";

console.log(somar(5, 3));
console.log(subtrair(5, 3));
```

Observe que, em importações relativas do Node.js com ES Modules, normalmente devemos informar a extensão `.js`.

### 2.2. Exportação padrão — `export default`

**Arquivo: `utils.js`**

```javascript
function somar(a, b) {
    return a + b;
}

export default somar;
```

**Arquivo: `api.js`**

```javascript
import somar from "./utils.js";

console.log(somar(5, 3));
```

Uma exportação padrão permite exportar um valor principal por módulo. O nome utilizado na importação pode ser diferente do nome original.

### 2.3. Exportar vários valores nomeados

**Arquivo: `utils.js`**

```javascript
const nome = "Atlas";
const versao = 1;

export { nome, versao };
```

**Arquivo: `api.js`**

```javascript
import { nome, versao } from "./utils.js";

console.log(nome);
console.log(versao);
```

### 2.4. Importar tudo de um módulo

**Arquivo: `api.js`**

```javascript
import * as utils from "./utils.js";

console.log(utils.somar(5, 3));
console.log(utils.subtrair(5, 3));
```

O identificador `utils` passa a representar um objeto de namespace com as exportações nomeadas do módulo.

### 2.5. Renomear uma importação

```javascript
import { somar as adicionar } from "./utils.js";

console.log(adicionar(5, 3));
```

A função exportada como `somar` é importada localmente com o nome `adicionar`.

---

## 3. Importando e exportando uma aplicação Express

Essa é uma das organizações mais úteis para APIs.

### 3.1. Exportar a aplicação

**Arquivo: `api.js`**

```javascript
import express from "express";

const app = express();

app.use(express.json());

app.get("/", (req, res) => {
    res.json({
        mensagem: "API funcionando"
    });
});

export default app;
```

Esse arquivo configura a aplicação e registra suas rotas, mas não inicia a escuta de uma porta.

### 3.2. Importar a aplicação e iniciar o servidor

**Arquivo: `server.js`**

```javascript
import app from "./api.js";

const port = 3000;

app.listen(port, () => {
    console.log(`Servidor iniciado na porta ${port}`);
});
```

Execute:

```bash
node server.js
```

A separação permite importar a aplicação sem iniciar automaticamente o servidor.

---

## 4. Exportar rotas separadamente

Quando uma API cresce, é útil dividir as rotas em arquivos.

**Arquivo: `routes.js`**

```javascript
import { Router } from "express";

const router = Router();

router.get("/usuarios", (req, res) => {
    res.json({
        usuarios: []
    });
});

router.get("/status", (req, res) => {
    res.json({
        online: true
    });
});

export default router;
```

**Arquivo: `api.js`**

```javascript
import express from "express";
import routes from "./routes.js";

const app = express();

app.use(express.json());
app.use("/api", routes);

export default app;
```

**Arquivo: `server.js`**

```javascript
import app from "./api.js";

app.listen(3000, () => {
    console.log("Servidor iniciado");
});
```

Agora, as rotas estarão disponíveis em:

- `GET /api/usuarios`
- `GET /api/status`

O `app.use("/api", routes)` acrescenta o prefixo `/api` aos caminhos definidos no roteador.

---

## 5. Importar um módulo sem importar valores

Também podemos importar um arquivo apenas para executar seu código de inicialização.

### ES Modules

```javascript
import "./config.js";
```

O arquivo `config.js` será executado como parte do carregamento do módulo, mesmo sem uma importação explícita de seus valores exportados.

### CommonJS

```javascript
require("./config");
```

O módulo será carregado e executado. O Node.js normalmente mantém o resultado em cache para reutilizações posteriores na mesma execução.

Utilize esse padrão com cuidado: módulos que executam operações automaticamente podem gerar efeitos colaterais durante a inicialização.

---

## 6. Comparação rápida

| Objetivo | CommonJS | ES Modules |
|---|---|---|
| Importar um módulo | `require("./arquivo")` | `import ... from "./arquivo.js"` |
| Exportar um valor principal | `module.exports = valor` | `export default valor` |
| Exportar valores nomeados | `module.exports = { a, b }` | `export { a, b }` |
| Importar valores nomeados | `const { a, b } = require("./arquivo")` | `import { a, b } from "./arquivo.js"` |
| Importar todas as exportações | `const modulo = require("./arquivo")` | `import * as modulo from "./arquivo.js"` |

## 7. Observações importantes

- Não misture `require()` com `import` e `module.exports` com `export` indiscriminadamente. Escolha um sistema de módulos para cada arquivo e configure o projeto corretamente.
- Em ES Modules, `export default` e `export` nomeado são formas diferentes de exportação.
- Importar um módulo não significa necessariamente iniciar um servidor. Para isso, a aplicação Express precisa chamar `app.listen()` ou ser iniciada por outro mecanismo apropriado.
- Ao importar módulos relativos com ES Modules no Node.js, inclua a extensão do arquivo, como `./api.js`.
- O nome de uma variável importada não precisa ser igual ao nome do arquivo. O que importa é o caminho do módulo e a forma de exportação utilizada.