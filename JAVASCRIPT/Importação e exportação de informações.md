# Importação e exportação de informações entre arquivos JavaScript

## 1. Introdução

Em JavaScript, podemos compartilhar informações entre diferentes arquivos utilizando mecanismos de importação e exportação, parâmetros de funções, objetos, armazenamento, eventos e outros recursos.

A escolha do método depende de alguns fatores:

- **Tipo de informação:** função, variável, classe, objeto, texto ou outro dado.
- **Ambiente de execução:** navegador ou Node.js.
- **Objetivo:** compartilhar código, transmitir dados, armazenar informações ou comunicar módulos independentes.

É importante compreender que importar uma informação de outro arquivo não significa necessariamente copiar seu conteúdo. Em sistemas de módulos, o JavaScript permite acessar valores exportados por outros módulos.

---

# 2. Exportação e importação com ES Modules

Os ES Modules (ESM) são o sistema moderno e padronizado de módulos do JavaScript.

Eles permitem dividir um programa em vários arquivos, cada um responsável por determinadas funcionalidades.

Existem duas formas principais de exportação:

1. Exportação nomeada (`named export`).
2. Exportação padrão (`default export`).

## 2.1. Exportação nomeada

Utilizamos a exportação nomeada quando desejamos disponibilizar uma ou várias informações de um arquivo.

### Arquivo: `matematica.js`

```javascript
export const pi = 3.14159;

export function somar(a, b) {
    return a + b;
}

export function multiplicar(a, b) {
    return a * b;
}
```

Nesse exemplo, exportamos uma constante e duas funções.

### Arquivo: `main.js`

```javascript
import { pi, somar, multiplicar } from "./matematica.js";

console.log(pi);
console.log(somar(5, 3));
console.log(multiplicar(4, 2));
```

### Sintaxe

```javascript
export const nome = valor;

export function nomeDaFuncao() {
    // Código
}
```

Para importar:

```javascript
import { nome, nomeDaFuncao } from "./arquivo.js";
```

**Observações:**

- Os nomes importados devem corresponder aos nomes exportados.
- As chaves `{}` são utilizadas para selecionar exportações nomeadas.
- O caminho do arquivo normalmente é relativo ao arquivo que realiza a importação.
- No navegador, o caminho de um módulo geralmente deve incluir a extensão `.js`.

### Quando utilizar?

Utilize exportações nomeadas quando um arquivo disponibilizar várias funcionalidades independentes, como funções matemáticas, utilitários, regras de validação ou configurações.

---

## 2.2. Exportação padrão

A exportação padrão permite definir uma exportação principal para um módulo.

Cada arquivo pode possuir apenas uma exportação padrão.

### Arquivo: `usuario.js`

```javascript
const usuario = {
    nome: "Willian",
    idade: 18
};

export default usuario;
```

### Arquivo: `main.js`

```javascript
import usuario from "./usuario.js";

console.log(usuario.nome);
console.log(usuario.idade);
```

O nome utilizado na importação pode ser diferente do nome original.

Por exemplo:

```javascript
import pessoa from "./usuario.js";
```

Isso funciona porque a importação está recebendo a exportação padrão, e não procurando uma exportação chamada `pessoa`.

### Exportando uma função diretamente

```javascript
export default function somar(a, b) {
    return a + b;
}
```

Importação:

```javascript
import somar from "./matematica.js";

console.log(somar(10, 5));
```

### Quando utilizar?

Utilize a exportação padrão quando o arquivo representar principalmente uma funcionalidade, classe, objeto ou componente específico.

---

## 2.3. Exportação nomeada no final do arquivo

Também podemos declarar variáveis e funções normalmente e exportá-las posteriormente.

### Arquivo: `dados.js`

```javascript
const nome = "Atlas";
const versao = 1;

function iniciar() {
    console.log("Sistema iniciado.");
}

export { nome, versao, iniciar };
```

Importação:

```javascript
import { nome, versao, iniciar } from "./dados.js";

console.log(nome);
iniciar();
```

Esse método é útil quando desejamos manter as declarações separadas da lista de exportações.

