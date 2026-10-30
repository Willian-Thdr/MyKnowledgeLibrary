# Guia de Métodos e Propriedades do JavaScript

> Referência de consulta para estudar JavaScript. Os métodos estão organizados por tipo de dado e finalidade.
>
> **Legenda:**
> - `()` indica um método que pode ser chamado.
> - `length` é uma propriedade, não um método.
> - Métodos que retornam um novo valor normalmente não modificam o original, salvo indicação contrária.
> - Alguns recursos dependem do navegador ou do ambiente Node.js.

---

# 1. Strings — `String`

Strings são sequências de caracteres utilizadas para armazenar textos.

```javascript
const texto = "Olá, JavaScript!";
```

## 1.1. Consulta e identificação

| Método ou propriedade | Utilidade | Exemplo |
|---|---|---|
| `.length` | Retorna o comprimento da string em unidades UTF-16. | `"Olá".length` → `3` |
| `.at(index)` | Retorna o caractere de um índice, aceitando índices negativos. | `"ABC".at(-1)` → `"C"` |
| `.charAt(index)` | Retorna o caractere de um índice. | `"ABC".charAt(1)` → `"B"` |
| `.charCodeAt(index)` | Retorna o valor UTF-16 do caractere. | `"A".charCodeAt(0)` → `65` |
| `.codePointAt(index)` | Retorna o ponto de código Unicode. | `"A".codePointAt(0)` → `65` |
| `.indexOf(valor)` | Retorna o índice da primeira ocorrência ou `-1`. | `"banana".indexOf("na")` → `2` |
| `.lastIndexOf(valor)` | Retorna o índice da última ocorrência ou `-1`. | `"banana".lastIndexOf("na")` → `4` |
| `.includes(valor)` | Verifica se contém determinado texto. | `"banana".includes("ana")` → `true` |
| `.startsWith(valor)` | Verifica se começa com determinado texto. | `"JavaScript".startsWith("Java")` → `true` |
| `.endsWith(valor)` | Verifica se termina com determinado texto. | `"arquivo.txt".endsWith(".txt")` → `true` |
| `.localeCompare(texto)` | Compara strings segundo regras de ordenação linguística. | `"a".localeCompare("b")` |

## 1.2. Transformação de texto

| Método | Utilidade | Exemplo |
|---|---|---|
| `.toUpperCase()` | Converte para maiúsculas. | `"olá".toUpperCase()` → `"OLÁ"` |
| `.toLowerCase()` | Converte para minúsculas. | `"OLÁ".toLowerCase()` → `"olá"` |
| `.toLocaleUpperCase()` | Converte para maiúsculas segundo regras locais. | `"i".toLocaleUpperCase("tr")` |
| `.toLocaleLowerCase()` | Converte para minúsculas segundo regras locais. | `"I".toLocaleLowerCase("tr")` |
| `.trim()` | Remove espaços em branco das extremidades. | `"  oi  ".trim()` → `"oi"` |
| `.trimStart()` | Remove espaços do início. | `"  oi".trimStart()` → `"oi"` |
| `.trimEnd()` | Remove espaços do final. | `"oi  ".trimEnd()` → `"oi"` |
| `.padStart(tamanho, texto)` | Preenche o início até atingir determinado comprimento. | `"5".padStart(3, "0")` → `"005"` |
| `.padEnd(tamanho, texto)` | Preenche o final até atingir determinado comprimento. | `"5".padEnd(3, "0")` → `"500"` |
| `.repeat(quantidade)` | Repete a string. | `"ha".repeat(3)` → `"hahaha"` |
| `.replace(alvo, novo)` | Substitui a primeira ocorrência, conforme o alvo. | `"a-a".replace("-", "/")` → `"a/a"` |
| `.replaceAll(alvo, novo)` | Substitui todas as ocorrências correspondentes. | `"a-a".replaceAll("-", "/")` → `"a/a"` |
| `.normalize()` | Normaliza a representação Unicode. | `"é".normalize("NFC")` |
| `.toWellFormed()` | Substitui unidades UTF-16 isoladas por U+FFFD. | `"texto".toWellFormed()` |

## 1.3. Extração e divisão

| Método | Utilidade | Exemplo |
|---|---|---|
| `.slice(inicio, fim)` | Extrai parte da string; aceita índices negativos. | `"JavaScript".slice(0, 4)` → `"Java"` |
| `.substring(inicio, fim)` | Extrai parte da string; índices negativos são tratados como zero. | `"JavaScript".substring(4, 10)` → `"Script"` |
| `.split(separador)` | Divide a string e retorna um array. | `"a,b,c".split(",")` → `["a","b","c"]` |
| `.match(expressao)` | Retorna correspondências com uma expressão regular. | `"abc123".match(/\d+/)` |
| `.matchAll(expressao)` | Retorna um iterador com todas as correspondências e seus grupos. | `Array.from("a1b2".matchAll(/\d/g))` |
| `.search(expressao)` | Retorna o índice da primeira correspondência ou `-1`. | `"abc123".search(/\d/)` → `3` |

## 1.4. Métodos estáticos de `String`

| Método | Utilidade |
|---|---|
| `String(valor)` | Converte um valor em string. |
| `String.fromCharCode(...)` | Cria uma string a partir de unidades UTF-16. |
| `String.fromCodePoint(...)` | Cria uma string a partir de pontos de código Unicode. |
| `String.raw(...)` | Obtém o texto bruto de um template literal marcado. |

**Observação:** strings são imutáveis. Métodos como `.replace()` e `.toUpperCase()` retornam uma nova string, sem modificar a original.

---

# 2. Arrays — `Array`

Arrays armazenam coleções ordenadas de valores.

```javascript
const numeros = [10, 20, 30, 40];
```

## 2.1. Consulta e verificação

