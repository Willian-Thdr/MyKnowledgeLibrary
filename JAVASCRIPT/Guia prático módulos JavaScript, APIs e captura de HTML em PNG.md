# Guia prático: módulos JavaScript, APIs e captura de HTML em PNG

Este guia reúne conceitos de JavaScript, Node.js, Express, operações
assíncronas e captura de páginas HTML em imagens. Os exemplos são
genéricos e podem ser adaptados a diferentes projetos.

## 1. Exportações em JavaScript: `default` e exportações nomeadas

Quando um arquivo JavaScript precisa disponibilizar funções, objetos ou
valores para outros arquivos, ele pode exportá-los.

### Exportação nomeada

Use uma exportação nomeada quando um módulo disponibiliza uma ou mais
funcionalidades identificadas por seus nomes.

``` js
// math.js
export function sum(a, b) {
    return a + b;
}

export function multiply(a, b) {
    return a * b;
}
```

Para importar essas funções:

``` js
// app.js
import { sum, multiply } from "./math.js";

console.log(sum(2, 3));
console.log(multiply(2, 3));
```

Os nomes entre chaves precisam corresponder aos nomes exportados, salvo
se você usar um alias:

``` js
import { sum as add } from "./math.js";

console.log(add(2, 3));
```

### Exportação padrão (`default`)

Um arquivo pode ter uma única exportação padrão. Ela costuma ser útil
quando existe uma funcionalidade principal que representa aquele módulo.

``` js
// formatter.js
export default function formatName(name) {
    return name.trim().toUpperCase();
}
```

A importação não precisa usar o mesmo nome da função exportada:

``` js
import formatName from "./formatter.js";

console.log(formatName("Ada"));
```

Também é possível exportar um valor como padrão:

``` js
const settings = {
    language: "pt-BR",
    debug: false
};

export default settings;
```

### Quando usar cada uma?

-   **`export default`**: quando o arquivo tem uma exportação principal.
-   **Exportações nomeadas**: quando o arquivo oferece várias
    funcionalidades ou quando é útil deixar explícito o nome de cada
    item importado.
-   Não é obrigatório que um arquivo com uma única função use `default`;
    escolha a forma que deixa a API do módulo mais clara e consistente.

Não confunda a declaração de uma variável com sua exportação. Isto é
inválido:

``` js
export default let data = {};
```

Declare a variável e depois exporte-a:

``` js
const data = {};
export default data;
```

Ou use uma exportação nomeada:

``` js
export const data = {};
```

## 2. ES Modules e CommonJS no Node.js

O Node.js oferece dois sistemas de módulos comuns. É importante não
misturar suas sintaxes inadvertidamente.

### ES Modules (ESM)

Usa `import` e `export`:

``` js
import path from "node:path";

export function getFileName(filePath) {
    return path.basename(filePath);
}
```

Para indicar que arquivos `.js` de um pacote usam ESM, o `package.json`
pode conter:

``` json
{
    "type": "module"
}
```

Também é possível usar a extensão `.mjs` para identificar explicitamente
um arquivo ESM.

### CommonJS (CJS)

Usa `require()` e `module.exports`:

``` js
const path = require("node:path");

function getFileName(filePath) {
    return path.basename(filePath);
}

module.exports = { getFileName };
```

Arquivos CommonJS podem usar a extensão `.cjs`.

### Regra prática

Se o projeto estiver configurado como ESM, mantenha a sintaxe ESM nos
arquivos `.js` abrangidos por essa configuração:

  -----------------------------------------------------------------------
  CommonJS                            ES Modules
  ----------------------------------- -----------------------------------
  `const x = require("x")`            `import x from "x"` ou outra
                                      importação compatível

  `module.exports = value`            `export default value`

  `exports.sum = sum`                 `export { sum }`

  `__dirname`                         `import.meta.dirname` em versões
                                      recentes do Node.js
  -----------------------------------------------------------------------

