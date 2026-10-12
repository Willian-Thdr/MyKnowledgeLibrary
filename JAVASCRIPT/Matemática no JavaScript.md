# Matemática no JavaScript — Guia de Referência Completo

## Sumário

1. Operadores aritméticos
2. Incremento e decremento
3. Operadores unários
4. Operadores de atribuição
5. Precedência dos operadores
6. Objeto `Math`
7. Arredondamento
8. Valor absoluto, mínimo e máximo
9. Potências e raízes
10. Logaritmos e exponenciais
11. Trigonometria
12. Números aleatórios
13. Constantes matemáticas
14. Operadores relacionais e lógicos
15. Operadores bit a bit
16. Particularidades numéricas do JavaScript
17. Fórmulas matemáticas implementadas em JavaScript
18. Referência dos métodos matemáticos
19. Exercícios práticos

---

## 1. Operadores aritméticos

Os operadores aritméticos permitem executar operações matemáticas diretamente.

| Operador | Nome | Exemplo | Resultado |
|---|---|---|---:|
| `+` | Adição | `10 + 3` | `13` |
| `-` | Subtração | `10 - 3` | `7` |
| `*` | Multiplicação | `10 * 3` | `30` |
| `/` | Divisão | `10 / 4` | `2.5` |
| `%` | Resto da divisão | `10 % 4` | `2` |
| `**` | Exponenciação | `2 ** 3` | `8` |

### 1.1. Adição e concatenação

```javascript
console.log(10 + 5);   // 15
console.log("10" + 5); // "105"
```

O operador `+` também concatena strings.

### 1.2. Subtração

```javascript
const resultado = 20 - 8;
console.log(resultado); // 12
```

### 1.3. Multiplicação

```javascript
const area = 8 * 5;
console.log(area); // 40
```

### 1.4. Divisão

```javascript
console.log(20 / 4); // 5
console.log(10 / 4); // 2.5
```

JavaScript não realiza divisão inteira automaticamente.

### 1.5. Resto da divisão: `%`

O operador `%` retorna o resto da divisão entre dois números.

```javascript
console.log(10 % 3); // 1
console.log(12 % 4); // 0
console.log(17 % 5); // 2
```

Aplicação: verificar se um número é par.

```javascript
const numero = 14;

if (numero % 2 === 0) {
    console.log("Par");
} else {
    console.log("Ímpar");
}
```

**Importante:** `%` não calcula diretamente uma porcentagem.

Para calcular 20% de 150:

```javascript
const resultado = 150 * (20 / 100);

console.log(resultado); // 30
```

### 1.6. Exponenciação: `**`

Representa uma potência.

```javascript
console.log(2 ** 3);   // 8
console.log(5 ** 2);   // 25
console.log(10 ** -2); // 0.01
```

Também existe `Math.pow(base, expoente)`:

```javascript
console.log(Math.pow(2, 3)); // 8
```

O operador `**` costuma ser a forma mais simples.

---

## 2. Incremento e decremento

| Operador | Significado |
|---|---|
| `++` | Incrementa em 1 |
| `--` | Decrementa em 1 |

```javascript
let numero = 10;

numero++;
console.log(numero); // 11

numero--;
console.log(numero); // 10
```

### 2.1. Prefixo: `++x`

O incremento acontece antes de a expressão retornar seu valor.

```javascript
let x = 5;

console.log(++x); // 6
```

### 2.2. Sufixo: `x++`

A expressão retorna o valor anterior e depois incrementa a variável.

```javascript
let x = 5;

console.log(x++); // 5
console.log(x);   // 6
```

O mesmo princípio vale para `--`.

---

## 3. Operadores unários

Operadores unários atuam sobre um único operando.

### 3.1. Negação numérica: `-`

```javascript
const x = 10;

console.log(-x); // -10
```

### 3.2. Conversão numérica: `+`

O operador unário `+` tenta converter um valor em número.

```javascript
console.log(+"25");    // 25
console.log(+"3.14");  // 3.14
console.log(+true);    // 1
console.log(+"texto"); // NaN
```

Útil para converter valores recebidos de formulários:

```javascript
const campo = document.querySelector("#idade");
const idade = +campo.value;
```