| Método ou propriedade | Utilidade | Exemplo |
|---|---|---|
| `.length` | Retorna a quantidade de posições ocupadas até o último índice existente, incluindo eventuais lacunas. | `[10,20,30].length` → `3` |
| `.at(indice)` | Obtém um elemento pelo índice, aceitando negativos. | `[10,20,30].at(-1)` → `30` |
| `.includes(valor)` | Verifica se contém um valor. | `[1,2,3].includes(2)` → `true` |
| `.indexOf(valor)` | Retorna o índice da primeira ocorrência ou `-1`. | `[1,2,3].indexOf(3)` → `2` |
| `.lastIndexOf(valor)` | Retorna o índice da última ocorrência ou `-1`. | `[1,2,1].lastIndexOf(1)` → `2` |
| `.find(callback)` | Retorna o primeiro elemento que satisfaz a condição. | `[2,4,5].find(n => n % 2)` → `5` |
| `.findIndex(callback)` | Retorna o índice do primeiro elemento que satisfaz a condição. | `[2,4,5].findIndex(n => n % 2)` → `2` |
| `.findLast(callback)` | Retorna o último elemento que satisfaz a condição. | `[1,2,3,4].findLast(n => n % 2 === 0)` → `4` |
| `.findLastIndex(callback)` | Retorna o índice do último elemento correspondente. | `[1,2,3,4].findLastIndex(n => n % 2 === 0)` → `3` |
| `.some(callback)` | Verifica se pelo menos um elemento satisfaz a condição. | `[1,3,4].some(n => n % 2 === 0)` → `true` |
| `.every(callback)` | Verifica se todos os elementos satisfazem a condição. | `[2,4,6].every(n => n % 2 === 0)` → `true` |

## 2.2. Iteração e transformação

| Método | Utilidade | Exemplo |
|---|---|---|
| `.forEach(callback)` | Executa uma função para cada elemento. | `[1,2].forEach(n => console.log(n))` |
| `.map(callback)` | Cria um novo array com os resultados da função. | `[1,2,3].map(n => n * 2)` → `[2,4,6]` |
| `.filter(callback)` | Cria um array apenas com elementos aprovados pela condição. | `[1,2,3,4].filter(n => n > 2)` → `[3,4]` |
| `.flat(profundidade)` | Achata arrays aninhados até determinada profundidade. | `[1,[2,[3]]].flat(2)` → `[1,2,3]` |
| `.flatMap(callback)` | Aplica um mapeamento e achata um nível. | `[1,2].flatMap(n => [n,n])` → `[1,1,2,2]` |
| `.reduce(callback, inicial)` | Reduz os elementos a um único resultado. | `[1,2,3].reduce((a,b) => a+b, 0)` → `6` |
| `.reduceRight(callback, inicial)` | Reduz percorrendo o array da direita para a esquerda. | `["a","b"].reduceRight((a,b) => a+b, "")` → `"ba"` |

## 2.3. Inserção, remoção e alteração

| Método | Utilidade | Modifica o array original? |
|---|---|---|
| `.push(valor)` | Adiciona um ou mais elementos ao final. | Sim |
| `.pop()` | Remove e retorna o último elemento. | Sim |
| `.unshift(valor)` | Adiciona elementos no início. | Sim |
| `.shift()` | Remove e retorna o primeiro elemento. | Sim |
| `.splice(inicio, quantidade, ...itens)` | Remove, substitui ou insere elementos em posições específicas. | Sim |
| `.fill(valor, inicio, fim)` | Preenche posições com um valor. | Sim |
| `.copyWithin(destino, inicio, fim)` | Copia parte do array para outra posição do próprio array. | Sim |
| `.reverse()` | Inverte a ordem dos elementos. | Sim |
| `.sort(callback)` | Ordena os elementos. Por padrão, compara representações em string. | Sim |

Exemplo de ordenação numérica:

```javascript
const numeros = [10, 2, 30];

numeros.sort((a, b) => a - b);

console.log(numeros); // [2, 10, 30]
```

## 2.4. Cópia, concatenação e conversão

| Método | Utilidade | Exemplo |
|---|---|---|
| `.slice(inicio, fim)` | Retorna uma cópia superficial de parte do array. | `[1,2,3].slice(1)` → `[2,3]` |
| `.concat(outroArray)` | Concatena arrays ou valores. | `[1,2].concat([3,4])` → `[1,2,3,4]` |
| `.join(separador)` | Junta elementos em uma string. | `["a","b"].join("-")` → `"a-b"` |
| `.toString()` | Converte o array em uma string, geralmente separada por vírgulas. | `[1,2,3].toString()` → `"1,2,3"` |
| `.toLocaleString()` | Converte elementos em representações localizadas. | `[1000].toLocaleString("pt-BR")` |
| `.with(indice, valor)` | Retorna uma cópia com um elemento substituído. | `[1,2,3].with(1,9)` → `[1,9,3]` |
| `.toReversed()` | Retorna uma cópia invertida. | `[1,2,3].toReversed()` → `[3,2,1]` |
| `.toSorted(callback)` | Retorna uma cópia ordenada. | `[3,1,2].toSorted((a,b) => a-b)` |
| `.toSpliced(...)` | Retorna uma cópia com alterações equivalentes às de `splice()`. | `[1,2,3].toSpliced(1,1)` → `[1,3]` |

## 2.5. Métodos estáticos de `Array`

| Método | Utilidade |
|---|---|
| `Array.isArray(valor)` | Verifica se um valor é um array. |
| `Array.from(iteravel)` | Cria um array a partir de um iterável ou objeto semelhante a array. |
| `Array.fromAsync(iteravel)` | Cria um array a partir de um iterável assíncrono ou de valores assíncronos. |
| `Array.of(...valores)` | Cria um array com os argumentos recebidos. |

Exemplo:

```javascript
Array.isArray([1, 2, 3]); // true
Array.from("ABC");        // ["A", "B", "C"]
Array.of(5);              // [5]
```

---

# 3. Objetos — `Object`

Objetos armazenam dados em pares de chave e valor.

```javascript
const usuario = {
    nome: "Ana",
    idade: 20
};
```

## 3.1. Métodos estáticos de `Object`

