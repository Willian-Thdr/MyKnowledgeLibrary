# Como obter informações JSON de um site usando JavaScript

## 1. Introdução

Muitos sites disponibilizam informações em formato JSON (*JavaScript Object Notation*), uma estrutura textual utilizada para representar e transmitir dados entre aplicações.

Por exemplo, um site pode disponibilizar informações sobre usuários, produtos, notícias, jogos ou estatísticas por meio de uma API. O JavaScript permite realizar requisições HTTP para acessar esses dados e utilizá-los em aplicações web.

Existem diferentes maneiras de obter essas informações, dependendo de como o site foi desenvolvido e de quais recursos ele disponibiliza.

As principais abordagens são:

- **Consumir uma API:** solicitar dados diretamente de um endpoint que retorna JSON.
- **Analisar o HTML:** obter o conteúdo de uma página e extrair informações de seus elementos.
- **Ler JSON incorporado no HTML:** localizar dados estruturados que o próprio site inclui no documento.
- **Realizar requisições pelo servidor:** utilizar Node.js para buscar dados quando a operação não pode ou não deve ser executada diretamente no navegador.

---

## 2. Obtendo dados JSON com `fetch()`

A maneira mais comum de obter dados JSON é utilizar a função `fetch()`, nativa dos navegadores modernos e também disponível nas versões atuais do Node.js.

A função permite realizar requisições HTTP para um endereço específico.

### Exemplo básico

```javascript
async function obterDados() {
    const resposta = await fetch(
        "https://jsonplaceholder.typicode.com/users"
    );

    const dados = await resposta.json();

    console.log(dados);
}

obterDados();
```

Nesse exemplo, utilizamos uma API pública de demonstração que retorna informações fictícias de usuários.

### Como funciona o código?

1. `fetch(url)` envia uma requisição HTTP ao endereço informado.
2. `await` aguarda a conclusão da operação assíncrona.
3. `resposta.json()` interpreta o corpo da resposta como JSON.
4. `console.log(dados)` exibe os dados obtidos.

O resultado será um array de objetos JavaScript, cada um contendo propriedades como `id`, `name`, `username`, `email` e `address`.

**Importante:** o método `response.json()` não transforma qualquer conteúdo em JSON. Ele tenta interpretar o corpo da resposta como JSON válido e pode gerar um erro caso o conteúdo seja HTML, texto inválido ou esteja vazio.

---

## 3. Tratamento de erros

Uma requisição pode falhar por diversos motivos:

- O servidor está indisponível.
- O endereço está incorreto.
- A conexão foi interrompida.
- O servidor retorna um código HTTP de erro.
- O conteúdo recebido não é um JSON válido.
- O navegador bloqueia o acesso devido às regras de CORS.

Além disso, `fetch()` não rejeita automaticamente a promessa quando o servidor retorna códigos como `404` ou `500`. Por isso, é necessário verificar a propriedade `response.ok`.

### Exemplo com tratamento de erros

```javascript
async function obterDados() {
    try {
        const resposta = await fetch(
            "https://jsonplaceholder.typicode.com/users"
        );

        if (!resposta.ok) {
            throw new Error(
                `Erro HTTP: ${resposta.status}`
            );
        }

        const dados = await resposta.json();

        console.log("Dados recebidos:", dados);
    } catch (erro) {
        console.error(
            "Não foi possível obter os dados:",
            erro.message
        );
    }
}

obterDados();
```

O bloco `try...catch` permite tratar falhas de rede, erros lançados pelo programa e problemas na interpretação do JSON.

---

## 4. Acessando propriedades específicas

Depois de obter o JSON, os dados passam a ser objetos ou arrays JavaScript. Isso permite acessar suas propriedades normalmente.

Considere a seguinte estrutura:

```json
{
    "id": 1,
    "nome": "Carlos",
    "idade": 25,
    "ativo": true
}
```

Se esse objeto estiver armazenado na variável `usuario`, podemos acessar seus valores desta maneira:

```javascript
console.log(usuario.nome);
console.log(usuario.idade);
console.log(usuario.ativo);
```

Para percorrer um array de usuários:

```javascript
const resposta = await fetch(
    "https://jsonplaceholder.typicode.com/users"
);

const usuarios = await resposta.json();

for (const usuario of usuarios) {
    console.log(usuario.name);
    console.log(usuario.email);
}
```

Também é possível filtrar os resultados:

```javascript
const usuariosFiltrados = usuarios.filter(
    usuario => usuario.name.includes("Leanne")
);

console.log(usuariosFiltrados);
```

A partir desse ponto, os dados podem ser utilizados para preencher tabelas, montar interfaces, gerar relatórios ou alimentar outras partes de uma aplicação.

---

## 5. Como descobrir se um site disponibiliza uma API JSON

Nem todo site possui uma API pública documentada. Antes de tentar extrair informações, é recomendável verificar se existe um endpoint apropriado.