Verifique se a conversão produziu um número válido quando necessário:

```javascript
if (Number.isFinite(idade)) {
    console.log("Número válido");
}
```

---

## 4. Operadores de atribuição

Permitem atualizar variáveis sem repetir toda a expressão.

| Operador | Equivalente |
|---|---|
| `x += 5` | `x = x + 5` |
| `x -= 5` | `x = x - 5` |
| `x *= 5` | `x = x * 5` |
| `x /= 5` | `x = x / 5` |
| `x %= 5` | `x = x % 5` |
| `x **= 5` | `x = x ** 5` |

Exemplo:

```javascript
let pontos = 100;

pontos += 20; // 120
pontos -= 10; // 110
pontos *= 2;  // 220
pontos /= 2;  // 110
```

Também existem operadores de atribuição bit a bit, como `&=`, `|=`, `^=`, `<<=`, `>>=` e `>>>=`.

---

## 5. Precedência dos operadores

A precedência determina a ordem em que as operações são realizadas.

```javascript
console.log(2 + 3 * 4);   // 14
console.log((2 + 3) * 4); // 20
```

Multiplicação e divisão têm precedência sobre adição e subtração.

A exponenciação é associativa à direita:

```javascript
console.log(2 ** 3 ** 2); // 512
```

Equivale a:

```javascript
console.log(2 ** (3 ** 2)); // 512
```

Use parênteses para tornar expressões complexas mais legíveis.

---

## 6. Objeto `Math`

O objeto global `Math` fornece constantes e funções matemáticas.

Sintaxe geral:

```javascript
Math.nomeDaFuncao(argumentos);
```

Exemplo:

```javascript
console.log(Math.sqrt(81)); // 9
```

Os métodos de `Math` são estáticos: não é necessário criar uma instância do objeto.

Documentação: https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Global_Objects/Math

---

## 7. Arredondamento

| Método | Finalidade |
|---|---|
| `Math.round(x)` | Arredonda para o inteiro mais próximo |
| `Math.floor(x)` | Arredonda para baixo, em direção a menos infinito |
| `Math.ceil(x)` | Arredonda para cima, em direção a mais infinito |
| `Math.trunc(x)` | Remove a parte decimal em direção a zero |

### 7.1. `Math.round()`

```javascript
Math.round(4.3); // 4
Math.round(4.7); // 5
Math.round(4.5); // 5
```

### 7.2. `Math.floor()`

```javascript
Math.floor(4.9);  // 4
Math.floor(-4.1); // -5
```

### 7.3. `Math.ceil()`

```javascript
Math.ceil(4.1);  // 5
Math.ceil(-4.1); // -4
```

### 7.4. `Math.trunc()`

```javascript
Math.trunc(4.9);  // 4
Math.trunc(-4.9); // -4
```

### 7.5. Arredondar para determinado número de casas decimais

```javascript
const valor = 3.14159;
const casas = 2;

const arredondado =
    Math.round(valor * 10 ** casas) / 10 ** casas;

console.log(arredondado); // 3.14
```

Para formatar um número com uma quantidade fixa de casas decimais:

```javascript
console.log((3.1).toFixed(2)); // "3.10"
```

`toFixed()` retorna uma string, não um número.

---

## 8. Valor absoluto, mínimo e máximo

| Método | Finalidade | Exemplo |
|---|---|---|
| `Math.abs(x)` | Valor absoluto | `Math.abs(-12)` → `12` |
| `Math.min(...)` | Menor argumento | `Math.min(4, 8, 2)` → `2` |
| `Math.max(...)` | Maior argumento | `Math.max(4, 8, 2)` → `8` |

### 8.1. Valor absoluto

O valor absoluto representa a distância de um número até zero.

```javascript
console.log(Math.abs(-25)); // 25
console.log(Math.abs(25));  // 25
```

Diferença absoluta entre dois valores:

```javascript
const a = 35;
const b = 20;

console.log(Math.abs(a - b)); // 15
```

### 8.2. Mínimo e máximo

```javascript
console.log(Math.min(10, 20, 5, 30)); // 5
console.log(Math.max(10, 20, 5, 30)); // 30
```

### 8.3. Limitar um valor a um intervalo

