# JavaScript — Do Básico ao Intermediário

> Guia prático para quem já possui conhecimentos de programação, especialmente C#.

---

# Sumário

1. [O que é JavaScript](#1-o-que-é-javascript)
2. [Executando JavaScript](#2-executando-javascript)
3. [Sintaxe básica](#3-sintaxe-básica)
4. [Variáveis](#4-variáveis)
5. [Tipos](#5-tipos)
6. [Strings](#6-strings)
7. [Operadores](#7-operadores)
8. [Conversão de tipos](#8-conversão-de-tipos)
9. [Condicionais](#9-condicionais)
10. [Loops](#10-loops)
11. [Funções](#11-funções)
12. [Arrow Functions](#12-arrow-functions)
13. [Escopo](#13-escopo)
14. [Closures](#14-closures)
15. [Arrays](#15-arrays)
16. [Objetos](#16-objetos)
17. [Destructuring](#17-destructuring)
18. [Spread e Rest](#18-spread-e-rest)
19. [Optional Chaining e Nullish Coalescing](#19-optional-chaining-e-nullish-coalescing)
20. [Métodos importantes de Arrays](#20-métodos-importantes-de-arrays)
21. [Classes](#21-classes)
22. [Herança](#22-herança)
23. [Static](#23-static)
24. [Getters e Setters](#24-getters-e-setters)
25. [Campos privados](#25-campos-privados)
26. [Métodos assíncronos](#26-métodos-assíncronos)
27. [Generators](#27-generators)
28. [Erros e exceções](#28-erros-e-exceções)
29. [Módulos](#29-módulos)
30. [JSON](#30-json)
31. [Promises](#31-promises)
32. [Async/Await](#32-asyncawait)
33. [Fetch e APIs](#33-fetch-e-apis)
34. [Map e Set](#34-map-e-set)
35. [Iterables e Iterators](#35-iterables-e-iterators)
36. [Regex](#36-regex)
37. [Date](#37-date)
38. [Programação funcional](#38-programação-funcional)
39. [Protótipos](#39-protótipos)
40. [Event Loop](#40-event-loop)
41. [Diferenças importantes para C#](#41-diferenças-importantes-para-c)
42. [Boas práticas](#42-boas-práticas)
43. [Checklist](#43-checklist)

---

# 1. O que é JavaScript

JavaScript é uma linguagem dinâmica, baseada em protótipos e multiparadigma.

Ela pode ser utilizada em:

* navegadores;
* servidores;
* aplicações desktop;
* ferramentas de linha de comando;
* aplicações mobile;
* jogos;
* automações;
* ferramentas de desenvolvimento.

O padrão da linguagem é chamado **ECMAScript**.

JavaScript não é Java.

Também é importante entender que JavaScript não é apenas "linguagem de navegador". O navegador fornece APIs como:

```js
document
window
fetch
localStorage
```

Enquanto ambientes como Node.js fornecem APIs próprias para servidor e sistema operacional.

---

# 2. Executando JavaScript

## No navegador

Pode-se executar:

```html
<script>
    console.log("Olá!");
</script>
```

Ou:

```html
<script src="script.js"></script>
```

## Node.js

Com um arquivo:

```js
console.log("Olá!");
```

Execute:

```bash
node script.js
```

---

# 3. Sintaxe básica

Comentários:

```js
// Comentário de uma linha

/*
   Comentário
   de várias linhas
*/
```

Ponto e vírgula:

```js
const x = 10;
const y = 20;
```

JavaScript possui Automatic Semicolon Insertion (ASI), então isto também pode funcionar:

```js
const x = 10
const y = 20
```

Mesmo assim, escolha um padrão e seja consistente.

---

# 4. Variáveis

Existem três formas históricas:

```js
var
let
const
```

## const

Use quando a variável não será reatribuída:

```js
const nome = "Willian";
```

Isto não pode:

```js
const nome = "Willian";
nome = "João";
```

Porém:

```js
const pessoa = {
    nome: "Willian"
};

pessoa.nome = "João";
```

funciona.

O `const` impede a reatribuição da referência, não torna automaticamente o objeto imutável.

---

## let

Permite reatribuição:

```js
let idade = 18;

idade = 19;
```

---

## var

Existe por compatibilidade com JavaScript antigo:

```js
var idade = 18;
```

Em código moderno, normalmente prefira:

```js
const
```

ou:

```js
let
```

---

# 5. Tipos

JavaScript possui tipos primitivos e objetos.

## String

```js
const nome = "Willian";
```

## Number

JavaScript usa `number` para números inteiros e de ponto flutuante:

```js
const idade = 20;
const altura = 1.80;
```

Diferente do C#:

```csharp
int
double
float
decimal
```

JavaScript normalmente usa:

```js
number
```

Existe também:

```js
bigint
```

para inteiros muito grandes.

---

## Boolean

```js
const ativo = true;
const administrador = false;
```

---

## undefined

Representa ausência de valor atribuído:

```js
let valor;

console.log(valor); // undefined
```

---

## null

Representa ausência intencional de valor:

```js
const usuario = null;
```

---

## bigint

```js
const numeroGrande = 123456789012345678901234567890n;
```

Observe o `n`.

---

## symbol

Usado para criar identificadores únicos:

```js
const id = Symbol("id");
```

---

## object

Objetos:

```js
const pessoa = {
    nome: "Willian",
    idade: 20
};
```

Arrays também são objetos:

```js
const numeros = [1, 2, 3];
```

---

# 6. Strings

JavaScript possui:

```js
"Olá"
'Olá'
`Olá`
```

As duas primeiras são strings normais.

A terceira é um **template literal**.

## Equivalente ao `$"..."` do C#

C#:

```csharp
string nome = "Willian";

Console.WriteLine($"Olá, {nome}!");
```

JavaScript:

```js
const nome = "Willian";

console.log(`Olá, ${nome}!`);
```

Essa é uma das diferenças mais importantes para quem vem de C#.

---

## Expressões dentro da string

```js
const a = 10;
const b = 20;

console.log(`Resultado: ${a + b}`);
```

Também:

```js
const usuario = {
    nome: "Willian",
    idade: 20
};

console.log(`Nome: ${usuario.nome}`);
```

---

## Strings multilinha

```js
const texto = `
    Primeira linha
    Segunda linha
    Terceira linha
`;
```

---

## Métodos importantes

```js
const texto = "Olá mundo";

texto.length;
texto.toUpperCase();
texto.toLowerCase();
texto.includes("mundo");
texto.startsWith("Olá");
texto.endsWith("mundo");
texto.indexOf("mundo");
texto.slice(0, 3);
texto.replace("mundo", "JavaScript");
texto.trim();
texto.split(" ");
```

---

# 7. Operadores

## Aritméticos

```js
+
-
*
/
%
**
```

Exemplo:

```js
const soma = 10 + 5;
const resto = 10 % 3;
const potencia = 2 ** 3;
```

---

## Comparação

```js
>
<
>=
<=
==
===
!=
!==
```

Prefira:

```js
===
```

em vez de:

```js
==
```

E:

```js
!==
```

em vez de:

```js
!=
```

Exemplo:

```js
10 === 10; // true
10 === "10"; // false
```

Já:

```js
10 == "10"; // true
```

porque `==` permite coerção de tipos.

---

## Lógicos

```js
&&
||
!
```

Exemplo:

```js
if (idade >= 18 && ativo) {
    console.log("Permitido");
}
```

---

## Nullish

```js
??
```

Exemplo:

```js
const nome = null;

const resultado = nome ?? "Desconhecido";
```

Resultado:

```text
Desconhecido
```

Diferença importante:

```js
const valor = 0;

console.log(valor || 10); // 10
console.log(valor ?? 10); // 0
```

`||` considera vários valores falsy.

`??` só considera:

```js
null
undefined
```

---

## Atribuição

```js
=
+=
-=
*=
/=
%=

??=
||=
&&=
```

Exemplo:

```js
let idade = 20;

idade += 1;
```

---

# 8. Conversão de tipos

JavaScript permite conversões.

```js
const numero = Number("123");
```

Resultado:

```js
123
```

String:

```js
const texto = String(123);
```

Boolean:

```js
Boolean(1); // true
Boolean(0); // false
```

---

## Falsy

Valores considerados falsy incluem:

```js
false
0
-0
0n
""
null
undefined
NaN
```

Exemplo:

```js
if ("") {
    console.log("Executou");
}
```

Não executará.

---

# 9. Condicionais

## if

```js
if (idade >= 18) {
    console.log("Maior de idade");
}
```

## else

```js
if (idade >= 18) {
    console.log("Maior");
} else {
    console.log("Menor");
}
```

## else if

```js
if (idade >= 18) {
    console.log("Maior");
} else if (idade >= 13) {
    console.log("Adolescente");
} else {
    console.log("Criança");
}
```

---

## Operador ternário

C#:

```csharp
string resultado = idade >= 18 ? "Maior" : "Menor";
```

JavaScript:

```js
const resultado = idade >= 18 ? "Maior" : "Menor";
```

---

## switch

```js
switch (opcao) {
    case 1:
        console.log("Novo");
        break;

    case 2:
        console.log("Editar");
        break;

    default:
        console.log("Desconhecido");
        break;
}
```

---

# 10. Loops

## for

```js
for (let i = 0; i < 10; i++) {
    console.log(i);
}
```

---

## while

```js
while (condicao) {
    // código
}
```

---

## do while

```js
do {
    // código
} while (condicao);
```

---

## for...of

Percorre valores:

```js
const numeros = [10, 20, 30];

for (const numero of numeros) {
    console.log(numero);
}
```

---

## for...in

Percorre propriedades/chaves:

```js
const pessoa = {
    nome: "Willian",
    idade: 20
};

for (const chave in pessoa) {
    console.log(chave);
}
```

Não confunda:

```js
for...of
```

com:

```js
for...in
```

---

# 11. Funções

Forma tradicional:

```js
function somar(a, b) {
    return a + b;
}
```

Uso:

```js
const resultado = somar(10, 20);
```

---

## Parâmetro padrão

```js
function saudar(nome = "desconhecido") {
    console.log(`Olá, ${nome}`);
}
```

---

## Retorno

```js
function quadrado(numero) {
    return numero * numero;
}
```

---

## Função sem retorno

```js
function mostrarMensagem() {
    console.log("Olá");
}
```

Se não houver `return`, o resultado será:

```js
undefined
```

---

# 12. Arrow Functions

Forma curta:

```js
const somar = (a, b) => {
    return a + b;
};
```

Pode ser reduzida:

```js
const somar = (a, b) => a + b;
```

Um parâmetro:

```js
const dobrar = x => x * 2;
```

Nenhum:

```js
const executar = () => {
    console.log("Executando");
};
```

---

## Arrow function e `this`

Uma diferença extremamente importante:

Arrow functions não possuem seu próprio `this`.

```js
const pessoa = {
    nome: "Willian",

    falar() {
        console.log(this.nome);
    }
};
```

Aqui:

```js
this
```

é determinado pelo modo como o método é chamado.

Arrow functions capturam o `this` do contexto externo.

---

# 13. Escopo

JavaScript possui escopo:

* global;
* de função;
* de bloco.

`let` e `const` possuem escopo de bloco.

```js
if (true) {
    let x = 10;
}

console.log(x);
```

Isso gera erro.

---

# 14. Closures

Closure é quando uma função mantém acesso ao ambiente onde foi criada.

```js
function criarContador() {
    let contador = 0;

    return function () {
        contador++;

        return contador;
    };
}
```

Uso:

```js
const contador = criarContador();

console.log(contador()); // 1
console.log(contador()); // 2
console.log(contador()); // 3
```

A variável:

```js
contador
```

continua existindo mesmo depois que `criarContador()` terminou.

Closures são muito importantes em JavaScript.

---

# 15. Arrays

Criando:

```js
const numeros = [1, 2, 3, 4];
```

Acessando:

```js
console.log(numeros[0]);
```

Índices começam em `0`.

---

## Adicionar

Final:

```js
numeros.push(5);
```

Início:

```js
numeros.unshift(0);
```

---

## Remover

Final:

```js
numeros.pop();
```

Início:

```js
numeros.shift();
```

---

## Tamanho

```js
numeros.length;
```

---

## Verificar existência

```js
numeros.includes(10);
```

---

# 16. Objetos

Objeto:

```js
const pessoa = {
    nome: "Willian",
    idade: 20,
    ativo: true
};
```

Acesso:

```js
pessoa.nome;
```

Ou:

```js
pessoa["nome"];
```

---

## Adicionando propriedade

```js
pessoa.email = "teste@email.com";
```

---

## Removendo

```js
delete pessoa.email;
```

---

## Métodos

```js
const pessoa = {
    nome: "Willian",

    falar() {
        console.log(`Olá, sou ${this.nome}`);
    }
};
```

---

# 17. Destructuring

Permite extrair valores.

```js
const pessoa = {
    nome: "Willian",
    idade: 20
};

const { nome, idade } = pessoa;
```

Agora:

```js
console.log(nome);
console.log(idade);
```

---

## Arrays

```js
const numeros = [10, 20, 30];

const [a, b, c] = numeros;
```

---

## Renomeando

```js
const { nome: nomeUsuario } = pessoa;
```

---

# 18. Spread e Rest

## Spread

Espalha valores.

```js
const a = [1, 2, 3];

const b = [...a, 4, 5];
```

Resultado:

```js
[1, 2, 3, 4, 5]
```

Objetos:

```js
const pessoa2 = {
    ...pessoa,
    idade: 21
};
```

---

## Rest

Agrupa valores.

```js
function somar(...numeros) {
    return numeros.reduce((total, numero) => total + numero, 0);
}
```

Uso:

```js
somar(1, 2, 3, 4);
```

---

# 19. Optional Chaining e Nullish Coalescing

## Optional chaining

```js
const cidade = pessoa?.endereco?.cidade;
```

Se alguma propriedade intermediária for `null` ou `undefined`, o resultado será `undefined`.

---

## Função opcional

```js
objeto.metodo?.();
```

---

## Nullish

```js
const nome = pessoa.nome ?? "Sem nome";
```

---

# 20. Métodos importantes de Arrays

Esta é uma das áreas mais importantes para quem vem de LINQ.

## map

Transforma cada elemento.

```js
const numeros = [1, 2, 3];

const dobrados = numeros.map(x => x * 2);
```

Resultado:

```js
[2, 4, 6]
```

C#:

```csharp
numeros.Select(x => x * 2)
```

---

## filter

```js
const pares = numeros.filter(x => x % 2 === 0);
```

C#:

```csharp
numeros.Where(x => x % 2 == 0)
```

---

## find

```js
const usuario = usuarios.find(x => x.id === 10);
```

---

## some

```js
const existe = numeros.some(x => x > 10);
```

---

## every

```js
const todosPositivos = numeros.every(x => x > 0);
```

---

## reduce

Muito importante.

```js
const soma = numeros.reduce(
    (total, numero) => total + numero,
    0
);
```

Pode representar várias operações semelhantes a agregações do LINQ.

---

## forEach

```js
numeros.forEach(numero => {
    console.log(numero);
});
```

---

# 21. Classes

JavaScript possui classes modernas.

```js
class Pessoa {
    constructor(nome, idade) {
        this.nome = nome;
        this.idade = idade;
    }

    apresentar() {
        console.log(`Meu nome é ${this.nome}`);
    }
}
```

Instanciando:

```js
const pessoa = new Pessoa("Willian", 20);
```

---

# 22. Herança

```js
class Animal {
    falar() {
        console.log("Som");
    }
}

class Cachorro extends Animal {
    falar() {
        console.log("Au au");
    }
}
```

Uso:

```js
const cachorro = new Cachorro();

cachorro.falar();
```

---

## super

```js
class Animal {
    constructor(nome) {
        this.nome = nome;
    }
}

class Cachorro extends Animal {
    constructor(nome, raca) {
        super(nome);

        this.raca = raca;
    }
}
```

---

# 23. Static

Método estático pertence à classe, não à instância.

```js
class Matematica {
    static somar(a, b) {
        return a + b;
    }
}
```

Uso:

```js
Matematica.somar(10, 20);
```

Não:

```js
const m = new Matematica();

m.somar(10, 20);
```

---

# 24. Getters e Setters

```js
class Pessoa {
    constructor(nome) {
        this._nome = nome;
    }

    get nome() {
        return this._nome;
    }

    set nome(valor) {
        this._nome = valor;
    }
}
```

Uso:

```js
const pessoa = new Pessoa("Willian");

console.log(pessoa.nome);

pessoa.nome = "João";
```

Observe que você usa:

```js
pessoa.nome
```

e não:

```js
pessoa.nome()
```

---

# 25. Campos privados

JavaScript moderno suporta campos privados com `#`.

```js
class Conta {
    #saldo = 0;

    depositar(valor) {
        this.#saldo += valor;
    }

    consultarSaldo() {
        return this.#saldo;
    }
}
```

Isto não é permitido:

```js
conta.#saldo;
```

---

# 26. Métodos assíncronos

Uma função pode ser:

```js
async function executar() {
}
```

Método:

```js
class Servico {
    async buscar() {
    }
}
```

Também:

```js
const buscar = async () => {
};
```

---

# 27. Generators

Generator usa:

```js
function*
```

e:

```js
yield
```

Exemplo:

```js
function* numeros() {
    yield 1;
    yield 2;
    yield 3;
}
```

Uso:

```js
const generator = numeros();

console.log(generator.next());
console.log(generator.next());
console.log(generator.next());
```

Cada chamada produz um resultado.

---

# 28. Erros e exceções

JavaScript possui:

```js
try
catch
finally
throw
```

Exemplo:

```js
try {
    throw new Error("Algo deu errado");
} catch (erro) {
    console.log(erro.message);
} finally {
    console.log("Finalizado");
}
```

---

## Criando erros

```js
throw new Error("Usuário não encontrado");
```

Também existem:

```js
TypeError
ReferenceError
RangeError
SyntaxError
URIError
AggregateError
```

---

## Classes de erro personalizadas

```js
class UsuarioNaoEncontradoError extends Error {
    constructor(mensagem) {
        super(mensagem);

        this.name = "UsuarioNaoEncontradoError";
    }
}
```

---

# 29. Módulos

Arquivo `matematica.js`:

```js
export function somar(a, b) {
    return a + b;
}
```

Outro arquivo:

```js
import { somar } from "./matematica.js";

console.log(somar(10, 20));
```

---

## Default export

```js
export default function somar(a, b) {
    return a + b;
}
```

Importação:

```js
import somar from "./matematica.js";
```

---

## Exportando várias coisas

```js
export const PI = 3.14;

export function somar(a, b) {
    return a + b;
}
```

---

# 30. JSON

JSON é muito utilizado para comunicação entre sistemas.

Objeto:

```js
const pessoa = {
    nome: "Willian",
    idade: 20
};
```

Converter para JSON:

```js
const json = JSON.stringify(pessoa);
```

JSON para objeto:

```js
const objeto = JSON.parse(json);
```

---

# 31. Promises

Promise representa uma operação que poderá produzir um resultado no futuro.

```js
const promessa = new Promise((resolve, reject) => {

    const sucesso = true;

    if (sucesso) {
        resolve("Funcionou");
    } else {
        reject(new Error("Falhou"));
    }
});
```

Consumindo:

```js
promessa
    .then(resultado => {
        console.log(resultado);
    })
    .catch(erro => {
        console.error(erro);
    })
    .finally(() => {
        console.log("Terminou");
    });
```

---

# 32. Async/Await

Forma moderna de trabalhar com Promises.

```js
async function executar() {
    const resultado = await promessa;

    console.log(resultado);
}
```

Com tratamento:

```js
async function executar() {
    try {
        const resultado = await promessa;

        console.log(resultado);
    } catch (erro) {
        console.error(erro);
    }
}
```

---

# 33. Fetch e APIs

No navegador e em ambientes modernos:

```js
const resposta = await fetch("https://api.exemplo.com/users");
```

Obtendo JSON:

```js
const dados = await resposta.json();
```

Exemplo:

```js
async function buscarUsuarios() {
    const resposta = await fetch("/api/users");

    if (!resposta.ok) {
        throw new Error("Erro ao buscar usuários");
    }

    return await resposta.json();
}
```

---

# 34. Map e Set

## Set

Coleção de valores únicos.

```js
const numeros = new Set();

numeros.add(1);
numeros.add(2);
numeros.add(2);
```

O segundo `2` não será duplicado.

---

## Map

Estrutura chave/valor.

```js
const usuarios = new Map();

usuarios.set(1, "Willian");
usuarios.set(2, "João");
```

Buscar:

```js
usuarios.get(1);
```

Verificar:

```js
usuarios.has(1);
```

Remover:

```js
usuarios.delete(1);
```

---

# 35. Iterables e Iterators

Um objeto pode implementar o protocolo de iteração.

Arrays são iteráveis.

Por isso:

```js
for (const numero of numeros) {
    console.log(numero);
}
```

funciona.

O mecanismo usa um iterator por trás.

---

# 36. Regex

Expressões regulares:

```js
const regex = /\d+/;
```

Verificar:

```js
regex.test("123");
```

Exemplo de email simples:

```js
const regex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
```

Uso:

```js
regex.test("teste@email.com");
```

---

# 37. Date

JavaScript possui:

```js
const agora = new Date();
```

Exemplos:

```js
agora.getFullYear();
agora.getMonth();
agora.getDate();
agora.getHours();
agora.getMinutes();
```

Cuidado:

```js
getMonth()
```

retorna mês baseado em zero.

Janeiro:

```text
0
```

Dezembro:

```text
11
```

Para aplicações complexas de data/hora, não trate `Date` como se fosse equivalente direto ao sistema de `DateTime` do C#.

---

# 38. Programação funcional

JavaScript permite programação funcional.

Funções são valores.

```js
const somar = (a, b) => a + b;
```

Podemos passar uma função:

```js
function executar(funcao) {
    funcao();
}

executar(() => {
    console.log("Olá");
});
```

Isso é chamado de **higher-order function**.

---

## Função como variável

```js
const saudacao = () => {
    console.log("Olá");
};
```

---

## Função retornando função

```js
function criarMultiplicador(fator) {
    return numero => numero * fator;
}

const dobrar = criarMultiplicador(2);

console.log(dobrar(10));
```

---

# 39. Protótipos

Aqui começa uma das partes mais importantes para realmente entender JavaScript.

JavaScript é baseado em protótipos.

Quando você faz:

```js
const pessoa = {
    nome: "Willian"
};
```

o objeto possui uma cadeia de protótipos.

Classes:

```js
class Pessoa {
    falar() {
        console.log("Olá");
    }
}
```

são uma sintaxe mais conveniente sobre mecanismos de protótipo.

Você não precisa dominar protótipos para começar a programar, mas precisa entendê-los para dominar JavaScript.

---

## prototype

```js
function Pessoa(nome) {
    this.nome = nome;
}

Pessoa.prototype.falar = function () {
    console.log(`Olá, ${this.nome}`);
};
```

---

# 40. Event Loop

Essa é uma das partes mais importantes do JavaScript.

JavaScript executa código de forma síncrona em sua thread principal, mas ambientes como navegador e Node.js fornecem mecanismos para lidar com operações assíncronas.

Exemplo:

```js
console.log("A");

setTimeout(() => {
    console.log("B");
}, 0);

console.log("C");
```

Resultado:

```text
A
C
B
```

O `setTimeout` não significa "execute imediatamente".

Ele agenda a callback para execução posterior.

---

## Modelo mental

Simplificando:

```text
Código JavaScript
       |
       v
Call Stack
       |
       v
APIs do ambiente
       |
       v
Task/Microtask Queues
       |
       v
Event Loop
       |
       v
Call Stack
```

Promises possuem tratamento especial através da fila de microtasks.

---

# 41. Diferenças importantes para C#

## 41.1 Tipagem

C#:

```csharp
int idade = 20;
```

JavaScript:

```js
let idade = 20;
```

JavaScript não verifica estaticamente que `idade` é `number`.

---

## 41.2 Classes

C#:

```csharp
public class Pessoa
{
    public string Nome { get; set; }

    public void Falar()
    {
    }
}
```

JavaScript:

```js
class Pessoa {
    constructor(nome) {
        this.nome = nome;
    }

    falar() {
    }
}
```

---

## 41.3 Static

C#:

```csharp
public static int Somar(int a, int b)
{
    return a + b;
}
```

JavaScript:

```js
static somar(a, b) {
    return a + b;
}
```

---

## 41.4 Async

C#:

```csharp
public async Task<string> Buscar()
{
    return await ...
}
```

JavaScript:

```js
async buscar() {
    return await ...;
}
```

O equivalente conceitual de `Task` é normalmente uma `Promise`, mas não são a mesma abstração.

---

## 41.5 LINQ

C#:

```csharp
var resultado = numeros
    .Where(x => x > 10)
    .Select(x => x * 2)
    .ToList();
```

JavaScript:

```js
const resultado = numeros
    .filter(x => x > 10)
    .map(x => x * 2);
```

---

## 41.6 Extension Methods

C#:

```csharp
public static class StringExtensions
{
    public static bool EhValida(this string valor)
    {
        return !string.IsNullOrWhiteSpace(valor);
    }
}
```

JavaScript não possui um equivalente nativo direto.

É possível alterar prototypes:

```js
String.prototype.ehValida = function () {
    return this.trim().length > 0;
};
```

Mas isso normalmente deve ser evitado em aplicações grandes.

Prefira:

```js
function ehValida(valor) {
    return valor.trim().length > 0;
}
```

ou:

```js
const ehValida = valor => valor.trim().length > 0;
```

---

## 41.7 Overload

C# possui overload real:

```csharp
void Somar(int a, int b)
void Somar(double a, double b)
```

JavaScript não possui overload tradicional.

Se você declarar:

```js
function somar(a, b) {}
function somar(a, b, c) {}
```

a segunda definição sobrescreve a primeira.

Normalmente usa-se:

```js
function somar(...numeros) {
    // ...
}
```

ou lógica condicional.

TypeScript adiciona suporte a **overload signatures**, mas isso será explicado no arquivo de TypeScript.

---

# 42. Boas práticas

## Prefira const

```js
const nome = "Willian";
```

Use `let` quando precisar reatribuir.

Evite `var`.

---

## Prefira ===

```js
if (valor === 10) {
}
```

---

## Evite modificar objetos sem necessidade

Em vez de:

```js
pessoa.nome = "João";
```

às vezes prefira:

```js
const novaPessoa = {
    ...pessoa,
    nome: "João"
};
```

---

## Não abuse de classes

JavaScript funciona muito bem com:

* funções;
* objetos;
* composição;
* módulos;
* programação funcional.

Classe não é obrigatória.

---

## Separe responsabilidades

Evite:

```js
async function fazerTudo() {
    // valida usuário
    // acessa banco
    // faz HTTP
    // transforma dados
    // salva arquivo
    // envia email
}
```

Prefira componentes menores.

---

# 43. Checklist

Antes de considerar seu JavaScript básico/intermediário consolidado, você deve conseguir explicar:

## Fundamentos

* [ ] `let`
* [ ] `const`
* [ ] `var`
* [ ] `string`
* [ ] `number`
* [ ] `boolean`
* [ ] `null`
* [ ] `undefined`
* [ ] `bigint`
* [ ] `symbol`
* [ ] `object`

## Controle

* [ ] `if`
* [ ] `else`
* [ ] `switch`
* [ ] `for`
* [ ] `while`
* [ ] `for...of`
* [ ] `for...in`

## Funções

* [ ] funções tradicionais
* [ ] arrow functions
* [ ] parâmetros padrão
* [ ] rest
* [ ] closures
* [ ] callbacks
* [ ] higher-order functions

## Estruturas

* [ ] arrays
* [ ] objetos
* [ ] destructuring
* [ ] spread
* [ ] Map
* [ ] Set

## OOP

* [ ] classes
* [ ] constructor
* [ ] métodos
* [ ] herança
* [ ] `extends`
* [ ] `super`
* [ ] `static`
* [ ] getters
* [ ] setters
* [ ] campos privados

## Assíncrono

* [ ] Promise
* [ ] async
* [ ] await
* [ ] try/catch
* [ ] fetch
* [ ] Event Loop

## JavaScript avançado/intermediário

* [ ] prototypes
* [ ] prototype chain
* [ ] generators
* [ ] iterators
* [ ] closures
* [ ] microtasks
* [ ] módulos
* [ ] JSON
* [ ] regex

---

# Mentalidade para quem vem de C#

A maior mudança não é decorar:

```js
const
let
function
class
```

A mudança real é entender que JavaScript é uma linguagem dinâmica e baseada em protótipos.

Em C#, você tende a pensar:

```text
Classe
    ↓
Objeto
    ↓
Tipo
    ↓
Contrato
```

Em JavaScript, você precisa se acostumar com:

```text
Objeto
    ↓
Protótipo
    ↓
Outro protótipo
    ↓
Object.prototype
    ↓
null
```

E também:

```text
Função
    ↓
pode ser valor
    ↓
pode ser argumento
    ↓
pode ser retorno
    ↓
pode possuir propriedades
```

Essa mudança de mentalidade é mais importante que decorar sintaxe.

---

# Próximo passo

Depois de dominar este arquivo, o caminho natural é:

```text
JavaScript básico
        ↓
JavaScript intermediário
        ↓
TypeScript
        ↓
Node.js
        ↓
npm
        ↓
APIs
        ↓
Frameworks
        ↓
Arquitetura
```

TypeScript deve ser estudado **depois de entender razoavelmente bem JavaScript**, porque TypeScript não substitui o modelo de execução do JavaScript. Ele adiciona principalmente verificação estática e recursos de tipos ao ecossistema JavaScript.