Uma maneira prática de investigar isso é utilizar as ferramentas de desenvolvedor do navegador.

### Procedimento

1. Abra o site desejado.
2. Pressione `F12` para abrir as ferramentas de desenvolvedor.
3. Acesse a aba **Network** (Rede).
4. Selecione o filtro **Fetch/XHR**, quando disponível.
5. Atualize a página.
6. Observe as requisições realizadas.
7. Selecione uma requisição e examine as abas **Headers**, **Preview** e **Response**.

A aba **Response** mostra o conteúdo recebido do servidor. Se a resposta contiver JSON, será possível observar sua estrutura e identificar as propriedades disponíveis.

A aba **Headers** permite verificar informações como:

- URL da requisição;
- método HTTP;
- código de status;
- tipo de conteúdo;
- cabeçalhos enviados e recebidos.

Por exemplo, uma resposta pode apresentar o cabeçalho:

```http
Content-Type: application/json
```

Isso indica que o servidor declara estar enviando JSON.

Entretanto, esse cabeçalho não garante, isoladamente, que o corpo seja um JSON válido.

### Reproduzindo a requisição

Depois de identificar o endpoint, é possível tentar acessá-lo com `fetch()`:

```javascript
const resposta = await fetch(
    "https://exemplo.com/api/produtos"
);

const produtos = await resposta.json();

console.log(produtos);
```

O endereço acima é apenas ilustrativo. O endpoint real deve ser obtido na documentação do serviço ou nas requisições legítimas que o site realiza.

Algumas APIs exigem parâmetros, autenticação ou cabeçalhos específicos. Nesses casos, a requisição precisa respeitar os requisitos documentados pelo serviço.

---

## 6. E se o site não disponibilizar uma API?

Se o site não oferecer uma API acessível, uma alternativa é obter o HTML da página e extrair informações de seus elementos.

É importante compreender a diferença entre HTML e JSON: **o HTML representa a estrutura de uma página; o JSON representa dados estruturados**. Um documento HTML não se torna JSON simplesmente porque contém informações organizadas.

No navegador, podemos analisar o HTML usando o DOM (*Document Object Model*).

### Exemplo de leitura de elementos da página atual

```javascript
const titulo = document.querySelector("h1");

if (titulo) {
    console.log(titulo.textContent);
}
```

Esse exemplo obtém o texto do primeiro elemento `h1` da página atual.

Para selecionar vários elementos:

```javascript
const links = document.querySelectorAll("a");

for (const link of links) {
    console.log({
        texto: link.textContent.trim(),
        endereco: link.href
    });
}
```

Esse procedimento funciona com o documento que já está carregado no navegador.

**Limitação importante:** executar `document.querySelector()` em um site acessado pelo navegador não concede automaticamente acesso ao HTML de outros domínios.

---

## 7. Obtendo o HTML de outra página

É possível tentar obter o HTML de uma página com `fetch()`:

```javascript
async function obterHTML(url) {
    const resposta = await fetch(url);

    if (!resposta.ok) {
        throw new Error(`Erro HTTP: ${resposta.status}`);
    }

    const html = await resposta.text();

    return html;
}
```

Observe que utilizamos `response.text()`, e não `response.json()`, pois estamos esperando receber HTML.

O conteúdo pode então ser analisado com `DOMParser` em um navegador:

```javascript
async function extrairTitulo(url) {
    const html = await obterHTML(url);

    const documento = new DOMParser().parseFromString(
        html,
        "text/html"
    );

    return documento.querySelector("title")?.textContent;
}
```

Entretanto, esse código somente funcionará se o navegador permitir que a aplicação obtenha a resposta do endereço solicitado.

### O que é CORS?

CORS (*Cross-Origin Resource Sharing*) é um mecanismo de segurança dos navegadores que controla quais origens podem acessar determinados recursos de outra origem.

Por exemplo, uma aplicação executada em:

```text
https://minhaaplicacao.com
```

pode tentar acessar:

```text
https://outrosite.com/dados
```

Se o servidor de destino não autorizar essa origem por meio dos cabeçalhos apropriados, o navegador poderá impedir que o JavaScript leia a resposta.

Isso não significa necessariamente que o endereço esteja indisponível. A requisição pode até chegar ao servidor, mas o navegador não permitirá que o código da aplicação acesse seu conteúdo.

CORS é uma política aplicada pelo navegador; não é um mecanismo de autenticação e não substitui as permissões do servidor.

Quando houver essa restrição, as alternativas adequadas incluem utilizar uma API oficialmente disponibilizada, solicitar a configuração correta ao responsável pelo servidor ou realizar a consulta por um backend autorizado.

Não é recomendável tentar contornar a restrição por meio de proxies públicos desconhecidos.

---

## 8. Extraindo JSON incorporado no HTML

Alguns sites incluem dados JSON diretamente no HTML, em vez de disponibilizá-los exclusivamente por meio de uma API independente.