---

## 2.4. Renomeando exportações

Podemos utilizar um nome externo diferente do nome original.

### Arquivo: `dados.js`

```javascript
const nomeCompleto = "Willian";

export { nomeCompleto as nome };
```

### Arquivo: `main.js`

```javascript
import { nome } from "./dados.js";

console.log(nome);
```

A informação continua sendo `nomeCompleto` dentro do arquivo original, mas pode ser importada como `nome`.

Também podemos renomear durante a importação:

```javascript
import { nomeCompleto as nome } from "./dados.js";
```

Isso é útil para evitar conflitos entre nomes iguais.

---

## 2.5. Importando todas as exportações nomeadas

Podemos importar todas as exportações nomeadas de um módulo como um objeto.

### Arquivo: `matematica.js`

```javascript
export const pi = 3.14;

export function somar(a, b) {
    return a + b;
}
```

### Arquivo: `main.js`

```javascript
import * as matematica from "./matematica.js";

console.log(matematica.pi);
console.log(matematica.somar(2, 3));
```

A expressão `* as matematica` reúne as exportações nomeadas em um objeto de namespace.

A exportação padrão não passa a fazer parte desse objeto automaticamente.

### Quando utilizar?

Esse método é útil quando queremos agrupar as funcionalidades de um módulo sob um mesmo nome.

---

## 2.6. Importando e exportando novamente

Um arquivo pode importar funcionalidades de outro arquivo e disponibilizá-las para terceiros.

Isso é conhecido como *re-exportação*.

### Estrutura

```text
projeto/
├── matematica.js
├── textos.js
├── utilitarios.js
└── main.js
```

### Arquivo: `utilitarios.js`

```javascript
export { somar, multiplicar } from "./matematica.js";
export { formatarTexto } from "./textos.js";
```

### Arquivo: `main.js`

```javascript
import { somar, formatarTexto } from "./utilitarios.js";
```

O arquivo `utilitarios.js` funciona como um ponto central de exportação.

Também podemos exportar todas as exportações nomeadas de outro módulo:

```javascript
export * from "./matematica.js";
```

Essa sintaxe não reexporta a exportação padrão.

Para reexportá-la:

```javascript
export { default as Matematica } from "./matematica.js";
```

---

## 2.7. Importação dinâmica

Normalmente, utilizamos `import` no início do arquivo para declarar as dependências do módulo.

Entretanto, existe também a importação dinâmica, que permite carregar um módulo durante a execução.

### Exemplo

```javascript
async function carregarMatematica() {
    const matematica = await import("./matematica.js");

    console.log(matematica.somar(2, 3));
}

carregarMatematica();
```

O método `import()` retorna uma `Promise`.

Por isso, podemos utilizar `await` dentro de uma função `async` ou encadear um `.then()`.

```javascript
import("./matematica.js")
    .then((modulo) => {
        console.log(modulo.pi);
    })
    .catch((erro) => {
        console.error("Falha ao carregar o módulo:", erro);
    });
```

### Quando utilizar?

- Carregar funcionalidades apenas quando forem necessárias.
- Dividir aplicações grandes em partes.
- Carregar telas ou componentes sob demanda.
- Evitar carregar imediatamente módulos que raramente serão utilizados.

---

# 3. Utilizando módulos no navegador

Para utilizar ES Modules diretamente em um site, precisamos configurar o HTML.

### Arquivo: `index.html`

```html
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <title>Exemplo de módulos</title>
</head>
<body>
    <script type="module" src="./main.js"></script>
</body>
</html>
```

O atributo `type="module"` informa ao navegador que o arquivo JavaScript será executado como um módulo.

### Características dos módulos no navegador

- Suportam `import` e `export`.
- São executados em modo estrito (*strict mode*).
- Suas declarações não são adicionadas automaticamente ao objeto global `window`.
- Suportam importações relativas.
- Podem ser carregados de maneira assíncrona pelo navegador.