A conversão depende do formato real de cada módulo. Não basta trocar
`require` por `import`: também é necessário ajustar as exportações e
verificar como os módulos são usados.

### Caminhos de arquivos em ESM

Em CommonJS, `__dirname` representa o diretório do arquivo atual. Em
versões recentes do Node.js, ESM oferece `import.meta.dirname`:

``` js
import path from "node:path";

const assetsDirectory = path.join(import.meta.dirname, "assets");
```

Isso é diferente de `process.cwd()`, que representa o diretório de onde
o processo foi iniciado. Eles podem ser diferentes, por isso escolha a
opção adequada ao objetivo.

## 3. JSON: dados não são a mesma coisa que texto JSON

JSON é um formato textual para representar dados estruturados. Em
JavaScript, um objeto e sua representação em texto não são a mesma
coisa.

``` js
const user = {
    name: "Ada",
    active: true
};

const jsonText = JSON.stringify(user);
console.log(jsonText);
```

`JSON.stringify()` converte um valor JavaScript compatível em texto
JSON.

Para converter texto JSON em um valor JavaScript:

``` js
const jsonText = '{"name":"Ada","active":true}';
const userData = JSON.parse(jsonText);

console.log(userData.name);
```

Em uma API Express, `res.json(value)` normalmente é a maneira mais
direta de responder com JSON:

``` js
app.get("/api/user", (req, res) => {
    res.json({
        name: "Ada",
        active: true
    });
});
```

Não é necessário chamar `JSON.stringify()` manualmente nesse caso: o
Express serializa o objeto para a resposta.

## 4. Promises e `async`/`await`

Algumas operações não terminam imediatamente: ler arquivos, consultar
serviços, iniciar navegadores ou fazer requisições de rede são exemplos
comuns. Essas operações podem retornar uma **Promise**.

``` js
async function getMessage() {
    return "Concluído";
}

const result = getMessage();
console.log(result);
```

O resultado de `getMessage()` é uma Promise, não diretamente a string.
Por isso, o console pode mostrar algo como `Promise { <pending> }`: a
operação ainda está pendente ou a Promise não foi aguardada.

Use `await` dentro de uma função `async` ou no topo de um arquivo ESM:

``` js
const message = await getMessage();
console.log(message);
```

Também é possível tratar erros com `try`/`catch`:

``` js
try {
    const result = await performTask();
    console.log(result);
} catch (error) {
    console.error("A operação falhou:", error);
}
```

**Ideia central:** se uma função retorna uma Promise, use `await` quando
precisar do resultado resolvido antes de continuar.

## 5. Inicialização de uma API Express

Uma API Express costuma seguir esta estrutura:

``` js
import express from "express";

const app = express();
const PORT = 3000;

app.use(express.json());

app.get("/", (req, res) => {
    res.json({ status: "online" });
});

app.listen(PORT, () => {
    console.log(`Servidor disponível na porta ${PORT}`);
});
```

`app.listen()` inicia o servidor para que ele passe a aceitar
requisições. A ordem de inicialização importa.

### Tarefa assíncrona antes de iniciar o servidor

Se o servidor depende de uma tarefa para funcionar corretamente, pode
ser apropriado aguardá-la antes de chamar `listen()`:

``` js
await initializeApplication();

app.listen(PORT, () => {
    console.log(`Servidor disponível na porta ${PORT}`);
});
```

Isso garante que a inicialização termine antes de o servidor começar a
aceitar requisições. Porém, se `initializeApplication()` precisar fazer
uma requisição à própria API, essa ordem pode causar espera ou falha,
pois o servidor ainda não está escutando.

### Tarefa que pode ocorrer depois de iniciar o servidor

Se a tarefa não for necessária para o servidor começar a responder, ela
pode ser executada depois:

``` js
app.listen(PORT, async () => {
    console.log(`Servidor disponível na porta ${PORT}`);

    try {
        await runBackgroundTask();
    } catch (error) {
        console.error("A tarefa falhou:", error);
    }
});
```