| Método | Utilidade |
|---|---|
| `Object.keys(obj)` | Retorna um array com as chaves próprias enumeráveis. |
| `Object.values(obj)` | Retorna um array com os valores próprios enumeráveis. |
| `Object.entries(obj)` | Retorna um array de pares `[chave, valor]`. |
| `Object.fromEntries(iteravel)` | Converte pares `[chave, valor]` em um objeto. |
| `Object.assign(destino, ...fontes)` | Copia propriedades enumeráveis para o objeto de destino. |
| `Object.hasOwn(obj, chave)` | Verifica se o objeto possui determinada propriedade própria. |
| `Object.freeze(obj)` | Impede alterações nas propriedades próprias do objeto, sem congelar recursivamente os objetos internos. |
| `Object.seal(obj)` | Impede adicionar ou remover propriedades, mas permite alterar propriedades existentes que sejam graváveis. |
| `Object.preventExtensions(obj)` | Impede a adição de novas propriedades. |
| `Object.is(valor1, valor2)` | Compara valores segundo as regras de `Object.is()`. |
| `Object.create(prototipo)` | Cria um objeto com o protótipo especificado. |
| `Object.getPrototypeOf(obj)` | Obtém o protótipo do objeto. |
| `Object.setPrototypeOf(obj, prototipo)` | Altera o protótipo do objeto; seu uso costuma ser desaconselhado em código de desempenho crítico. |
| `Object.getOwnPropertyNames(obj)` | Retorna os nomes de todas as propriedades próprias, inclusive as não enumeráveis. |
| `Object.getOwnPropertySymbols(obj)` | Retorna os símbolos que são propriedades próprias. |
| `Object.getOwnPropertyDescriptor(obj, chave)` | Obtém o descritor de uma propriedade própria. |
| `Object.getOwnPropertyDescriptors(obj)` | Obtém os descritores de todas as propriedades próprias. |
| `Object.defineProperty(obj, chave, descritor)` | Cria ou altera uma propriedade usando um descritor. |
| `Object.defineProperties(obj, descritores)` | Define várias propriedades de uma vez. |
| `Object.isFrozen(obj)` | Verifica se o objeto está congelado. |
| `Object.isSealed(obj)` | Verifica se o objeto está selado. |
| `Object.isExtensible(obj)` | Verifica se novas propriedades podem ser adicionadas. |
| `Object.groupBy(iteravel, callback)` | Agrupa elementos de um iterável em um objeto conforme o resultado da função. |

Exemplo:

```javascript
const usuario = {
    nome: "Ana",
    idade: 20
};

console.log(Object.keys(usuario));
// ["nome", "idade"]

console.log(Object.values(usuario));
// ["Ana", 20]

console.log(Object.entries(usuario));
// [["nome", "Ana"], ["idade", 20]]
```

**Atenção:** `Object.freeze()` não torna o objeto profundamente imutável. Se ele contiver outro objeto, esse objeto interno ainda poderá ser alterado, salvo se também for congelado.

---

# 4. Números — `Number` e `Math`

## 4.1. Métodos de `Number`

| Método ou propriedade | Utilidade |
|---|---|
| `Number(valor)` | Converte um valor em número, quando possível. |
| `Number.isFinite(valor)` | Verifica se o valor é um número finito, sem fazer coerção de tipo. |
| `Number.isInteger(valor)` | Verifica se o valor é um número inteiro. |
| `Number.isNaN(valor)` | Verifica se o valor é exatamente `NaN`. |
| `Number.isSafeInteger(valor)` | Verifica se o valor é um inteiro seguro. |
| `Number.parseInt(texto, base)` | Converte o início de uma string em inteiro. |
| `Number.parseFloat(texto)` | Converte o início de uma string em número de ponto flutuante. |
| `.toFixed(casas)` | Formata um número com determinada quantidade de casas decimais e retorna uma string. |
| `.toPrecision(dígitos)` | Formata o número com determinada quantidade de algarismos significativos. |
| `.toExponential(casas)` | Retorna uma representação em notação científica. |
| `.toString(base)` | Converte o número em string, opcionalmente usando outra base. |
| `.toLocaleString(local)` | Formata o número conforme as regras de localização. |
| `.valueOf()` | Retorna o valor numérico primitivo do objeto `Number`. |

Constantes importantes:

| Constante | Utilidade |
|---|---|
| `Number.MAX_VALUE` | Maior número finito representável. |
| `Number.MIN_VALUE` | Menor número positivo representável maior que zero. |
| `Number.MAX_SAFE_INTEGER` | Maior inteiro seguro. |
| `Number.MIN_SAFE_INTEGER` | Menor inteiro seguro. |
| `Number.POSITIVE_INFINITY` | Infinito positivo. |
| `Number.NEGATIVE_INFINITY` | Infinito negativo. |
| `Number.NaN` | Valor que representa um resultado numérico inválido. |
| `Number.EPSILON` | Distância entre `1` e o próximo número representável maior que `1`. |

## 4.2. Métodos de `Math`

`Math` é um objeto com métodos e constantes matemáticas. Não é uma classe que precise ser instanciada.

| Método | Utilidade |
|---|---|
| `Math.abs(x)` | Valor absoluto. |
| `Math.ceil(x)` | Arredonda para cima. |
| `Math.floor(x)` | Arredonda para baixo. |
| `Math.round(x)` | Arredonda para o inteiro mais próximo. |
| `Math.trunc(x)` | Remove a parte decimal. |
| `Math.max(...valores)` | Retorna o maior valor. |
| `Math.min(...valores)` | Retorna o menor valor. |
| `Math.random()` | Gera um número pseudoaleatório entre `0` (inclusive) e `1` (exclusivo). |
| `Math.sqrt(x)` | Raiz quadrada. |
| `Math.cbrt(x)` | Raiz cúbica. |
| `Math.pow(x, y)` | Potência de `x` elevado a `y`. |
| `Math.hypot(...valores)` | Calcula a raiz da soma dos quadrados dos argumentos. |
| `Math.sign(x)` | Indica o sinal do valor. |
| `Math.clz32(x)` | Conta os zeros à esquerda na representação binária de 32 bits. |
| `Math.imul(x, y)` | Multiplicação com resultado inteiro de 32 bits. |
| `Math.fround(x)` | Arredonda para a precisão de ponto flutuante de 32 bits. |
| `Math.log(x)` | Logaritmo natural. |
| `Math.log10(x)` | Logaritmo na base 10. |
| `Math.log2(x)` | Logaritmo na base 2. |
| `Math.exp(x)` | Calcula `e` elevado a `x`. |
| `Math.expm1(x)` | Calcula `e^x - 1` com maior precisão para valores próximos de zero. |
| `Math.log1p(x)` | Calcula `ln(1 + x)` com maior precisão para valores próximos de zero. |
| `Math.sin(x)` | Seno, em radianos. |
| `Math.cos(x)` | Cosseno, em radianos. |
| `Math.tan(x)` | Tangente, em radianos. |
| `Math.asin(x)` | Arco seno. |
| `Math.acos(x)` | Arco cosseno. |
| `Math.atan(x)` | Arco tangente. |
| `Math.atan2(y, x)` | Arco tangente considerando os sinais de `x` e `y`. |
| `Math.sinh(x)` | Seno hiperbólico. |
| `Math.cosh(x)` | Cosseno hiperbólico. |
| `Math.tanh(x)` | Tangente hiperbólica. |
| `Math.asinh(x)` | Arco seno hiperbólico. |
| `Math.acosh(x)` | Arco cosseno hiperbólico. |
| `Math.atanh(x)` | Arco tangente hiperbólica. |
| `Math.f16round(x)` | Arredonda para a precisão de ponto flutuante de 16 bits. |