**Importante:** ao desenvolver localmente, utilize um servidor HTTP de desenvolvimento. Abrir arquivos diretamente com `file://` pode provocar erros de carregamento de módulos por causa das restrições de segurança do navegador.

Além disso, os caminhos relativos são resolvidos em relação ao arquivo do módulo que realiza a importação, não necessariamente em relação ao HTML.

---

# 4. Exportando e importando informações no Node.js

O Node.js permite utilizar ES Modules, mas também possui um sistema tradicional chamado CommonJS.

Os dois sistemas têm sintaxes diferentes.

## 4.1. ES Modules no Node.js

Uma maneira de habilitar ES Modules em um projeto Node.js é utilizar `"type": "module"` no arquivo `package.json`.

### Arquivo: `package.json`

```json
{
    "type": "module"
}
```

Depois, podemos utilizar normalmente:

```javascript
// matematica.js

export function somar(a, b) {
    return a + b;
}
```

```javascript
// main.js

import { somar } from "./matematica.js";

console.log(somar(5, 7));
```

Também é possível utilizar a extensão `.mjs` para identificar explicitamente arquivos ES Modules.

---

## 4.2. CommonJS: `module.exports`

CommonJS é um sistema de módulos tradicional do Node.js.

Nele, podemos disponibilizar informações por meio de `module.exports`.

### Arquivo: `matematica.js`

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

### Arquivo: `main.js`

```javascript
const matematica = require("./matematica.js");

console.log(matematica.somar(5, 3));
console.log(matematica.subtrair(5, 3));
```

### Exportando apenas uma função

```javascript
function iniciar() {
    console.log("Iniciando...");
}

module.exports = iniciar;
```

Importação:

```javascript
const iniciar = require("./iniciar.js");

iniciar();
```

Nesse caso, `module.exports` recebe diretamente a função.

### Quando utilizar?

CommonJS continua presente em muitos projetos e pacotes Node.js existentes. Em projetos novos, ES Modules costuma ser uma escolha adequada, desde que as dependências e a configuração sejam compatíveis.

**Atenção:** `require()` e `module.exports` não são a sintaxe nativa de módulos do navegador. Não os utilize diretamente em um arquivo JavaScript comum de uma página HTML sem ferramentas ou ambientes específicos que ofereçam esse suporte.

---

# 5. Compartilhando informações por meio de funções

Nem toda comunicação entre arquivos precisa ocorrer por meio de exportações diretas de dados.

Podemos exportar uma função que recebe informações como parâmetros.

### Arquivo: `calculadora.js`

```javascript
export function calcular(a, b, operacao) {
    if (operacao === "somar") {
        return a + b;
    }

    if (operacao === "multiplicar") {
        return a * b;
    }

    return null;
}
```

### Arquivo: `main.js`

```javascript
import { calcular } from "./calculadora.js";

const resultado = calcular(10, 5, "multiplicar");

console.log(resultado);
```

Nesse exemplo, o arquivo principal transmite dados para a função e recebe o resultado retornado.

O fluxo é:

1. O arquivo principal fornece os argumentos.
2. A função recebe os valores.
3. A função realiza o processamento.
4. O `return` devolve o resultado.
5. O arquivo principal utiliza o valor retornado.

Esse método é especialmente útil para separar responsabilidades e evitar que diferentes partes do programa dependam diretamente umas das outras.

---

# 6. Compartilhando objetos e referências

JavaScript permite compartilhar objetos exportados por módulos.

### Arquivo: `configuracao.js`

```javascript
export const configuracao = {
    tema: "escuro",
    idioma: "pt-BR"
};
```

### Arquivo: `main.js`

```javascript
import { configuracao } from "./configuracao.js";

console.log(configuracao.tema);
```

Como os módulos ES utilizam *live bindings*, uma importação nomeada acompanha o valor atual da exportação. Para objetos, ambos os módulos podem acessar o mesmo objeto exportado.

Por exemplo:

```javascript
configuracao.tema = "claro";
```

A alteração será visível para os demais módulos que consultarem aquele mesmo objeto.

Isso não significa que todas as importações podem ser reatribuídas livremente. O identificador importado é somente leitura no módulo que o recebe.

