# TypeScript — Do Básico ao Intermediário

> Guia de TypeScript para quem já possui fundamentos de programação e conhecimentos de C#.

---

# Sumário

1. [O que é TypeScript](#1-o-que-é-typescript)
2. [JavaScript × TypeScript](#2-javascript--typescript)
3. [Como TypeScript funciona](#3-como-typescript-funciona)
4. [Configurando um projeto](#4-configurando-um-projeto)
5. [Tipos básicos](#5-tipos-básicos)
6. [Inferência de tipos](#6-inferência-de-tipos)
7. [Arrays](#7-arrays)
8. [Tuplas](#8-tuplas)
9. [Objetos tipados](#9-objetos-tipados)
10. [Type Alias](#10-type-alias)
11. [Interfaces](#11-interfaces)
12. [Optional e Readonly](#12-optional-e-readonly)
13. [Union Types](#13-union-types)
14. [Literal Types](#14-literal-types)
15. [Intersection Types](#15-intersection-types)
16. [any](#16-any)
17. [unknown](#17-unknown)
18. [never](#18-never)
19. [void](#19-void)
20. [Funções](#20-funções)
21. [Parâmetros opcionais](#21-parâmetros-opcionais)
22. [Rest Parameters](#22-rest-parameters)
23. [Function Types](#23-function-types)
24. [Overloads](#24-overloads)
25. [Classes](#25-classes)
26. [Public, Private e Protected](#26-public-private-e-protected)
27. [Readonly](#27-readonly)
28. [Static](#28-static)
29. [Abstract](#29-abstract)
30. [Override](#30-override)
31. [Herança](#31-herança)
32. [Implements](#32-implements)
33. [Getters e Setters](#33-getters-e-setters)
34. [Parameter Properties](#34-parameter-properties)
35. [Generics](#35-generics)
36. [Generic Constraints](#36-generic-constraints)
37. [Narrowing](#37-narrowing)
38. [Type Guards](#38-type-guards)
39. [Type Assertions](#39-type-assertions)
40. [typeof](#40-typeof)
41. [keyof](#41-keyof)
42. [Indexed Access Types](#42-indexed-access-types)
43. [Utility Types](#43-utility-types)
44. [Mapped Types](#44-mapped-types)
45. [Conditional Types](#45-conditional-types)
46. [Template Literal Types](#46-template-literal-types)
47. [Enums](#47-enums)
48. [Modules](#48-modules)
49. [Promises](#49-promises)
50. [Async/Await](#50-asyncawait)
51. [Exceções](#51-exceções)
52. [Extension Methods](#52-extension-methods)
53. [Decorators](#53-decorators)
54. [Declaration Merging](#54-declaration-merging)
55. [Structural Typing](#55-structural-typing)
56. [Tipos em runtime × compile time](#56-tipos-em-runtime--compile-time)
57. [Type Erasure](#57-type-erasure)
58. [TypeScript × C#](#58-typescript--c)
59. [Boas práticas](#59-boas-práticas)
60. [Checklist](#60-checklist)

---

# 1. O que é TypeScript

TypeScript é uma linguagem construída sobre JavaScript que adiciona um sistema de tipos estático e ferramentas de verificação durante o desenvolvimento.

A ideia central:

```text
TypeScript
    ↓
verificação de tipos
    ↓
JavaScript
    ↓
runtime
```

O navegador normalmente não executa TypeScript diretamente.

O TypeScript é transformado em JavaScript.

---

# 2. JavaScript × TypeScript

JavaScript:

```js
function somar(a, b) {
    return a + b;
}
```

TypeScript:

```ts
function somar(a: number, b: number): number {
    return a + b;
}
```

Agora temos:

```text
a: number
b: number
): number
```

Ou seja:

```text
parâmetro : tipo
retorno : tipo
```

---

# 3. Como TypeScript funciona

Imagine:

```ts
const idade: number = 20;
```

O TypeScript verifica o código.

Depois, o código pode virar algo como:

```js
const idade = 20;
```

A anotação:

```ts
: number
```

não precisa existir no JavaScript final.

Isso é fundamental:

> TypeScript adiciona informações de tipos ao desenvolvimento, mas o runtime continua sendo JavaScript.

---

# 4. Configurando um projeto

Inicializar:

```bash
npm init -y
```

Instalar TypeScript:

```bash
npm install -D typescript
```

Criar configuração:

```bash
npx tsc --init
```

Normalmente você terá:

```text
projeto/
├── src/
│   └── index.ts
├── package.json
└── tsconfig.json
```

---

# 5. Tipos básicos

## string

```ts
let nome: string = "Willian";
```

## number

```ts
let idade: number = 20;
```

## boolean

```ts
let ativo: boolean = true;
```

## bigint

```ts
const numero: bigint = 123456789n;
```

## symbol

```ts
const id: symbol = Symbol("id");
```

## null

```ts
let valor: null = null;
```

## undefined

```ts
let valor: undefined = undefined;
```

---

# 6. Inferência de tipos

Você não precisa escrever tipo em absolutamente tudo.

```ts
const nome = "Willian";
```

TypeScript entende:

```text
nome: string
```

Outro exemplo:

```ts
const idade = 20;
```

O compilador infere:

```text
idade: number
```

Portanto, isto normalmente é desnecessário:

```ts
const nome: string = "Willian";
```

A inferência pode ser preferível:

```ts
const nome = "Willian";
```

---

# 7. Arrays

Forma:

```ts
const numeros: number[] = [1, 2, 3];
```

Também:

```ts
const numeros: Array<number> = [1, 2, 3];
```

Strings:

```ts
const nomes: string[] = [
    "Willian",
    "João"
];
```

---

# 8. Tuplas

Tupla representa uma estrutura com posições e tipos definidos.

```ts
const pessoa: [string, number] = [
    "Willian",
    20
];
```

Aqui:

```text
posição 0 → string
posição 1 → number
```

Pode lembrar:

```csharp
(string Nome, int Idade)
```

ou certos usos de `ValueTuple`.

---

# 9. Objetos tipados

```ts
const pessoa: {
    nome: string;
    idade: number;
} = {
    nome: "Willian",
    idade: 20
};
```

Funciona, mas repetir esse formato não é conveniente.

Para estruturas reutilizáveis, use:

```ts
type Pessoa = {
    nome: string;
    idade: number;
};
```

Depois:

```ts
const pessoa: Pessoa = {
    nome: "Willian",
    idade: 20
};
```

---

# 10. Type Alias

Criando um tipo:

```ts
type Pessoa = {
    nome: string;
    idade: number;
};
```

Uso:

```ts
const pessoa: Pessoa = {
    nome: "Willian",
    idade: 20
};
```

Pode também representar tipos primitivos:

```ts
type Id = number;
```

Ou união:

```ts
type Status = "ativo" | "inativo";
```

---

# 11. Interfaces

Interface:

```ts
interface Pessoa {
    nome: string;
    idade: number;
}
```

Uso:

```ts
const pessoa: Pessoa = {
    nome: "Willian",
    idade: 20
};
```

---

## Interface com método

```ts
interface Pessoa {
    nome: string;

    falar(): void;
}
```

Implementação:

```ts
class Usuario implements Pessoa {
    nome: string;

    falar(): void {
        console.log("Olá");
    }
}
```

---

# 12. Optional e Readonly

## Optional

```ts
interface Pessoa {
    nome: string;
    idade?: number;
}
```

Agora isto é válido:

```ts
const pessoa: Pessoa = {
    nome: "Willian"
};
```

O `?` significa:

```text
propriedade pode não existir
```

---

## Readonly

```ts
interface Pessoa {
    readonly id: number;
    nome: string;
}
```

Depois:

```ts
pessoa.id = 10;
```

pode gerar erro de TypeScript.

---

# 13. Union Types

Uma variável pode aceitar mais de um tipo.

```ts
let id: number | string;
```

Agora:

```ts
id = 10;
id = "abc";
```

são válidos.

Mas:

```ts
id = true;
```

não.

---

## Union com objetos

```ts
type Resultado =
    | string
    | number
    | null;
```

---

# 14. Literal Types

Podemos restringir os valores possíveis.

```ts
type Status = "ativo" | "inativo";
```

Agora:

```ts
let status: Status = "ativo";
```

Isto é inválido:

```ts
status = "qualquer";
```

---

## Similar a enum conceitual

```ts
type Direcao =
    | "up"
    | "down"
    | "left"
    | "right";
```

---

# 15. Intersection Types

Une tipos.

```ts
type Pessoa = {
    nome: string;
};

type Funcionario = {
    salario: number;
};

type FuncionarioCompleto = Pessoa & Funcionario;
```

Agora:

```ts
const funcionario: FuncionarioCompleto = {
    nome: "Willian",
    salario: 5000
};
```

---

# 16. any

```ts
let valor: any;
```

`any` praticamente desliga a verificação de tipos naquele valor.

```ts
valor = 10;
valor = "texto";
valor = true;
```

Pode acessar:

```ts
valor.algumaCoisa.inexistente();
```

O compilador pode deixar passar.

Evite `any` sempre que possível.

---

# 17. unknown

`unknown` é mais seguro.

```ts
let valor: unknown;
```

Você não pode simplesmente fazer:

```ts
valor.toUpperCase();
```

Primeiro precisa verificar:

```ts
if (typeof valor === "string") {
    valor.toUpperCase();
}
```

Mentalidade:

```text
any
↓
"confie em mim"

unknown
↓
"prove para mim que é seguro"
```

---

# 18. never

Representa algo que nunca acontece.

Exemplo:

```ts
function erro(): never {
    throw new Error("Erro");
}
```

Outro caso:

```ts
function loopInfinito(): never {
    while (true) {
    }
}
```

Também aparece bastante em análise exaustiva de unions.

---

# 19. void

Normalmente utilizado para funções que não retornam valor útil:

```ts
function logar(mensagem: string): void {
    console.log(mensagem);
}
```

---

# 20. Funções

```ts
function somar(
    a: number,
    b: number
): number {
    return a + b;
}
```

Arrow:

```ts
const somar = (
    a: number,
    b: number
): number => {
    return a + b;
};
```

Forma curta:

```ts
const somar = (a: number, b: number): number =>
    a + b;
```

---

# 21. Parâmetros opcionais

```ts
function saudar(nome?: string) {
    console.log(nome);
}
```

Uso:

```ts
saudar();
saudar("Willian");
```

---

# 22. Rest Parameters

```ts
function somar(...numeros: number[]): number {
    return numeros.reduce(
        (total, numero) => total + numero,
        0
    );
}
```

Uso:

```ts
somar(1, 2, 3, 4);
```

---

# 23. Function Types

Podemos armazenar o tipo de uma função.

```ts
type Operacao = (
    a: number,
    b: number
) => number;
```

Depois:

```ts
const somar: Operacao = (a, b) => a + b;
```

Outro exemplo:

```ts
function executar(
    operacao: Operacao
) {
    return operacao(10, 20);
}
```

---

# 24. Overloads

Aqui existe uma diferença interessante para C#.

TypeScript permite declarar overload signatures:

```ts
function buscar(id: number): Usuario;
function buscar(nome: string): Usuario;

function buscar(
    valor: number | string
): Usuario {
    // implementação
}
```

A implementação possui uma única função real.

O TypeScript utiliza as assinaturas para verificar as chamadas.

Isso não cria múltiplos métodos em runtime.

---

# 25. Classes

```ts
class Pessoa {
    nome: string;
    idade: number;

    constructor(nome: string, idade: number) {
        this.nome = nome;
        this.idade = idade;
    }

    apresentar(): void {
        console.log(
            `Meu nome é ${this.nome}`
        );
    }
}
```

Uso:

```ts
const pessoa = new Pessoa(
    "Willian",
    20
);
```

---

# 26. Public, Private e Protected

## public

```ts
class Pessoa {
    public nome: string;
}
```

`public` é o padrão.

Então:

```ts
class Pessoa {
    nome: string;
}
```

é equivalente a:

```ts
class Pessoa {
    public nome: string;
}
```

---

## private

```ts
class Conta {
    private saldo: number = 0;
}
```

Isso é verificado pelo TypeScript.

---

## protected

```ts
class Animal {
    protected nome: string;

    constructor(nome: string) {
        this.nome = nome;
    }
}
```

Classe filha pode acessar:

```ts
class Cachorro extends Animal {
    mostrarNome() {
        console.log(this.nome);
    }
}
```

---

# 27. Readonly

```ts
class Pessoa {
    readonly id: number;

    constructor(id: number) {
        this.id = id;
    }
}
```

Depois:

```ts
pessoa.id = 10;
```

gera erro de TypeScript.

---

# 28. Static

```ts
class Matematica {
    static PI = 3.14159;

    static somar(
        a: number,
        b: number
    ): number {
        return a + b;
    }
}
```

Uso:

```ts
Matematica.PI;

Matematica.somar(10, 20);
```

Não:

```ts
const m = new Matematica();

m.somar(10, 20);
```

---

# 29. Abstract

Classe abstrata:

```ts
abstract class Animal {
    abstract falar(): void;

    dormir(): void {
        console.log("Dormindo");
    }
}
```

Não pode:

```ts
const animal = new Animal();
```

Classe concreta:

```ts
class Cachorro extends Animal {
    falar(): void {
        console.log("Au au");
    }
}
```

---

# 30. Override

Esse é especialmente familiar para quem vem de C#.

```ts
class Animal {
    falar(): void {
        console.log("Som");
    }
}

class Cachorro extends Animal {
    override falar(): void {
        console.log("Au au");
    }
}
```

`override` informa que o método está sobrescrevendo um membro da classe pai.

Isso ajuda o compilador a detectar erros.

---

# 31. Herança

```ts
class Pessoa {
    constructor(
        public nome: string
    ) {}
}

class Aluno extends Pessoa {
    constructor(
        nome: string,
        public matricula: string
    ) {
        super(nome);
    }
}
```

Uso:

```ts
const aluno = new Aluno(
    "Willian",
    "123"
);
```

---

# 32. Implements

Uma classe pode implementar uma interface.

```ts
interface Animal {
    nome: string;

    falar(): void;
}
```

Classe:

```ts
class Cachorro implements Animal {
    nome: string;

    constructor(nome: string) {
        this.nome = nome;
    }

    falar(): void {
        console.log("Au au");
    }
}
```

---

# 33. Getters e Setters

```ts
class Pessoa {
    private _nome: string;

    constructor(nome: string) {
        this._nome = nome;
    }

    get nome(): string {
        return this._nome;
    }

    set nome(valor: string) {
        this._nome = valor;
    }
}
```

Uso:

```ts
const pessoa = new Pessoa("Willian");

console.log(pessoa.nome);

pessoa.nome = "João";
```

Isso é conceitualmente próximo das propriedades de C#.

---

# 34. Parameter Properties

TypeScript possui uma funcionalidade extremamente conveniente para quem vem de C#.

Em vez de:

```ts
class Pessoa {
    public nome: string;
    public idade: number;

    constructor(
        nome: string,
        idade: number
    ) {
        this.nome = nome;
        this.idade = idade;
    }
}
```

Pode escrever:

```ts
class Pessoa {
    constructor(
        public nome: string,
        public idade: number
    ) {}
}
```

Também:

```ts
class Conta {
    constructor(
        private saldo: number
    ) {}
}
```

E:

```ts
class Usuario {
    constructor(
        public readonly id: number,
        public nome: string
    ) {}
}
```

Isso é uma das partes do TypeScript que mais lembra C#.

---

# 35. Generics

Generic:

```ts
function identidade<T>(
    valor: T
): T {
    return valor;
}
```

Uso:

```ts
const numero = identidade<number>(10);

const texto = identidade<string>("Olá");
```

Frequentemente o TypeScript infere:

```ts
const numero = identidade(10);
```

---

## Generic em classe

```ts
class Caixa<T> {
    constructor(
        public valor: T
    ) {}
}
```

Uso:

```ts
const caixaNumero =
    new Caixa<number>(10);

const caixaTexto =
    new Caixa<string>("Olá");
```

---

# 36. Generic Constraints

Podemos restringir um generic.

```ts
function tamanho<T extends { length: number }>(
    valor: T
): number {
    return valor.length;
}
```

Funciona:

```ts
tamanho("Olá");
tamanho([1, 2, 3]);
```

Mas não:

```ts
tamanho(10);
```

Porque `number` não possui `length`.

---

# 37. Narrowing

TypeScript consegue refinar tipos.

```ts
function imprimir(
    valor: string | number
) {
    if (typeof valor === "string") {
        console.log(
            valor.toUpperCase()
        );
    } else {
        console.log(
            valor.toFixed(2)
        );
    }
}
```

Antes:

```text
string | number
```

Depois do `typeof`:

```text
string
```

ou:

```text
number
```

---

# 38. Type Guards

Podemos criar verificações próprias.

```ts
interface Cachorro {
    latir(): void;
}

interface Gato {
    miar(): void;
}

function ehCachorro(
    animal: Cachorro | Gato
): animal is Cachorro {
    return "latir" in animal;
}
```

Agora:

```ts
function fazerBarulho(
    animal: Cachorro | Gato
) {
    if (ehCachorro(animal)) {
        animal.latir();
    } else {
        animal.miar();
    }
}
```

O:

```ts
animal is Cachorro
```

é um **type predicate**.

---

# 39. Type Assertions

Às vezes você sabe algo que o compilador não sabe.

```ts
const elemento =
    document.getElementById("app")
    as HTMLDivElement;
```

Outra sintaxe:

```ts
const elemento =
    <HTMLDivElement>(
        document.getElementById("app")
    );
```

Em código moderno com JSX, prefira:

```ts
as
```

porque a outra sintaxe pode conflitar com JSX.

---

# 40. typeof

`typeof` pode ser utilizado para verificar tipos em runtime:

```ts
typeof valor === "string"
```

Também pode ser utilizado em contexto de tipos.

```ts
const pessoa = {
    nome: "Willian",
    idade: 20
};

type Pessoa = typeof pessoa;
```

Agora:

```text
Pessoa
```

é derivado do objeto.

---

# 41. keyof

`keyof` obtém as chaves de um tipo.

```ts
type Pessoa = {
    nome: string;
    idade: number;
};
```

Então:

```ts
type ChavePessoa = keyof Pessoa;
```

Equivale conceitualmente a:

```text
"nome" | "idade"
```

---

## Uso prático

```ts
function obterValor(
    pessoa: Pessoa,
    chave: keyof Pessoa
) {
    return pessoa[chave];
}
```

Agora:

```ts
obterValor(pessoa, "nome");
obterValor(pessoa, "idade");
```

Mas:

```ts
obterValor(pessoa, "banana");
```

é inválido.

---

# 42. Indexed Access Types

Podemos acessar um tipo através de uma chave.

```ts
type Pessoa = {
    nome: string;
    idade: number;
};
```

Então:

```ts
type TipoNome = Pessoa["nome"];
```

Resultado:

```text
string
```

E:

```ts
type TipoIdade = Pessoa["idade"];
```

Resultado:

```text
number
```

---

# 43. Utility Types

TypeScript possui vários tipos utilitários.

## Partial

Torna propriedades opcionais.

```ts
type Pessoa = {
    nome: string;
    idade: number;
};

type PessoaParcial = Partial<Pessoa>;
```

Agora:

```ts
const pessoa: PessoaParcial = {};
```

---

## Required

Torna propriedades obrigatórias:

```ts
type PessoaCompleta =
    Required<PessoaParcial>;
```

---

## Readonly

```ts
type PessoaImutavel =
    Readonly<Pessoa>;
```

---

## Pick

Seleciona propriedades:

```ts
type PessoaResumo =
    Pick<Pessoa, "nome">;
```

---

## Omit

Remove propriedades:

```ts
type PessoaSemId =
    Omit<Pessoa, "id">;
```

---

## Record

Cria um objeto baseado em chave/valor:

```ts
type Usuarios =
    Record<number, string>;
```

Exemplo:

```ts
const usuarios: Usuarios = {
    1: "Willian",
    2: "João"
};
```

---

## Exclude

Remove membros de uma união:

```ts
type Status =
    "ativo"
    | "inativo"
    | "bloqueado";

type StatusPermitido =
    Exclude<Status, "bloqueado">;
```

---

## Extract

Extrai membros compatíveis:

```ts
type A = Extract<
    "a" | "b" | "c",
    "a" | "b"
>;
```

Resultado:

```text
"a" | "b"
```

---

## ReturnType

Obtém o retorno de uma função.

```ts
function buscar(): Promise<string> {
    // ...
}
```

Então:

```ts
type Resultado =
    ReturnType<typeof buscar>;
```

Resultado:

```text
Promise<string>
```

---

# 44. Mapped Types

Mapped types permitem construir tipos a partir de outros tipos.

Exemplo:

```ts
type Pessoa = {
    nome: string;
    idade: number;
};
```

Podemos criar:

```ts
type SomenteLeitura<T> = {
    readonly [P in keyof T]: T[P];
};
```

Agora:

```ts
type PessoaReadonly =
    SomenteLeitura<Pessoa>;
```

É semelhante à ideia de:

```ts
Readonly<Pessoa>
```

---

# 45. Conditional Types

Tipos condicionais:

```ts
type EhString<T> =
    T extends string
        ? true
        : false;
```

Então:

```ts
type A = EhString<string>;
```

é:

```text
true
```

Enquanto:

```ts
type B = EhString<number>;
```

é:

```text
false
```

Isso é uma das partes que começa a levar TypeScript para um nível mais avançado.

---

# 46. Template Literal Types

Não confunda com template literals normais do JavaScript.

JavaScript:

```ts
const nome = "Willian";

const texto = `Olá ${nome}`;
```

TypeScript pode usar template literal types:

```ts
type Evento =
    `on${string}`;
```

Então:

```ts
const evento: Evento = "onclick";
```

---

## Exemplo mais interessante

```ts
type Cor =
    "red"
    | "blue"
    | "green";

type Classe =
    `bg-${Cor}`;
```

Agora:

```text
bg-red
bg-blue
bg-green
```

são válidos.

---

# 47. Enums

TypeScript possui `enum`.

```ts
enum Status {
    Ativo,
    Inativo,
    Bloqueado
}
```

Uso:

```ts
const status = Status.Ativo;
```

Enums existem no TypeScript, mas não são sempre a melhor escolha.

Muitas vezes:

```ts
type Status =
    | "ativo"
    | "inativo"
    | "bloqueado";
```

é mais simples e adequado.

---

# 48. Modules

Exportar:

```ts
export function somar(
    a: number,
    b: number
): number {
    return a + b;
}
```

Importar:

```ts
import { somar } from "./matematica";
```

---

## Export default

```ts
export default class Pessoa {
}
```

Importação:

```ts
import Pessoa from "./Pessoa";
```

---

# 49. Promises

```ts
const promessa: Promise<string> =
    new Promise((resolve) => {
        resolve("Olá");
    });
```

Função:

```ts
function buscarNome(): Promise<string> {
    return Promise.resolve("Willian");
}
```

---

# 50. Async/Await

```ts
async function buscarNome(): Promise<string> {
    return "Willian";
}
```

Consumindo:

```ts
async function executar() {
    const nome = await buscarNome();

    console.log(nome);
}
```

Uma função `async` normalmente retorna uma `Promise`.

Por exemplo:

```ts
async function numero(): Promise<number> {
    return 10;
}
```

Mesmo retornando:

```ts
10
```

a função produz:

```text
Promise<number>
```

---

# 51. Exceções

```ts
try {
    throw new Error("Erro");
} catch (erro) {
    console.log(erro);
}
```

Uma diferença importante:

JavaScript não possui checked exceptions como parte do sistema de tipos.

TypeScript também não força:

```ts
try/catch
```

em chamadas que podem falhar.

---

## unknown no catch

Você pode configurar o TypeScript para tratar o erro capturado como `unknown`.

Isso é mais seguro:

```ts
try {
    // ...
} catch (erro) {
    if (erro instanceof Error) {
        console.log(erro.message);
    }
}
```

---

# 52. Extension Methods

Essa é uma das diferenças importantes para quem vem de C#.

C#:

```csharp
public static bool EhValida(
    this string valor)
{
    return !string.IsNullOrWhiteSpace(valor);
}
```

Você consegue:

```csharp
texto.EhValida();
```

TypeScript não possui extension methods nativos equivalentes aos de C#.

Uma alternativa é uma função:

```ts
function ehValida(
    valor: string
): boolean {
    return valor.trim().length > 0;
}
```

Uso:

```ts
ehValida(texto);
```

---

## Prototype augmentation

Tecnicamente é possível modificar prototypes:

```ts
interface String {
    ehValida(): boolean;
}

String.prototype.ehValida =
    function (): boolean {
        return this.trim().length > 0;
    };
```

Agora:

```ts
"Olá".ehValida();
```

pode funcionar.

Mas isso deve ser usado com muito cuidado.

Em aplicações grandes, modificar prototypes globais pode causar conflitos e comportamento inesperado.

---

# 53. Decorators

Decorators permitem adicionar metaprogramação a certas construções.

Exemplo conceitual:

```ts
function logged(
    originalMethod: any,
    context: ClassMethodDecoratorContext
) {
    // ...
}
```

Uso:

```ts
class Pessoa {
    @logged
    falar() {
        console.log("Olá");
    }
}
```

Decorators são um assunto mais avançado e possuem detalhes importantes relacionados ao padrão ECMAScript e às diferentes configurações/legados do TypeScript.

Não trate decorators simplesmente como "anotações de C#".

---

# 54. Declaration Merging

TypeScript possui uma característica muito particular:

```ts
interface Pessoa {
    nome: string;
}

interface Pessoa {
    idade: number;
}
```

As interfaces podem ser combinadas.

Agora:

```ts
const pessoa: Pessoa = {
    nome: "Willian",
    idade: 20
};
```

Isso é chamado de **declaration merging**.

---

# 55. Structural Typing

Essa é uma das diferenças mais importantes entre TypeScript e C#.

TypeScript usa principalmente **structural typing**.

Imagine:

```ts
interface Pessoa {
    nome: string;
}
```

E:

```ts
const usuario = {
    nome: "Willian",
    idade: 20
};
```

Podemos fazer:

```ts
const pessoa: Pessoa = usuario;
```

Por quê?

Porque `usuario` possui pelo menos a estrutura necessária:

```text
nome: string
```

---

## C# × TypeScript

C# tende a utilizar tipagem nominal:

```text
Tipo A
≠
Tipo B
```

mesmo que tenham membros semelhantes.

TypeScript pergunta mais:

```text
"Esse objeto possui a estrutura necessária?"
```

Essa diferença precisa ser entendida profundamente.

---

# 56. Tipos em runtime × compile time

Este código:

```ts
const idade: number = 20;
```

O tipo:

```ts
number
```

é uma informação usada pelo TypeScript.

No runtime JavaScript, não existe:

```text
TypeScript number
```

como sistema de tipos runtime equivalente ao C#.

Por isso isto não funciona como você poderia imaginar:

```ts
if (idade instanceof number) {
}
```

`number` não é uma classe dessa forma.

Use:

```ts
typeof idade === "number"
```

quando precisar de uma verificação runtime.

---

# 57. Type Erasure

Considere:

```ts
function somar(
    a: number,
    b: number
): number {
    return a + b;
}
```

O JavaScript resultante pode ser essencialmente:

```js
function somar(a, b) {
    return a + b;
}
```

Os tipos foram removidos.

Isso é chamado de **type erasure**.

Portanto:

```ts
interface Usuario {
    nome: string;
}
```

não cria automaticamente uma entidade runtime chamada:

```text
Usuario
```

---

# 58. TypeScript × C#

## Variáveis

C#:

```csharp
int idade = 20;
```

TypeScript:

```ts
let idade: number = 20;
```

---

## Inferência

C#:

```csharp
var idade = 20;
```

TypeScript:

```ts
const idade = 20;
```

Ambos inferem tipos, mas `var` de C# e `const` de JS/TS têm significados diferentes.

---

## Classe

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

TypeScript:

```ts
class Pessoa {
    nome: string;

    constructor(nome: string) {
        this.nome = nome;
    }

    falar(): void {
    }
}
```

---

## Propriedade

C#:

```csharp
public string Nome { get; set; }
```

TypeScript:

```ts
get nome(): string {
    return this._nome;
}

set nome(valor: string) {
    this._nome = valor;
}
```

Ou simplesmente um campo:

```ts
nome: string;
```

---

## Static

C#:

```csharp
public static int Somar(
    int a,
    int b)
{
    return a + b;
}
```

TypeScript:

```ts
static somar(
    a: number,
    b: number
): number {
    return a + b;
}
```

---

## Abstract

C#:

```csharp
public abstract class Animal
{
    public abstract void Falar();
}
```

TypeScript:

```ts
abstract class Animal {
    abstract falar(): void;
}
```

---

## Interface

C#:

```csharp
public interface IAnimal
{
    void Falar();
}
```

TypeScript:

```ts
interface Animal {
    falar(): void;
}
```

---

## Generic

C#:

```csharp
public T Identidade<T>(T valor)
{
    return valor;
}
```

TypeScript:

```ts
function identidade<T>(
    valor: T
): T {
    return valor;
}
```

---

## Task

C#:

```csharp
Task<string>
```

TypeScript:

```ts
Promise<string>
```

São conceitos relacionados, mas não são implementações idênticas.

---

## LINQ

C#:

```csharp
var resultado = numeros
    .Where(x => x > 10)
    .Select(x => x * 2)
    .ToList();
```

TypeScript:

```ts
const resultado = numeros
    .filter(x => x > 10)
    .map(x => x * 2);
```

---

## Extension Methods

C#:

```csharp
texto.EhValido();
```

TypeScript:

```ts
ehValido(texto);
```

Não existe equivalente nativo direto.

---

# 59. Boas práticas

## Evite any

Ruim:

```ts
function processar(valor: any) {
}
```

Prefira:

```ts
function processar(valor: unknown) {
}
```

e faça narrowing.

---

## Use tipos expressivos

Ruim:

```ts
let status: string;
```

Melhor:

```ts
type Status =
    | "ativo"
    | "inativo"
    | "bloqueado";
```

---

## Prefira inferência quando for óbvia

Desnecessário:

```ts
const nome: string = "Willian";
```

Pode ser:

```ts
const nome = "Willian";
```

Mas explicitar tipos é útil em APIs públicas e lugares onde melhora a leitura.

---

## Use interfaces/types com propósito

Não transforme toda variável em uma abstração gigante.

Ruim:

```ts
type TipoSuperAbstratoComTudo = ...
```

Mantenha os tipos compreensíveis.

---

## Use strict

Em projetos sérios, habilitar verificações estritas é altamente recomendável.

No `tsconfig.json`:

```json
{
    "compilerOptions": {
        "strict": true
    }
}
```

Isso muda bastante a qualidade da verificação de tipos.

---

# 60. Checklist

## Fundamentos

* [ ] `string`
* [ ] `number`
* [ ] `boolean`
* [ ] `null`
* [ ] `undefined`
* [ ] `bigint`
* [ ] `symbol`
* [ ] arrays
* [ ] tuples
* [ ] objects

## Sistema de tipos

* [ ] inferência
* [ ] type aliases
* [ ] interfaces
* [ ] optional properties
* [ ] readonly
* [ ] unions
* [ ] literal types
* [ ] intersections
* [ ] any
* [ ] unknown
* [ ] never
* [ ] void

## Funções

* [ ] parâmetros tipados
* [ ] retorno tipado
* [ ] funções opcionais
* [ ] rest parameters
* [ ] function types
* [ ] overloads

## OOP

* [ ] classes
* [ ] constructor
* [ ] public
* [ ] private
* [ ] protected
* [ ] readonly
* [ ] static
* [ ] abstract
* [ ] override
* [ ] extends
* [ ] implements
* [ ] getters
* [ ] setters
* [ ] parameter properties

## Generics

* [ ] generic functions
* [ ] generic classes
* [ ] constraints
* [ ] `extends` em generics

## Type manipulation

* [ ] narrowing
* [ ] type guards
* [ ] type predicates
* [ ] assertions
* [ ] typeof
* [ ] keyof
* [ ] indexed access
* [ ] utility types
* [ ] mapped types
* [ ] conditional types
* [ ] template literal types

## JavaScript/Runtime

* [ ] Promise
* [ ] async
* [ ] await
* [ ] modules
* [ ] exceptions
* [ ] fetch
* [ ] classes JavaScript
* [ ] prototypes
* [ ] Event Loop

## TypeScript avançando

* [ ] declaration merging
* [ ] declaration files
* [ ] module augmentation
* [ ] decorators
* [ ] advanced generics

---

# Mentalidade final

Se você vem de C#, uma forma boa de pensar é:

```text
C#
│
├── Tipagem nominal
├── Classes
├── Interfaces
├── Generics
├── LINQ
├── Task
├── Extension Methods
└── Runtime fortemente tipado
```

Enquanto:

```text
JavaScript
│
├── Tipagem dinâmica
├── Objetos
├── Protótipos
├── Funções como valores
├── Promise
├── Array methods
├── Event Loop
└── Runtime JavaScript
```

E:

```text
TypeScript
│
├── JavaScript
│
├── Tipagem estática
├── Interfaces
├── Type aliases
├── Generics
├── Unions
├── Intersections
├── Utility Types
├── Type narrowing
├── Overloads
├── Abstract
├── Override
└── Ferramentas de verificação
```

A maneira correta de enxergar TypeScript não é:

```text
"C# com sintaxe de JavaScript"
```

É:

```text
JavaScript
    +
sistema de tipos estático
    +
ferramentas de desenvolvimento
```

---

# O que estudar depois deste arquivo

Depois de dominar este conteúdo, o caminho recomendado é:

```text
JavaScript
    ↓
TypeScript
    ↓
npm
    ↓
Node.js
    ↓
HTTP
    ↓
REST APIs
    ↓
Banco de dados
    ↓
Framework
    ↓
Testes
    ↓
Arquitetura
```

E, para um programador vindo de C#, eu recomendaria prestar atenção especial nestes assuntos:

1. **Structural Typing**
2. **Union Types**
3. **Narrowing**
4. **Generics**
5. **Utility Types**
6. **JavaScript prototypes**
7. **Closures**
8. **Event Loop**
9. **Promise**
10. **Módulos ES**
11. **Type Erasure**
12. **Diferença entre compile-time e runtime**

Esses pontos são justamente onde a experiência prévia em C# ajuda, mas também pode induzir você a pensar em TypeScript de maneira errada.