O padrão conhecido como *clamping* limita um valor a um intervalo definido.

```javascript
const tamanho = 150;

const limitado = Math.min(100, Math.max(12, tamanho));

console.log(limitado); // 100
```

Nesse exemplo, o resultado fica entre 12 e 100.

Aplicações: tamanho de fontes, volume, barras de progresso e posições de elementos.

---

## 9. Potências e raízes

| Operação | Sintaxe | Exemplo |
|---|---|---|
| Potência | `x ** y` | `2 ** 4` → `16` |
| Potência por função | `Math.pow(x, y)` | `Math.pow(2, 4)` → `16` |
| Raiz quadrada | `Math.sqrt(x)` | `Math.sqrt(49)` → `7` |
| Raiz cúbica | `Math.cbrt(x)` | `Math.cbrt(27)` → `3` |
| Hipotenusa / norma | `Math.hypot(...)` | `Math.hypot(3, 4)` → `5` |

### 9.1. Raiz de índice arbitrário

A raiz de índice `n` pode ser expressa por uma potência fracionária:

\[
\sqrt[n]{x}=x^{1/n}
\]

```javascript
const raizquarta = 81 ** (1 / 4);

console.log(raizquarta); // aproximadamente 3
```

Para raízes cúbicas, prefira `Math.cbrt()`, que também trata corretamente valores negativos.

### 9.2. Hipotenusa

A função `Math.hypot()` calcula a raiz quadrada da soma dos quadrados dos argumentos.

\[
h=\sqrt{x^2+y^2}
\]

```javascript
console.log(Math.hypot(3, 4)); // 5
```

Pode ser utilizada para calcular distâncias entre pontos.

---

## 10. Logaritmos e exponenciais

### 10.1. Logaritmo natural: `Math.log(x)`

Calcula o logaritmo natural, cuja base é o número de Euler `e`.

\[
\ln(x)=y\iff e^y=x
\]

```javascript
console.log(Math.log(Math.E)); // 1
console.log(Math.log(1));      // 0
```

### 10.2. Logaritmo de base 10

```javascript
console.log(Math.log10(1000)); // 3
```

### 10.3. Logaritmo de base 2

```javascript
console.log(Math.log2(8)); // 3
```

### 10.4. Logaritmo em uma base arbitrária

A mudança de base é:

\[
\log_b(x)=\frac{\ln(x)}{\ln(b)}
\]

```javascript
function logBase(x, base) {
    return Math.log(x) / Math.log(base);
}

console.log(logBase(81, 3)); // 4
```

### 10.5. Exponencial: `Math.exp(x)`

Calcula \(e^x\).

```javascript
console.log(Math.exp(1)); // aproximadamente 2.71828
console.log(Math.exp(0)); // 1
```

### 10.6. Exponenciação geral

```javascript
console.log(2 ** 5); // 32
```

### 10.7. Crescimento com juros compostos

\[
M=C(1+i)^t
\]

```javascript
const capital = 1000;
const taxa = 0.05;
const tempo = 3;

const montante = capital * (1 + taxa) ** tempo;

console.log(montante); // 1157.625
```

### 10.8. Métodos adicionais

- `Math.log1p(x)`: calcula `Math.log(1 + x)` com atenção à precisão numérica.
- `Math.expm1(x)`: calcula `Math.exp(x) - 1` com atenção à precisão numérica.

---

## 11. Trigonometria

**Atenção:** os métodos trigonométricos de `Math` utilizam radianos, não graus.

| Método | Operação |
|---|---|
| `Math.sin(x)` | Seno |
| `Math.cos(x)` | Cosseno |
| `Math.tan(x)` | Tangente |
| `Math.asin(x)` | Arco-seno |
| `Math.acos(x)` | Arco-cosseno |
| `Math.atan(x)` | Arco-tangente |
| `Math.atan2(y, x)` | Ângulo considerando os sinais de duas coordenadas |

### 11.1. Conversão de graus para radianos

\[
180^\circ=\pi\text{ rad}
\]

```javascript
function grausParaRadianos(graus) {
    return graus * Math.PI / 180;
}

console.log(grausParaRadianos(180)); // Math.PI
```

### 11.2. Conversão de radianos para graus