Constantes matemáticas:

- `Math.PI` — número π.
- `Math.E` — número de Euler.
- `Math.LN2` — logaritmo natural de 2.
- `Math.LN10` — logaritmo natural de 10.
- `Math.LOG2E` — logaritmo de `e` na base 2.
- `Math.LOG10E` — logaritmo de `e` na base 10.
- `Math.SQRT2` — raiz quadrada de 2.
- `Math.SQRT1_2` — raiz quadrada de 1/2.

---

# 5. Datas — `Date`

O objeto `Date` representa um instante no tempo, normalmente em milissegundos desde 1º de janeiro de 1970, UTC.

```javascript
const agora = new Date();
```

## 5.1. Obtenção de informações

| Método | Utilidade |
|---|---|
| `.getTime()` | Obtém o timestamp em milissegundos. |
| `.getFullYear()` | Obtém o ano local. |
| `.getMonth()` | Obtém o mês local, de `0` a `11`. |
| `.getDate()` | Obtém o dia do mês local. |
| `.getDay()` | Obtém o dia da semana local, de `0` a `6`. |
| `.getHours()` | Obtém a hora local. |
| `.getMinutes()` | Obtém os minutos locais. |
| `.getSeconds()` | Obtém os segundos locais. |
| `.getMilliseconds()` | Obtém os milissegundos locais. |
| `.getTimezoneOffset()` | Obtém a diferença entre o horário local e UTC, em minutos, com sinal definido pela API. |
| `.getUTCFullYear()` | Obtém o ano em UTC. |
| `.getUTCMonth()` | Obtém o mês em UTC. |
| `.getUTCDate()` | Obtém o dia do mês em UTC. |
| `.getUTCDay()` | Obtém o dia da semana em UTC. |
| `.getUTCHours()` | Obtém a hora em UTC. |
| `.getUTCMinutes()` | Obtém os minutos em UTC. |
| `.getUTCSeconds()` | Obtém os segundos em UTC. |
| `.getUTCMilliseconds()` | Obtém os milissegundos em UTC. |

## 5.2. Alteração de datas

Existem métodos como `.setFullYear()`, `.setMonth()`, `.setDate()`, `.setHours()`, `.setMinutes()`, `.setSeconds()` e `.setMilliseconds()` para alterar componentes da data local.

Também existem versões UTC, como `.setUTCFullYear()` e `.setUTCMonth()`.

Outros métodos importantes:

| Método | Utilidade |
|---|---|
| `.setTime(timestamp)` | Define a data a partir de milissegundos desde a época Unix. |
| `.toISOString()` | Retorna uma string padronizada em UTC. |
| `.toJSON()` | Retorna a representação ISO utilizada na serialização JSON. |
| `.toDateString()` | Retorna uma representação textual da data local. |
| `.toTimeString()` | Retorna uma representação textual da hora local. |
| `.toLocaleDateString()` | Formata a data conforme a localização. |
| `.toLocaleTimeString()` | Formata a hora conforme a localização. |
| `.toLocaleString()` | Formata data e hora conforme a localização. |
| `.toUTCString()` | Retorna uma representação textual em UTC. |
| `.valueOf()` | Retorna o timestamp em milissegundos. |

Métodos estáticos:

- `Date.now()` — timestamp atual.
- `Date.parse(texto)` — tenta interpretar uma string como data.
- `Date.UTC(ano, mês, dia, ...)` — calcula um timestamp UTC a partir dos componentes fornecidos.

**Cuidado:** o mês começa em `0`, e não em `1`. Além disso, interpretar datas escritas em formatos não padronizados pode gerar resultados inconsistentes entre ambientes.

---

# 6. Map — `Map`

Um `Map` armazena pares de chave e valor. Diferentemente dos objetos comuns, aceita valores de qualquer tipo como chave.

```javascript
const usuarios = new Map();
```

| Método ou propriedade | Utilidade |
|---|---|
| `.set(chave, valor)` | Adiciona ou atualiza um par. |
| `.get(chave)` | Obtém o valor associado à chave. |
| `.has(chave)` | Verifica se a chave existe. |
| `.delete(chave)` | Remove um par pela chave. |
| `.clear()` | Remove todos os pares. |
| `.keys()` | Retorna um iterador de chaves. |
| `.values()` | Retorna um iterador de valores. |
| `.entries()` | Retorna um iterador de pares. |
| `.forEach(callback)` | Executa uma função para cada par. |
| `.size` | Informa a quantidade de pares. |

Exemplo:

```javascript
const usuario = new Map();

usuario.set("nome", "Ana");
usuario.set("idade", 20);

console.log(usuario.get("nome")); // Ana
console.log(usuario.has("idade")); // true
console.log(usuario.size); // 2
```

Métodos estáticos importantes:

- `Map.groupBy(iteravel, callback)` — agrupa elementos em um `Map` usando os resultados da função como chaves.

---

# 7. Set — `Set`

Um `Set` armazena valores únicos, sem duplicatas segundo as regras de igualdade utilizadas pela estrutura.