Escolha a ordem de acordo com as dependências reais. Não mova uma tarefa
antes ou depois de `listen()` sem verificar se ela precisa acessar a
própria API.

## 6. Renderizar HTML em PNG com Playwright

O Playwright pode abrir uma página em um navegador automatizado e
capturar uma imagem. Isso é útil para gerar prévias, cartões, relatórios
visuais e imagens estáticas de componentes HTML.

Instale a dependência e o navegador:

``` bash
npm install -D playwright
npx playwright install chromium
```

Exemplo de script ESM chamado `capture.js`:

``` js
import { chromium } from "playwright";

const browser = await chromium.launch();

try {
    const page = await browser.newPage({
        viewport: {
            width: 1200,
            height: 400
        },
        deviceScaleFactor: 2
    });

    await page.goto("http://127.0.0.1:3000/example.html", {
        waitUntil: "networkidle"
    });

    await page.screenshot({
        path: "page.png"
    });
} finally {
    await browser.close();
}
```

O endereço usado no exemplo precisa apontar para uma página realmente
disponível. Se o HTML for um arquivo local, também é possível abrir uma
URL `file://` construída corretamente ou usar `page.setContent()` para
fornecer o HTML diretamente.

### O que significam as opções?

-   `viewport`: define a largura e a altura da área de visualização em
    CSS pixels.
-   `deviceScaleFactor`: controla a escala de pixels da captura. Com
    valor `2`, a imagem normalmente terá o dobro de pixels em cada
    dimensão da área capturada. Isso costuma melhorar a nitidez, mas
    também aumenta o tamanho do arquivo.
-   `waitUntil: "networkidle"`: espera que a atividade de rede fique
    ociosa. Nem toda página atinge esse estado, por exemplo, páginas que
    mantêm conexões constantes; nesses casos, pode ser necessário
    aguardar um seletor ou outro sinal explícito de que o conteúdo
    terminou de carregar.
-   `path`: indica onde salvar o PNG.

A captura de página inteira pode incluir espaço excedente. Para obter
somente um componente, prefira capturar o elemento específico.

## 7. Capturar somente um elemento HTML

Considere um componente com um identificador:

``` html
<section id="card">
    <h1>Olá!</h1>
    <p>Este é um cartão de exemplo.</p>
</section>
```

No Playwright:

``` js
const card = page.locator("#card");

await card.screenshot({
    path: "card.png"
});
```

O Playwright captura os limites do elemento selecionado, em vez de
capturar a página inteira. O seletor precisa corresponder a um elemento
existente, e ele deve estar visível.

Se o conteúdo for carregado de forma assíncrona, aguarde a condição
apropriada antes de capturar:

``` js
await page.locator("#card").waitFor({ state: "visible" });
await page.locator("#card").screenshot({ path: "card.png" });
```

A captura de um elemento evita boa parte do espaço externo da página,
mas não remove margens ou preenchimentos que façam parte do próprio
elemento. Ajuste o CSS se eles não forem desejados.

## 8. PNG com fundo transparente e cantos arredondados

O formato PNG suporta transparência. Para gerar cantos externos
transparentes, é necessário que os pixels fora do componente não sejam
pintados com uma cor sólida.

Exemplo de CSS:

``` css
html,
body {
    margin: 0;
    background: transparent;
}

#card {
    border-radius: 16px;
    overflow: hidden;
    background: #202938;
    color: white;
}
```

-   `margin: 0` remove a margem padrão do documento.
-   `background: transparent` deixa o fundo da página transparente.
-   `border-radius` arredonda os cantos do componente.
-   `overflow: hidden` recorta o conteúdo que ultrapassaria os limites
    arredondados.
-   O fundo sólido aplicado ao próprio cartão mantém o interior
    preenchido, enquanto os cantos externos podem permanecer
    transparentes.