```javascript
function radianosParaGraus(radianos) {
    return radianos * 180 / Math.PI;
}

console.log(radianosParaGraus(Math.PI)); // 180
```

### 11.3. Seno, cosseno e tangente

```javascript
const angulo = grausParaRadianos(30);

console.log(Math.sin(angulo)); // 0.5
console.log(Math.cos(angulo)); // aproximadamente 0.866
console.log(Math.tan(angulo)); // aproximadamente 0.577
```

### 11.4. Funções trigonométricas inversas

```javascript
const angulo = Math.asin(0.5);

console.log(angulo); // aproximadamente 0.5236 rad
console.log(radianosParaGraus(angulo)); // aproximadamente 30°
```

### 11.5. `Math.atan2()`

Muito útil para jogos, vetores e interfaces gráficas.

```javascript
const dx = 100;
const dy = 50;

const angulo = Math.atan2(dy, dx);
const graus = radianosParaGraus(angulo);

console.log(graus); // aproximadamente 26.565°
```

### 11.6. Funções hiperbólicas

- `Math.sinh(x)` — seno hiperbólico.
- `Math.cosh(x)` — cosseno hiperbólico.
- `Math.tanh(x)` — tangente hiperbólica.
- `Math.asinh(x)` — arco-seno hiperbólico.
- `Math.acosh(x)` — arco-cosseno hiperbólico.
- `Math.atanh(x)` — arco-tangente hiperbólico.

```javascript
console.log(Math.sinh(0)); // 0
console.log(Math.cosh(0)); // 1
console.log(Math.tanh(0)); // 0
```

---

## 12. Números aleatórios

`Math.random()` retorna um número pseudoaleatório no intervalo:

\[
0\leq x<1
\]

```javascript
console.log(Math.random());
```

### 12.1. Inteiro aleatório entre dois limites inclusivos

```javascript
function aleatorioInteiro(min, max) {
    return Math.floor(Math.random() * (max - min + 1)) + min;
}

console.log(aleatorioInteiro(1, 6));
```

Pode simular um dado de seis faces.

### 12.2. Decimal aleatório em um intervalo

```javascript
function aleatorioDecimal(min, max) {
    return Math.random() * (max - min) + min;
}

console.log(aleatorioDecimal(10, 20));
```

O resultado será maior ou igual a 10 e menor que 20.

**Segurança:** `Math.random()` não deve ser utilizado para gerar senhas ou tokens de segurança. Para isso, utilize a API `crypto.getRandomValues()`.

---

## 13. Constantes matemáticas

| Constante | Significado |
|---|---|
| `Math.PI` | Número π |
| `Math.E` | Número de Euler |
| `Math.LN2` | Logaritmo natural de 2 |
| `Math.LN10` | Logaritmo natural de 10 |
| `Math.LOG2E` | Logaritmo de e na base 2 |
| `Math.LOG10E` | Logaritmo de e na base 10 |
| `Math.SQRT2` | Raiz quadrada de 2 |
| `Math.SQRT1_2` | Raiz quadrada de 1/2 |

Exemplo: área e circunferência de um círculo.

\[
A=\pi r^2
\]

\[
C=2\pi r
\]

```javascript
const raio = 5;

const area = Math.PI * raio ** 2;
const circunferencia = 2 * Math.PI * raio;

console.log(area);          // aproximadamente 78.54
console.log(circunferencia); // aproximadamente 31.42
```

---

## 14. Operadores relacionais e lógicos

Esses operadores permitem comparar valores e construir condições matemáticas.

| Operador | Significado | Exemplo |
|---|---|---|
| `<` | Menor que | `3 < 5` → `true` |
| `>` | Maior que | `8 > 10` → `false` |
| `<=` | Menor ou igual | `5 <= 5` → `true` |
| `>=` | Maior ou igual | `6 >= 4` → `true` |
| `===` | Igualdade estrita | `5 === 5` → `true` |
| `!==` | Diferença estrita | `5 !== "5"` → `true` |

### Operadores lógicos

- `&&` — E lógico.
- `||` — OU lógico.
- `!` — negação lógica.

Exemplo:

```javascript
const nota = 8;

if (nota >= 0 && nota <= 10) {
    console.log("Nota válida");
}
```