Também é possível exportar classes:

```javascript
// usuario.js

export class Usuario {
    constructor(nome) {
        this.nome = nome;
    }
}
```

```javascript
// main.js

import { Usuario } from "./usuario.js";

const usuario = new Usuario("Willian");

console.log(usuario.nome);
```

**Cuidado:** compartilhar objetos mutáveis pode criar dependências difíceis de rastrear. Quando possível, prefira funções que recebem dados e retornam resultados, ou controle explicitamente quem pode alterar o estado.

---

# 7. Importar e exportar informações usando JSON

JSON é um formato textual utilizado para representar dados estruturados.

É muito comum em configurações, APIs e armazenamento de informações.

## 7.1. Importando JSON no Node.js

Em versões modernas do Node.js, arquivos JSON podem ser importados com sintaxe de módulos, mas o suporte e os requisitos variam conforme a versão e o ambiente.

Uma alternativa explícita é ler o arquivo e converter seu conteúdo com `JSON.parse()`.

### Arquivo: `dados.json`

```json
{
    "nome": "Atlas",
    "versao": 1,
    "ativo": true
}
```

### Arquivo: `main.js`

```javascript
import { readFile } from "node:fs/promises";

const conteudo = await readFile(
    new URL("./dados.json", import.meta.url),
    "utf8"
);

const dados = JSON.parse(conteudo);

console.log(dados.nome);
console.log(dados.versao);
```

Aqui, `readFile()` lê o arquivo como texto, e `JSON.parse()` converte esse texto em um objeto JavaScript.

## 7.2. Convertendo um objeto em JSON

Para transformar um objeto JavaScript em uma string JSON:

```javascript
const usuario = {
    nome: "Willian",
    idade: 18
};

const texto = JSON.stringify(usuario);

console.log(texto);
```

Resultado:

```json
{"nome":"Willian","idade":18}
```

Para melhorar a legibilidade:

```javascript
const texto = JSON.stringify(usuario, null, 4);

console.log(texto);
```

O terceiro argumento, `4`, define a indentação.

**Diferença importante:**

- `JSON.parse()` converte uma string JSON em um valor JavaScript.
- `JSON.stringify()` converte um valor JavaScript compatível em uma string JSON.

Essas funções não leem nem gravam arquivos por conta própria.

---

# 8. Lendo e gravando arquivos no Node.js

Quando precisamos transferir informações entre arquivos físicos, podemos utilizar o módulo `node:fs`.

Esse recurso pertence ao Node.js e não está disponível diretamente em páginas web comuns.

## 8.1. Gravando informações em um arquivo

```javascript
import { writeFile } from "node:fs/promises";

const conteudo = "Minha informação.";

await writeFile("./dados.txt", conteudo, "utf8");
```

Se o arquivo não existir, ele normalmente será criado. Se já existir, seu conteúdo será substituído.

## 8.2. Lendo informações de um arquivo

```javascript
import { readFile } from "node:fs/promises";

const conteudo = await readFile("./dados.txt", "utf8");

console.log(conteudo);
```

## 8.3. Adicionando conteúdo sem apagar o anterior

```javascript
import { appendFile } from "node:fs/promises";

await appendFile("./dados.txt", "\nNova informação.", "utf8");
```

## 8.4. Gravando objetos em JSON

```javascript
import { writeFile } from "node:fs/promises";

const dados = {
    nome: "Atlas",
    ativo: true
};

const conteudo = JSON.stringify(dados, null, 4);

await writeFile("./dados.json", conteudo, "utf8");
```

### Quando utilizar?

- Ler configurações.
- Salvar registros em arquivos.
- Gerar relatórios.
- Armazenar dados em formato JSON.
- Criar sistemas de leitura e escrita no Node.js.

Lembre-se de tratar erros com `try...catch` em operações que possam falhar, como quando o arquivo não existe ou não há permissão para acessá-lo.

---

# 9. Comunicação entre arquivos no navegador por eventos

Quando dois arquivos participam de uma aplicação web, eles podem precisar comunicar acontecimentos, em vez de apenas compartilhar funções.