Para capturar o elemento sem pintar o fundo padrão da página:

``` js
await page.locator("#card").screenshot({
    path: "card.png",
    omitBackground: true
});
```

`omitBackground: true` faz com que o Playwright omita o fundo padrão do
documento durante a captura. Isso não transforma automaticamente todas
as áreas brancas em transparentes: se algum elemento realmente tiver
fundo branco, esse branco continuará na imagem.

### Suavidade das bordas

Para curvas e texto mais nítidos, use uma escala de captura maior, por
exemplo `deviceScaleFactor: 2`. A suavização depende também do
navegador, do CSS e do tipo de conteúdo. O aumento da escala não
equivale a desfocar as bordas nem cria transparência sozinho.

## 9. Responsividade HTML versus imagem estática

Uma página HTML pode reorganizar seu conteúdo conforme a largura
disponível usando CSS responsivo, como media queries, Flexbox e Grid.
Uma imagem PNG, por outro lado, é uma captura estática: ela não
recalcula o layout quando a tela muda.

É possível fazer a imagem ocupar uma largura adaptável em uma página:

``` html
<img
    src="./card.png"
    alt="Cartão de exemplo"
    style="display: block; width: 100%; height: auto;"
/>
```

Isso redimensiona a imagem proporcionalmente, mas não reorganiza os
elementos que já foram renderizados dentro dela.

Se o layout precisar mudar bastante em telas menores, considere gerar
versões em diferentes dimensões ou usar HTML/CSS diretamente em um
ambiente que aceite esse conteúdo. Em plataformas que aceitam apenas
imagens estáticas, a imagem terá de representar uma composição já
renderizada.

## 10. Lista de verificação para depuração

Quando algo não funcionar, verifique estes pontos:

1.  **Módulos:** o projeto está usando ESM ou CommonJS? As importações e
    exportações seguem o mesmo formato?
2.  **Caminhos:** o caminho é relativo ao arquivo ou ao diretório de
    trabalho? O arquivo realmente existe?
3.  **Promises:** a função retorna uma Promise? O código aguarda o
    resultado com `await`?
4.  **Ordem de inicialização:** a tarefa precisa que a API já esteja
    escutando, ou precisa terminar antes de o servidor aceitar
    requisições?
5.  **Captura:** o seletor identifica o elemento correto e ele já está
    visível?
6.  **Dimensões:** o `viewport` corresponde ao layout desejado?
7.  **Espaços excedentes:** existem margens, preenchimentos ou alturas
    desnecessárias no documento ou no componente?
8.  **Transparência:** o fundo da página e os elementos externos são
    transparentes? Há algum elemento branco realmente pintado?
9.  **Nitidez:** uma escala de captura maior melhora o resultado sem
    deixar o arquivo desnecessariamente pesado?
10. **Erros:** use `try`/`catch` em tarefas assíncronas e leia a
    mensagem completa do terminal.

------------------------------------------------------------------------

## Resumo

-   Use `default` para a exportação principal de um módulo e exportações
    nomeadas para funcionalidades identificadas explicitamente.
-   Não misture `require`/`module.exports` com `import`/`export` sem
    entender a configuração de módulos.
-   `JSON.stringify()` converte dados para texto JSON; `JSON.parse()`
    faz o caminho inverso; `res.json()` facilita respostas JSON no
    Express.
-   Uma Promise representa o resultado futuro de uma operação
    assíncrona; use `await` quando precisar do valor resolvido.
-   A ordem entre tarefas assíncronas e `app.listen()` depende das
    dependências da aplicação.
-   O Playwright captura páginas inteiras ou elementos específicos em
    PNG.
-   `deviceScaleFactor` pode aumentar a nitidez; `omitBackground: true`
    ajuda a preservar transparência.
-   HTML/CSS pode ser responsivo; um PNG é estático e só pode ser
    redimensionado depois de gerado.