```javascript
const numeros = new Set([1, 2, 2, 3]);
```

| Método ou propriedade | Utilidade |
|---|---|
| `.add(valor)` | Adiciona um valor. |
| `.has(valor)` | Verifica se o valor existe. |
| `.delete(valor)` | Remove um valor. |
| `.clear()` | Remove todos os valores. |
| `.keys()` | Retorna um iterador dos valores. |
| `.values()` | Retorna um iterador dos valores. |
| `.entries()` | Retorna pares `[valor, valor]`. |
| `.forEach(callback)` | Executa uma função para cada valor. |
| `.size` | Retorna a quantidade de valores únicos. |

Exemplo:

```javascript
const numeros = new Set([1, 2, 2, 3]);

console.log(numeros.size); // 3

numeros.add(4);
numeros.delete(1);

console.log([...numeros]); // [2, 3, 4]
```

Operações de conjuntos disponíveis nas implementações modernas:

- `.union(outroSet)` — união.
- `.intersection(outroSet)` — interseção.
- `.difference(outroSet)` — diferença.
- `.symmetricDifference(outroSet)` — diferença simétrica.
- `.isSubsetOf(outroSet)` — verifica se é subconjunto.
- `.isSupersetOf(outroSet)` — verifica se é superconjunto.
- `.isDisjointFrom(outroSet)` — verifica se os conjuntos não possuem elementos em comum.

---

# 8. JSON — `JSON`

JSON é um formato de serialização de dados. `JSON` é um objeto com métodos estáticos.

| Método | Utilidade |
|---|---|
| `JSON.stringify(valor)` | Converte um valor compatível em uma string JSON. |
| `JSON.parse(texto)` | Converte uma string JSON válida em um valor JavaScript. |

Exemplo:

```javascript
const usuario = {
    nome: "Ana",
    idade: 20
};

const texto = JSON.stringify(usuario);
const objeto = JSON.parse(texto);

console.log(texto);
console.log(objeto.nome);
```

**Atenção:** JSON não preserva diretamente funções, símbolos ou a identidade de objetos. Algumas propriedades podem ser omitidas durante a serialização. `JSON.parse()` também lança erro se o texto não for JSON válido.

---

# 9. Expressões regulares — `RegExp`

Expressões regulares servem para procurar, validar e substituir padrões em textos.

```javascript
const padrao = /\d+/g;
```

| Método ou propriedade | Utilidade |
|---|---|
| `.test(texto)` | Verifica se existe correspondência. |
| `.exec(texto)` | Retorna informações sobre a próxima correspondência. |
| `.source` | Retorna o padrão textual da expressão. |
| `.flags` | Retorna as flags utilizadas. |
| `.global` | Indica se a flag `g` está ativa. |
| `.ignoreCase` | Indica se a flag `i` está ativa. |
| `.multiline` | Indica se a flag `m` está ativa. |
| `.dotAll` | Indica se a flag `s` está ativa. |
| `.unicode` | Indica se a flag `u` está ativa. |
| `.unicodeSets` | Indica se a flag `v` está ativa. |
| `.sticky` | Indica se a flag `y` está ativa. |
| `.lastIndex` | Indica a posição de início da próxima busca em expressões com estado. |

Exemplo:

```javascript
const padrao = /\d+/;

console.log(padrao.test("abc123")); // true
console.log(padrao.exec("abc123")[0]); // "123"
```

**Cuidado:** expressões com as flags `g` ou `y` podem alterar `lastIndex`. Repetir `.test()` ou `.exec()` na mesma expressão pode produzir resultados diferentes.

---

# 10. Promise — `Promise`

Uma `Promise` representa a conclusão ou falha futura de uma operação assíncrona.

```javascript
const promessa = new Promise((resolve, reject) => {
    resolve("Concluído");
});
```

## Métodos de instância

| Método | Utilidade |
|---|---|
| `.then(callback)` | Executa uma função quando a promessa é resolvida e permite encadear operações. |
| `.catch(callback)` | Trata rejeições. |
| `.finally(callback)` | Executa uma função ao terminar, independentemente de sucesso ou falha. |

## Métodos estáticos

| Método | Utilidade |
|---|---|
| `Promise.resolve(valor)` | Cria uma promessa resolvida com o valor fornecido. |
| `Promise.reject(erro)` | Cria uma promessa rejeitada. |
| `Promise.all(iteravel)` | Aguarda todas as promessas; rejeita se alguma falhar. |
| `Promise.allSettled(iteravel)` | Aguarda todas e informa o resultado individual de cada uma. |
| `Promise.race(iteravel)` | Assume o resultado da primeira promessa que se estabelecer. |
| `Promise.any(iteravel)` | Assume o resultado da primeira promessa cumprida; rejeita se todas forem rejeitadas. |
| `Promise.withResolvers()` | Retorna uma promessa e suas funções `resolve` e `reject`. |

Exemplo:

```javascript
Promise.resolve("Olá")
    .then(valor => console.log(valor))
    .catch(erro => console.error(erro))
    .finally(() => console.log("Finalizado"));
```

---

# 11. Funções — `Function`

Funções são objetos que podem executar código.

| Método | Utilidade |
|---|---|
| `.call(thisArg, ...argumentos)` | Executa a função com um `this` especificado e argumentos individuais. |
| `.apply(thisArg, argumentos)` | Executa a função com um `this` especificado e argumentos fornecidos em um array ou iterável compatível. |
| `.bind(thisArg, ...argumentos)` | Retorna uma nova função com o `this` e, opcionalmente, argumentos previamente definidos. |
| `.toString()` | Retorna uma representação textual da função. |

Exemplo:

```javascript
function somar(a, b) {
    return a + b;
}

console.log(somar.call(null, 2, 3)); // 5
console.log(somar.apply(null, [2, 3])); // 5

const somarDez = somar.bind(null, 10);

console.log(somarDez(5)); // 15
```

---

# 12. Boolean — `Boolean`

Representa valores lógicos: `true` e `false`.