Uma maneira de fazer isso é utilizar eventos.

### Arquivo: `eventos.js`

```javascript
export const canal = new EventTarget();
```

### Arquivo: `emissor.js`

```javascript
import { canal } from "./eventos.js";

canal.dispatchEvent(
    new CustomEvent("usuario-criado", {
        detail: {
            nome: "Willian"
        }
    })
);
```

### Arquivo: `receptor.js`

```javascript
import { canal } from "./eventos.js";

canal.addEventListener("usuario-criado", (evento) => {
    console.log(evento.detail.nome);
});
```

Para funcionar, os módulos `emissor.js` e `receptor.js` precisam utilizar a mesma instância de `canal`, e o receptor precisa registrar o evento antes de ele ser emitido.

Esse exemplo demonstra o princípio, mas não substitui um sistema completo de gerenciamento de estado.

### Quando utilizar?

- Notificar que um usuário foi criado.
- Informar que uma janela foi aberta.
- Atualizar uma interface após uma ação.
- Desacoplar partes de uma aplicação.

---

# 10. Comunicação entre janelas e abas

Em uma aplicação web, uma página pode precisar comunicar informações a outra janela ou aba.

Para isso, existe a API `postMessage()`.

### Enviando uma mensagem

```javascript
outraJanela.postMessage(
    {
        tipo: "saudacao",
        mensagem: "Olá!"
    },
    "https://exemplo.com"
);
```

`outraJanela` representa uma referência válida a uma janela, como a retornada por `window.open()`.

### Recebendo uma mensagem

```javascript
window.addEventListener("message", (evento) => {
    if (evento.origin !== "https://exemplo.com") {
        return;
    }

    console.log(evento.data);
});
```

O domínio usado no exemplo é ilustrativo. Em aplicações reais, verifique cuidadosamente a origem esperada e valide os dados recebidos.

**Importante:** `postMessage()` é destinado à comunicação entre contextos de execução, como janelas, abas e determinados frames. Não é necessário utilizá-lo para importar uma função de outro arquivo JavaScript.

---

# 11. Armazenamento no navegador

Se a intenção for compartilhar ou preservar informações entre diferentes scripts ou sessões de uma aplicação web, podemos utilizar mecanismos de armazenamento.

## 11.1. localStorage

O `localStorage` armazena strings que permanecem disponíveis entre sessões do navegador, até serem removidas.

```javascript
localStorage.setItem("nome", "Willian");

const nome = localStorage.getItem("nome");

console.log(nome);
```

Para remover:

```javascript
localStorage.removeItem("nome");
```

Para apagar todos os itens da origem atual:

```javascript
localStorage.clear();
```

## 11.2. Armazenando objetos

Como o `localStorage` trabalha com strings, precisamos converter objetos em JSON.

```javascript
const usuario = {
    nome: "Willian",
    ativo: true
};

localStorage.setItem("usuario", JSON.stringify(usuario));
```

Para recuperar:

```javascript
const texto = localStorage.getItem("usuario");

if (texto !== null) {
    const usuario = JSON.parse(texto);

    console.log(usuario.nome);
}
```

## 11.3. sessionStorage

O `sessionStorage` possui uma interface semelhante, mas seu armazenamento está associado à sessão da aba.

```javascript
sessionStorage.setItem("pagina", "login");

const pagina = sessionStorage.getItem("pagina");
```

### Diferenças

| Recurso | Finalidade principal |
|---|---|
| `localStorage` | Preservar dados entre sessões |
| `sessionStorage` | Preservar dados durante a sessão da aba |
| `import` / `export` | Compartilhar código e valores entre módulos |

**Atenção:** esses mecanismos não são bancos de dados completos. Também não devem ser utilizados para guardar senhas ou informações sensíveis sem uma arquitetura de segurança apropriada.

---

# 12. Comunicação entre frontend e backend

Quando uma aplicação possui frontend e backend, o JavaScript pode enviar informações de um ambiente para outro por meio de requisições HTTP.