As duas condições precisam ser verdadeiras para que o operador `&&` resulte em `true`.

---

## 15. Operadores bit a bit

Os operadores *bitwise* manipulam números por meio de suas representações binárias.

| Operador | Nome |
|---|---|
| `&` | AND bit a bit |
| `\|` | OR bit a bit |
| `^` | XOR bit a bit |
| `~` | NOT bit a bit |
| `<<` | Deslocamento à esquerda |
| `>>` | Deslocamento à direita com sinal |
| `>>>` | Deslocamento à direita sem sinal |

### 15.1. AND bit a bit

```javascript
console.log(5 & 3); // 1
```

Representação binária:

```text
5 = 101
3 = 011
    ---
    001
```

O resultado é 1 porque apenas a última posição contém o bit 1 nos dois números.

### 15.2. Deslocamento à esquerda

```javascript
console.log(5 << 1); // 10
```

Para esse exemplo, deslocar os bits uma posição à esquerda equivale a multiplicar por 2.

**Cuidado:** os operadores bit a bit normalmente convertem os operandos para inteiros de 32 bits. Não os utilize como substitutos universais da aritmética convencional.

---

## 16. Particularidades numéricas do JavaScript

### 16.1. Divisão por zero

```javascript
console.log(10 / 0);  // Infinity
console.log(-10 / 0); // -Infinity
console.log(0 / 0);   // NaN
```

- `Infinity`: infinito positivo.
- `-Infinity`: infinito negativo.
- `NaN`: resultado numérico inválido.

Verificação:

```javascript
console.log(Number.isFinite(10 / 2)); // true
console.log(Number.isFinite(10 / 0)); // false
console.log(Number.isNaN(0 / 0));     // true
```

### 16.2. Imprecisão de decimais

```javascript
console.log(0.1 + 0.2); // 0.30000000000000004
```

Isso acontece porque muitos números decimais não possuem representação binária finita.

Para comparações aproximadas:

```javascript
const resultado = 0.1 + 0.2;
const esperado = 0.3;

console.log(Math.abs(resultado - esperado) < 1e-10); // true
```

Em aplicações financeiras, considere trabalhar com unidades inteiras, como centavos, quando apropriado, ou utilizar uma biblioteca de aritmética decimal.

### 16.3. Limites dos inteiros

```javascript
console.log(Number.MAX_SAFE_INTEGER);
// 9007199254740991
```

Para inteiros maiores, existe `BigInt`:

```javascript
const enorme = 9007199254740993n;

console.log(enorme + 2n);
// 9007199254740995n
```

O sufixo `n` identifica um literal `BigInt`.

Não é permitido misturar diretamente `BigInt` e `Number` em operações aritméticas.

### 16.4. Métodos matemáticos adicionais

| Método | Finalidade |
|---|---|
| `Math.sign(x)` | Retorna o sinal do valor |
| `Math.hypot(...)` | Calcula a raiz da soma dos quadrados |
| `Math.fround(x)` | Aproxima o valor para ponto flutuante de 32 bits |
| `Math.imul(a, b)` | Multiplicação de inteiros de 32 bits |
| `Math.clz32(x)` | Conta zeros à esquerda na representação binária de 32 bits |

Exemplos:

```javascript
console.log(Math.sign(-15)); // -1
console.log(Math.hypot(3, 4)); // 5
console.log(Math.imul(3, 4)); // 12
console.log(Math.clz32(1));   // 31
```

---

## 17. Fórmulas matemáticas implementadas em JavaScript

### 17.1. Porcentagem

\[
R=x\cdot\frac{p}{100}
\]

```javascript
function porcentagem(valor, percentual) {
    return valor * percentual / 100;
}

console.log(porcentagem(200, 15)); // 30
```

Aumentar um valor em 15%:

```javascript
const valor = 200;
const resultado = valor * (1 + 15 / 100);

console.log(resultado); // 230
```

Aplicar um desconto de 15%:

```javascript
const valor = 200;
const resultado = valor * (1 - 15 / 100);

console.log(resultado); // 170
```

### 17.2. Média aritmética

\[
\bar{x}=\frac{x_1+x_2+\cdots+x_n}{n}
\]