| Método ou recurso | Utilidade |
|---|---|
| `Boolean(valor)` | Converte um valor em booleano. |
| `!!valor` | Outra forma de converter um valor em booleano. |
| `.valueOf()` | Retorna o valor primitivo de um objeto `Boolean`. |
| `.toString()` | Retorna `"true"` ou `"false"`. |

Exemplo:

```javascript
Boolean("");      // false
Boolean("Olá");   // true
Boolean(0);       // false
Boolean(10);      // true
```

**Atenção:** `new Boolean(false)` cria um objeto que é verdadeiro em contextos booleanos. Prefira `Boolean(valor)` ou `!!valor`.

---

# 13. Símbolos — `Symbol`

Símbolos são valores primitivos únicos, úteis para criar chaves sem colisões acidentais.

| Método ou propriedade | Utilidade |
|---|---|
| `Symbol(descricao)` | Cria um símbolo único. |
| `Symbol.for(chave)` | Obtém ou registra um símbolo em um registro global. |
| `Symbol.keyFor(simbolo)` | Obtém a chave global de um símbolo registrado com `Symbol.for()`. |
| `.description` | Retorna a descrição do símbolo. |
| `.toString()` | Retorna uma representação textual do símbolo. |
| `.valueOf()` | Retorna o símbolo primitivo de um objeto `Symbol`. |

Símbolos especiais:

- `Symbol.iterator` — define o iterador de um objeto.
- `Symbol.asyncIterator` — define o iterador assíncrono.
- `Symbol.toPrimitive` — personaliza a conversão para um valor primitivo.
- `Symbol.toStringTag` — personaliza a identificação textual de um objeto.
- `Symbol.hasInstance` — personaliza o comportamento de `instanceof`.
- `Symbol.isConcatSpreadable` — influencia o comportamento de `concat()`.
- `Symbol.match` — personaliza o comportamento de correspondência.
- `Symbol.replace` — personaliza substituições.
- `Symbol.search` — personaliza buscas.
- `Symbol.split` — personaliza divisões.
- `Symbol.species` — influencia a construção de objetos derivados em algumas operações.
- `Symbol.unscopables` — controla quais propriedades são excluídas do ambiente léxico de `with`.

---

# 14. Iteradores — `Iterator`

Iteradores permitem percorrer sequências de valores.

| Método ou propriedade | Utilidade |
|---|---|
| `.next()` | Retorna o próximo resultado, geralmente com `value` e `done`. |
| `.return()` | Permite encerrar a iteração antecipadamente, quando implementado. |
| `.throw(erro)` | Permite lançar um erro no iterador, quando implementado. |
| `[Symbol.iterator]()` | Retorna um iterador síncrono, quando implementado. |
| `[Symbol.asyncIterator]()` | Retorna um iterador assíncrono, quando implementado. |

Recursos de iteradores modernos incluem:

- `.map(callback)` — transforma os valores.
- `.filter(callback)` — filtra os valores.
- `.take(quantidade)` — limita a quantidade de valores.
- `.drop(quantidade)` — ignora os primeiros valores.
- `.flatMap(callback)` — transforma e achata um nível.
- `.reduce(callback, inicial)` — reduz os valores a um resultado.
- `.toArray()` — materializa os valores em um array.
- `.forEach(callback)` — executa uma função para cada valor.

**Compatibilidade:** os métodos modernos de iteradores dependem da versão do ambiente JavaScript. Para compatibilidade ampla, verifique o suporte antes de utilizá-los.

---

# 15. Typed Arrays — Arrays tipados

Arrays tipados armazenam dados numéricos em estruturas de memória com tipos específicos.

Principais tipos:

- `Int8Array`
- `Uint8Array`
- `Uint8ClampedArray`
- `Int16Array`
- `Uint16Array`
- `Int32Array`
- `Uint32Array`
- `Float16Array`
- `Float32Array`
- `Float64Array`
- `BigInt64Array`
- `BigUint64Array`

Métodos comuns:

| Método ou propriedade | Utilidade |
|---|---|
| `.length` | Quantidade de elementos. |
| `.byteLength` | Quantidade de bytes utilizados pelos elementos. |
| `.byteOffset` | Deslocamento em bytes dentro do buffer. |
| `.buffer` | Buffer de memória subjacente. |
| `.at(indice)` | Obtém um elemento pelo índice. |
| `.set(array, deslocamento)` | Copia valores para a estrutura. |
| `.subarray(inicio, fim)` | Cria uma visualização de uma parte da mesma memória. |
| `.slice(inicio, fim)` | Cria uma cópia de parte dos elementos. |
| `.fill(valor)` | Preenche posições com um valor. |
| `.reverse()` | Inverte os elementos. |
| `.sort(callback)` | Ordena os elementos. |
| `.map(callback)` | Produz outro array tipado com os resultados. |
| `.filter(callback)` | Produz um array tipado filtrado. |
| `.reduce(callback)` | Reduz os valores a um resultado. |
| `.includes(valor)` | Verifica se contém um valor. |
| `.indexOf(valor)` | Localiza a primeira ocorrência. |
| `.join(separador)` | Converte os elementos em string. |

Essas estruturas são úteis para processamento numérico, gráficos, áudio, imagens e manipulação binária.

---

# 16. BigInt — Inteiros grandes

`BigInt` representa inteiros com precisão arbitrária, limitados pela memória disponível.

```javascript
const numero = 12345678901234567890n;
```

| Método ou propriedade | Utilidade |
|---|---|
| `BigInt(valor)` | Converte um valor compatível em `BigInt`. |
| `.toString(base)` | Converte para string, opcionalmente em outra base. |
| `.toLocaleString(local)` | Formata o inteiro conforme a localização. |
| `.valueOf()` | Retorna o valor primitivo de um objeto `BigInt`. |

**Limitação:** não é possível misturar diretamente `BigInt` e `Number` em operações aritméticas comuns. Converta os tipos conscientemente.

---

# 17. Intl — Internacionalização

O objeto `Intl` fornece recursos de formatação e comparação linguística.

## Classes principais