Uma técnica comum é utilizar um elemento `script` com o atributo `type="application/json"`.

Por exemplo:

```html
<script id="dados" type="application/json">
{
    "produto": "Teclado",
    "preco": 199.90
}
</script>
```

Se esse elemento estiver presente no documento atual, podemos extrair o conteúdo e interpretá-lo:

```javascript
const elemento = document.querySelector("#dados");

if (elemento) {
    const dados = JSON.parse(elemento.textContent);

    console.log(dados.produto);
    console.log(dados.preco);
}
```

Nesse caso, `JSON.parse()` transforma uma string JSON em um objeto JavaScript.

Algumas aplicações também incluem dados em scripts executáveis ou em estruturas internas utilizadas para renderização. Esses casos exigem uma análise específica da implementação do site; nem todo script contém JSON independente ou pode ser interpretado com segurança usando `JSON.parse()`.

Além disso, o conteúdo HTML recebido inicialmente pode ser diferente do DOM final construído por JavaScript. Páginas que carregam dados dinamicamente podem exigir a identificação da requisição de rede responsável por fornecer esses dados.

---

## 9. Quando utilizar Node.js

O Node.js permite executar JavaScript fora do navegador. Ele é útil para criar scripts de coleta autorizada, serviços intermediários e aplicações de backend.

Em versões atuais do Node.js, `fetch()` está disponível globalmente.

### Exemplo em Node.js

Crie um arquivo chamado `buscar.js`:

```javascript
async function obterUsuarios() {
    try {
        const resposta = await fetch(
            "https://jsonplaceholder.typicode.com/users"
        );

        if (!resposta.ok) {
            throw new Error(
                `Erro HTTP: ${resposta.status}`
            );
        }

        const usuarios = await resposta.json();

        console.log(usuarios);
    } catch (erro) {
        console.error("Falha na requisição:", erro);
    }
}

obterUsuarios();
```

Execute no terminal:

```bash
node buscar.js
```

Diferentemente do navegador, o Node.js não aplica automaticamente a política CORS do navegador às requisições realizadas por `fetch()`.

Isso, contudo, não garante acesso irrestrito. O servidor ainda pode exigir autenticação, rejeitar a requisição, limitar o tráfego ou aplicar outras regras de segurança.

O uso de Node.js também não autoriza acessar dados privados ou contornar controles de acesso.

### Quando escolher cada abordagem?

| Situação | Abordagem recomendada |
|---|---|
| O site possui uma API JSON pública | `fetch()` no navegador ou no Node.js |
| A aplicação precisa ler sua própria página | DOM e `document.querySelector()` |
| O HTML contém JSON incorporado | Seleção do elemento e `JSON.parse()` |
| A aplicação precisa consultar uma API sem autorização CORS para o navegador | Backend autorizado, respeitando as regras do serviço |
| O serviço exige credenciais secretas | Backend, com credenciais armazenadas de maneira segura |

---

## 10. Boas práticas

Ao obter dados de sites, algumas precauções são fundamentais.

### Verifique o status HTTP

Não presuma que toda resposta bem-sucedida do ponto de vista da rede contém dados válidos.

```javascript
if (!resposta.ok) {
    throw new Error(`HTTP ${resposta.status}`);
}
```

### Valide os dados

Mesmo quando o servidor retorna JSON válido, as propriedades podem estar ausentes ou possuir tipos inesperados.

```javascript
if (!Array.isArray(usuarios)) {
    throw new Error("Formato de dados inesperado");
}
```

### Evite expor credenciais

Chaves privadas, tokens secretos e senhas não devem ser inseridos diretamente em código executado no navegador. Utilize um backend quando for necessário proteger essas informações.

### Respeite os limites do serviço

Verifique a documentação, os limites de requisições, os termos de uso e as permissões de acesso. Evite sobrecarregar servidores com requisições excessivas.

### Prefira APIs oficiais

APIs documentadas geralmente oferecem estruturas mais estáveis e previsíveis do que a extração direta de HTML. Alterações no layout de uma página podem quebrar um extrator baseado em seletores CSS.

---

## 11. Conclusão

Para obter informações JSON de um site com JavaScript, o primeiro passo é identificar de onde os dados vêm.

Se o site disponibilizar um endpoint JSON, utilize `fetch()` e interprete a resposta com `response.json()`. Se os dados estiverem no HTML, será necessário analisar o documento e localizar os elementos ou estruturas relevantes. Quando a aplicação estiver sujeita às restrições do navegador, um backend autorizado poderá ser a solução adequada.

A escolha da técnica depende da arquitetura do site, do formato da resposta, das permissões de acesso e do ambiente em que o código será executado.

A regra principal é simples: **identifique a fonte real dos dados antes de implementar a extração**. Isso reduz erros, evita soluções frágeis e facilita a manutenção do código.