```javascript
function media(valores) {
    if (valores.length === 0) {
        return NaN;
    }

    const soma = valores.reduce(
        (total, valor) => total + valor,
        0
    );

    return soma / valores.length;
}

console.log(media([7, 8, 9])); // 8
```

### 17.3. Distância entre dois pontos

\[
d=\sqrt{(x_2-x_1)^2+(y_2-y_1)^2}
\]

```javascript
function distancia(x1, y1, x2, y2) {
    return Math.hypot(x2 - x1, y2 - y1);
}

console.log(distancia(0, 0, 3, 4)); // 5
```

### 17.4. Área de um triângulo

\[
A=\frac{b\cdot h}{2}
\]

```javascript
function areaTriangulo(base, altura) {
    return base * altura / 2;
}

console.log(areaTriangulo(10, 6)); // 30
```

### 17.5. Regra de três simples

Em uma proporção direta:

\[
x=\frac{b\cdot c}{a}
\]

```javascript
function regraDeTres(a, b, c) {
    if (a === 0) {
        throw new Error("O divisor não pode ser zero.");
    }

    return b * c / a;
}

console.log(regraDeTres(2, 10, 5)); // 25
```

---

## 18. Referência dos principais métodos de `Math`

| Categoria | Métodos |
|---|---|
| Arredondamento | `round()`, `floor()`, `ceil()`, `trunc()` |
| Sinal e magnitude | `abs()`, `sign()` |
| Mínimo e máximo | `min()`, `max()` |
| Potências e raízes | `pow()`, `sqrt()`, `cbrt()` |
| Distâncias | `hypot()` |
| Exponenciais | `exp()`, `expm1()` |
| Logaritmos | `log()`, `log10()`, `log2()`, `log1p()` |
| Trigonometria | `sin()`, `cos()`, `tan()` |
| Trigonometria inversa | `asin()`, `acos()`, `atan()`, `atan2()` |
| Funções hiperbólicas | `sinh()`, `cosh()`, `tanh()` |
| Funções hiperbólicas inversas | `asinh()`, `acosh()`, `atanh()` |
| Aleatoriedade | `random()` |
| Precisão e operações binárias | `fround()`, `imul()`, `clz32()` |

### Referências para estudo

- MDN — objeto Math: https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Global_Objects/Math
- MDN — operadores: https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Operators
- MDN — matemática no JavaScript: https://developer.mozilla.org/pt-BR/docs/Learn_web_development/Core/Scripting/Math

---

## 19. Exercícios práticos

Tente resolver os exercícios sem consultar as respostas imediatamente.

### Exercício 1 — Resto da divisão

Calcule o resto da divisão de 47 por 6.

```javascript
console.log(47 % 6);
```

### Exercício 2 — Raiz quadrada

Calcule a raiz quadrada de 144.

```javascript
console.log(Math.sqrt(144));
```

### Exercício 3 — Arredondamento negativo

Descubra o resultado:

```javascript
console.log(Math.floor(-2.3));
```

### Exercício 4 — Porcentagem

Calcule 25% de 80.

```javascript
console.log(80 * 25 / 100);
```

### Exercício 5 — Maior valor

Encontre o maior número entre 12, 7 e 19.

```javascript
console.log(Math.max(12, 7, 19));
```

### Exercício 6 — Exponenciação

Calcule 2 elevado à quinta potência.

```javascript
console.log(2 ** 5);
```

### Gabarito

1. `5`
2. `12`
3. `-3`
4. `20`
5. `19`
6. `32`

---

## Ordem recomendada de estudo

1. Operadores aritméticos e precedência.
2. Operadores de incremento, decremento e atribuição.
3. Arredondamento, mínimo, máximo e valor absoluto.
4. Potências, raízes e porcentagens.
5. Números aleatórios e constantes.
6. Logaritmos e exponenciais.
7. Trigonometria.
8. Comparações, operadores lógicos e bit a bit.
9. Precisão numérica, `Number` e `BigInt`.
10. Implementação de fórmulas matemáticas em funções.

**Princípio fundamental:** o JavaScript não precisa possuir uma função pronta para cada fórmula matemática. Você pode combinar operadores, métodos de `Math`, variáveis e funções para implementar as fórmulas de que precisar.