| Recurso | Utilidade |
|---|---|
| `Intl.NumberFormat` | Formata números, moedas e percentuais. |
| `Intl.DateTimeFormat` | Formata datas e horários. |
| `Intl.Collator` | Compara e ordena textos segundo regras linguísticas. |
| `Intl.PluralRules` | Determina regras de pluralização de um idioma. |
| `Intl.RelativeTimeFormat` | Formata tempos relativos, como "há 2 dias". |
| `Intl.ListFormat` | Formata listas conforme o idioma. |
| `Intl.DisplayNames` | Obtém nomes localizados de idiomas, regiões e outros códigos. |
| `Intl.Segmenter` | Segmenta textos em unidades linguísticas, como palavras e grafemas. |
| `Intl.Locale` | Representa e manipula identificadores de localização. |

Exemplo:

```javascript
const moeda = new Intl.NumberFormat("pt-BR", {
    style: "currency",
    currency: "BRL"
});

console.log(moeda.format(1234.56));
// Exemplo de saída: R$ 1.234,56
```

---

# 18. Manipulação do DOM — Document Object Model

O DOM permite acessar e alterar a estrutura HTML de uma página.

## 18.1. Seleção de elementos

| Método | Utilidade |
|---|---|
| `document.getElementById(id)` | Obtém um elemento pelo ID. |
| `document.getElementsByClassName(classe)` | Obtém uma coleção de elementos por classe. |
| `document.getElementsByTagName(tag)` | Obtém uma coleção de elementos pela tag. |
| `document.querySelector(seletor)` | Obtém o primeiro elemento correspondente ao seletor CSS. |
| `document.querySelectorAll(seletor)` | Obtém uma `NodeList` estática dos elementos correspondentes. |

## 18.2. Conteúdo e atributos

| Propriedade ou método | Utilidade |
|---|---|
| `.textContent` | Lê ou altera o texto de um nó e de seus descendentes. |
| `.innerText` | Lê ou altera o texto renderizado, considerando aspectos de apresentação. |
| `.innerHTML` | Lê ou altera o HTML interno. |
| `.outerHTML` | Lê ou substitui a representação HTML do próprio elemento e seus descendentes. |
| `.value` | Lê ou altera o valor de campos de formulário compatíveis. |
| `.getAttribute(nome)` | Obtém o valor de um atributo. |
| `.setAttribute(nome, valor)` | Define um atributo. |
| `.removeAttribute(nome)` | Remove um atributo. |
| `.hasAttribute(nome)` | Verifica se o atributo existe. |
| `.toggleAttribute(nome)` | Alterna a presença de um atributo. |
| `.matches(seletor)` | Verifica se o elemento corresponde a um seletor CSS. |
| `.closest(seletor)` | Procura o ancestral mais próximo que corresponda ao seletor. |

## 18.3. Inserção e remoção

| Método | Utilidade |
|---|---|
| `document.createElement(tag)` | Cria um elemento HTML. |
| `document.createTextNode(texto)` | Cria um nó de texto. |
| `.append(...itens)` | Insere nós ou texto ao final do elemento. |
| `.prepend(...itens)` | Insere nós ou texto no início. |
| `.before(...itens)` | Insere conteúdo antes do elemento. |
| `.after(...itens)` | Insere conteúdo depois do elemento. |
| `.replaceWith(...itens)` | Substitui o elemento por outros nós ou texto. |
| `.remove()` | Remove o elemento do DOM. |
| `.replaceChildren(...itens)` | Substitui todos os filhos. |
| `.cloneNode(profundo)` | Clona o nó, opcionalmente incluindo descendentes. |
| `.insertAdjacentHTML(posicao, html)` | Insere HTML em uma posição relativa ao elemento. |
| `.insertAdjacentText(posicao, texto)` | Insere texto em uma posição relativa ao elemento. |
| `.insertAdjacentElement(posicao, elemento)` | Insere um elemento em uma posição relativa ao elemento atual. |

## 18.4. Classes e CSS

| Método ou propriedade | Utilidade |
|---|---|
| `.classList.add(classe)` | Adiciona classes CSS. |
| `.classList.remove(classe)` | Remove classes CSS. |
| `.classList.toggle(classe)` | Alterna a presença de uma classe. |
| `.classList.contains(classe)` | Verifica se uma classe existe. |
| `.classList.replace(antiga, nova)` | Substitui uma classe por outra. |
| `.style.propriedade` | Lê ou altera estilos inline. |
| `getComputedStyle(elemento)` | Obtém os estilos calculados do elemento. |

## 18.5. Eventos

| Método | Utilidade |
|---|---|
| `.addEventListener(evento, callback)` | Registra um ouvinte de evento. |
| `.removeEventListener(evento, callback)` | Remove um ouvinte previamente registrado com os mesmos parâmetros relevantes. |
| `.dispatchEvent(evento)` | Despacha um evento no elemento. |
| `.preventDefault()` | Impede o comportamento padrão de um evento, quando cancelável. |
| `.stopPropagation()` | Impede que o evento continue se propagando. |
| `.stopImmediatePropagation()` | Impede a propagação e a execução de outros ouvintes posteriores no mesmo alvo. |

**Segurança:** evite inserir conteúdo não confiável com `.innerHTML`. Para inserir texto comum, prefira `.textContent`.

---

# 19. Web APIs importantes

Os recursos desta seção não são todos métodos de objetos nativos da linguagem ECMAScript. São APIs fornecidas principalmente pelos navegadores.

## 19.1. Fetch — requisições HTTP

| Método ou recurso | Utilidade |
|---|---|
| `fetch(url, opcoes)` | Realiza uma requisição HTTP. |
| `response.json()` | Lê o corpo da resposta como JSON. |
| `response.text()` | Lê o corpo como texto. |
| `response.blob()` | Lê o corpo como `Blob`. |
| `response.arrayBuffer()` | Lê o corpo como `ArrayBuffer`. |
| `response.formData()` | Lê o corpo como `FormData`. |
| `response.clone()` | Cria uma cópia da resposta para leitura independente. |

**Atenção:** `fetch()` não rejeita automaticamente a promessa para respostas HTTP como `404` ou `500`. Verifique `response.ok`.

## 19.2. Armazenamento no navegador

### `localStorage` e `sessionStorage`