Isso é diferente de importar arquivos.

### Frontend enviando informações

```javascript
const resposta = await fetch("/api/usuarios", {
    method: "POST",
    headers: {
        "Content-Type": "application/json"
    },
    body: JSON.stringify({
        nome: "Willian"
    })
});

const resultado = await resposta.json();

console.log(resultado);
```

### Backend recebendo informações

Em uma aplicação Node.js com Express, por exemplo:

```javascript
app.use(express.json());

app.post("/api/usuarios", (req, res) => {
    const usuario = req.body;

    res.json({
        mensagem: "Usuário recebido",
        nome: usuario.nome
    });
});
```

O frontend envia uma requisição HTTP; o backend interpreta os dados e responde.

Esse tipo de comunicação é útil quando o navegador precisa consultar ou modificar informações armazenadas em um servidor.

---

# 13. Comparação dos principais métodos

| Método | Compartilha código? | Transmite dados? | Persiste dados? |
|:---|:---:|:---:|---:|
| ES Modules (`import` / `export`) | Sim | Sim, por meio dos valores exportados | Não |
| CommonJS (`require`) | Sim | Sim, por meio dos valores exportados | Não |
| Parâmetros e `return` | Indiretamente, por funções | Sim | Não |
| JSON | Não, por si só | Sim, em formato textual | Não, por si só |
| `fs` no Node.js | Não, por si só | Sim | Sim, em arquivos |
| Eventos | Não, por si só | Sim | Não |
| `postMessage()` | Não, por si só | Sim | Não |
| `localStorage` | Não | Sim, por meio de strings | Sim, no navegador |
| `sessionStorage` | Não | Sim, por meio de strings | Durante a sessão |
| `fetch()` e HTTP | Não | Sim, entre sistemas | Depende do backend |

---

# 14. Boas práticas

1. **Prefira ES Modules para organizar código novo**, quando o ambiente permitir.
2. **Separe responsabilidades:** um arquivo pode conter funções matemáticas, outro pode gerenciar usuários e outro pode controlar a interface.
3. **Evite variáveis globais desnecessárias.** Elas podem causar conflitos e dificultar a manutenção.
4. **Utilize nomes claros.** `buscarUsuario()` é mais informativo do que `buscar()`.
5. **Trate erros.** Arquivos podem não existir, requisições podem falhar e dados podem estar em formato inválido.
6. **Valide dados externos.** Não confie cegamente em informações recebidas de arquivos, formulários ou requisições.
7. **Não confunda importação com persistência.** Exportar um objeto por meio de um módulo não significa salvá-lo no disco.
8. **Evite dependências circulares desnecessárias.** Elas ocorrem quando um módulo depende de outro que, direta ou indiretamente, depende do primeiro.
9. **Utilize JSON para representar dados estruturados**, não como substituto universal para todos os mecanismos de comunicação.
10. **Escolha o método conforme a necessidade.** Compartilhar uma função, armazenar uma configuração e enviar dados a um servidor são problemas diferentes.

---

# 15. Resumo final

Os mecanismos mais importantes para começar são:

- `export` e `import`: compartilhar funcionalidades entre arquivos JavaScript.
- `export default`: disponibilizar a exportação principal de um módulo.
- `import()`: carregar módulos dinamicamente.
- `module.exports` e `require()`: utilizar CommonJS no Node.js.
- Parâmetros e `return`: transmitir informações durante chamadas de funções.
- `JSON.parse()` e `JSON.stringify()`: converter entre strings JSON e valores JavaScript.
- `readFile()`, `writeFile()` e `appendFile()`: ler e gravar arquivos no Node.js.
- `localStorage` e `sessionStorage`: armazenar informações no navegador.
- `postMessage()`: comunicar contextos de execução distintos.
- `fetch()`: trocar informações entre frontend e backend.

A distinção fundamental é esta: **importar e exportar módulos organiza o código; transmitir dados comunica informações; persistir dados conserva informações para uso posterior.** Um projeto pode utilizar os três mecanismos simultaneamente, cada qual cumprindo uma função diferente.