| Método | Utilidade |
|---|---|
| `.setItem(chave, valor)` | Armazena um valor textual. |
| `.getItem(chave)` | Obtém um valor armazenado ou `null`. |
| `.removeItem(chave)` | Remove um item. |
| `.clear()` | Limpa todos os itens daquela área de armazenamento. |
| `.key(indice)` | Obtém a chave de uma posição. |
| `.length` | Quantidade de itens armazenados. |

Os valores são armazenados como strings. Para guardar objetos, utilize `JSON.stringify()` e `JSON.parse()`.

## 19.3. Temporizadores

| Método | Utilidade |
|---|---|
| `setTimeout(callback, tempo)` | Agenda uma execução após um atraso mínimo. |
| `clearTimeout(id)` | Cancela um temporizador pendente. |
| `setInterval(callback, tempo)` | Agenda execuções repetidas. |
| `clearInterval(id)` | Cancela uma execução repetitiva. |
| `requestAnimationFrame(callback)` | Agenda uma função para a próxima oportunidade de renderização. |
| `cancelAnimationFrame(id)` | Cancela uma solicitação de animação. |

Os tempos são normalmente expressos em milissegundos, mas não representam garantias de execução exata.

## 19.4. URL e parâmetros

| Método ou propriedade | Utilidade |
|---|---|
| `new URL(endereco)` | Cria um objeto que representa uma URL. |
| `new URLSearchParams(texto)` | Cria um objeto para manipular parâmetros de consulta. |
| `.searchParams.get(chave)` | Obtém um parâmetro da URL. |
| `.searchParams.set(chave, valor)` | Define ou substitui um parâmetro. |
| `.searchParams.append(chave, valor)` | Adiciona outro valor para um parâmetro. |
| `.searchParams.delete(chave)` | Remove parâmetros. |
| `.searchParams.has(chave)` | Verifica se o parâmetro existe. |
| `.searchParams.toString()` | Serializa os parâmetros. |

## 19.5. Clipboard

| Método | Utilidade |
|---|---|
| `navigator.clipboard.readText()` | Lê texto da área de transferência, quando permitido. |
| `navigator.clipboard.writeText(texto)` | Copia texto para a área de transferência, quando permitido. |

O acesso depende de permissões, contexto seguro e regras do navegador.

---

# 20. Operações comuns e alternativas úteis

| Objetivo | Recurso recomendado |
|---|---|
| Verificar se uma string está vazia ou contém apenas espaços | `texto.trim() === ""` |
| Verificar se um array contém um elemento | `array.includes(valor)` |
| Encontrar um elemento em um array | `array.find(callback)` |
| Encontrar a posição de um elemento | `array.findIndex(callback)` |
| Filtrar dados | `array.filter(callback)` |
| Transformar todos os elementos | `array.map(callback)` |
| Somar valores | `array.reduce((total, valor) => total + valor, 0)` |
| Verificar se todos os elementos atendem a uma condição | `array.every(callback)` |
| Verificar se pelo menos um elemento atende a uma condição | `array.some(callback)` |
| Converter uma string em array | `texto.split(separador)` |
| Converter um array em string | `array.join(separador)` |
| Copiar um array superficialmente | `[...array]` ou `array.slice()` |
| Remover duplicatas de valores primitivos | `[...new Set(array)]` |
| Obter chaves de um objeto | `Object.keys(objeto)` |
| Obter valores de um objeto | `Object.values(objeto)` |
| Obter pares de um objeto | `Object.entries(objeto)` |
| Verificar se uma variável é um array | `Array.isArray(valor)` |
| Verificar se um valor é `null` ou `undefined` | `valor == null` |
| Verificar se um valor é exatamente `null` | `valor === null` |
| Verificar se uma propriedade própria existe | `Object.hasOwn(objeto, chave)` |
| Converter um valor em string | `String(valor)` |
| Converter um valor em número | `Number(valor)` |
| Converter um valor em booleano | `Boolean(valor)` |
| Ordenar números em ordem crescente | `array.sort((a, b) => a - b)` |
| Copiar e ordenar números sem alterar o array original | `array.toSorted((a, b) => a - b)` |

---

# 21. Cuidados importantes

1. **Métodos mutáveis e imutáveis:** `push()`, `splice()`, `sort()` e `reverse()` modificam o array original. `map()`, `filter()` e `slice()` produzem novos arrays.

2. **Strings são imutáveis:** `replace()`, `trim()` e `toUpperCase()` retornam novas strings.

3. **`==` e `===`:** o operador `===` evita coerções de tipo e costuma ser a escolha mais previsível.

4. **`typeof null`:** retorna `"object"` por uma particularidade histórica da linguagem.

5. **Arrays não são objetos simples:** `typeof []` retorna `"object"`. Para identificar arrays, utilize `Array.isArray()`.

6. **Valores ausentes:** acessar uma propriedade inexistente normalmente retorna `undefined`. Acessar uma propriedade de `null` ou `undefined` diretamente causa um erro.

7. **Cópias superficiais:** `[...array]`, `slice()` e `Object.assign()` não copiam recursivamente objetos internos.

8. **Compatibilidade:** nem todos os métodos mais recentes estão disponíveis em todos os navegadores ou versões do Node.js.

9. **DOM e ECMAScript:** `document`, `window`, `fetch()` e `localStorage` pertencem às APIs do ambiente, não ao núcleo da linguagem ECMAScript.

10. **Segurança:** não confie em dados recebidos do usuário ou de serviços externos. Valide-os antes de utilizá-los em operações sensíveis.

---

# 22. Documentação oficial

Para consultar assinaturas, exemplos, compatibilidade e especificações atualizadas:

- [MDN Web Docs — JavaScript](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript)
- [MDN — Referência de JavaScript](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference)
- [MDN — Referência do DOM](https://developer.mozilla.org/pt-BR/docs/Web/API/Document_Object_Model)
- [ECMAScript — especificação oficial](https://tc39.es/ecma262/)
- [Node.js — documentação oficial](https://nodejs.org/docs/latest/api/)

**Sugestão de estudo:** comece por `String`, `Array`, `Object`, `Math`, funções e DOM. Em seguida, avance para `Map`, `Set`, `Promise`, JSON e APIs do navegador. Essa sequência oferece uma base prática para construir interfaces e aplicações em JavaScript.