# Guia de desenvolvimento: Timer com JavaScript

## 1. Introdução

Um timer é um mecanismo responsável por controlar a passagem do tempo, podendo executar determinadas ações quando um intervalo temporal é atingido.

Em JavaScript, podemos desenvolver timers utilizando métodos nativos da linguagem, principalmente:

- `setTimeout()`: executa uma função após determinado intervalo.
- `setInterval()`: executa uma função repetidamente em intervalos definidos.
- `clearTimeout()`: cancela uma execução agendada com `setTimeout()`.
- `clearInterval()`: interrompe uma repetição iniciada com `setInterval()`.

Neste projeto, desenvolveremos um cronômetro regressivo que permitirá:

- Definir um tempo inicial.
- Iniciar a contagem regressiva.
- Pausar a contagem.
- Retomar a contagem.
- Reiniciar o cronômetro.
- Executar uma ação quando o tempo chegar a zero.

---

## 2. Estrutura do projeto

Inicialmente, criaremos três arquivos:

```text
timer/
│
├── index.html
├── style.css
└── script.js
```

Cada arquivo terá uma responsabilidade específica:

| Arquivo | Responsabilidade |
|---|---|
| `index.html` | Estrutura dos elementos da interface. |
| `style.css` | Aparência e organização visual. |
| `script.js` | Lógica e funcionamento do timer. |

---

## 3. Compreendendo os métodos temporais

Antes de desenvolver o projeto, é importante compreender como JavaScript trabalha com intervalos de tempo.

### 3.1. setInterval()

O método `setInterval()` executa uma função repetidamente, respeitando um intervalo determinado em milissegundos.

Sintaxe:

```javascript
setInterval(callback, delay);
```

Exemplo:

```javascript
setInterval(() => {
    console.log("Executando...");
}, 1000);
```

Neste exemplo, a mensagem será exibida repetidamente, aproximadamente a cada segundo.

**Importante:** o método retorna um identificador numérico que pode ser utilizado posteriormente para interromper sua execução.

```javascript
const interval = setInterval(() => {
    console.log("Executando...");
}, 1000);

clearInterval(interval);
```

O `clearInterval()` interrompe a repetição.

### 3.2. setTimeout()

O método `setTimeout()` executa uma função uma única vez, após determinado intervalo.

Sintaxe:

```javascript
setTimeout(callback, delay);
```

Exemplo:

```javascript
setTimeout(() => {
    console.log("Um segundo se passou!");
}, 1000);
```

Diferentemente de `setInterval()`, esse método não repete automaticamente a execução.

Para cancelar uma execução agendada, utilizamos `clearTimeout()`.

### 3.3. Milissegundos

JavaScript trabalha com intervalos temporais expressos em milissegundos.

A conversão funciona da seguinte maneira:

| Unidade | Equivalência |
|---|---:|
| 1 segundo | 1.000 ms |
| 1 minuto | 60.000 ms |
| 1 hora | 3.600.000 ms |
| 1 dia | 86.400.000 ms |

Essa informação será importante para converter o tempo definido pelo usuário em um valor que o JavaScript possa processar.

---

## 4. Desenvolvendo a interface HTML

Primeiramente, criaremos os elementos que serão utilizados para apresentar e controlar o timer.

Arquivo: `index.html`

```html
<!DOCTYPE html>
<html lang="pt-BR">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <title>JavaScript Timer</title>

    <link rel="stylesheet" href="style.css">

    <script src="script.js" defer></script>
</head>

<body>

    <main class="timer">

        <h1>Countdown Timer</h1>

        <div id="display">
            00:00
        </div>

        <div class="configuration">

            <input
                type="number"
                id="minutes"
                min="0"
                max="999"
                value="1"
                placeholder="Minutos"
            >

            <input
                type="number"
                id="seconds"
                min="0"
                max="59"
                value="0"
                placeholder="Segundos"
            >

        </div>

        <div class="controls">

            <button id="start">Iniciar</button>

            <button id="pause">Pausar</button>

            <button id="reset">Reiniciar</button>

        </div>

    </main>

</body>

</html>
```

### 4.1. Explicação dos elementos

- `main`: representa o conteúdo principal da aplicação.
- `h1`: apresenta o título.
- `div#display`: apresenta o tempo restante.
- `input#minutes`: recebe os minutos.
- `input#seconds`: recebe os segundos.
- `button#start`: inicia a contagem.
- `button#pause`: pausa a contagem.
- `button#reset`: reinicia o cronômetro.

O atributo `defer` utilizado na tag `<script>` faz com que o navegador aguarde a análise do HTML antes de executar o JavaScript externo.

---

## 5. Desenvolvendo a estilização CSS

Agora, criaremos uma interface simples para facilitar a visualização do cronômetro.

Arquivo: `style.css`

```css
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

body {
    display: flex;
    justify-content: center;
    align-items: center;

    min-height: 100vh;

    background-color: #151515;
    color: white;

    font-family: Arial, sans-serif;
}

.timer {
    display: flex;
    flex-direction: column;
    align-items: center;

    gap: 25px;

    padding: 40px;

    background-color: #252525;
    border-radius: 15px;
}

#display {
    font-size: 60px;
    font-weight: bold;

    font-family: monospace;
}

.configuration {
    display: flex;
    gap: 10px;
}

input {
    width: 100px;
    padding: 10px;

    text-align: center;
    font-size: 16px;
}

.controls {
    display: flex;
    gap: 10px;
}

button {
    padding: 10px 15px;

    border: none;
    border-radius: 5px;

    cursor: pointer;
}

button:hover {
    opacity: 0.8;
}
```

---

## 6. Desenvolvendo a lógica JavaScript

Esta é a parte principal do projeto.

Arquivo: `script.js`

### 6.1. Selecionando os elementos HTML

Primeiramente, precisamos estabelecer uma comunicação entre JavaScript e HTML.

Para isso, utilizaremos `document.getElementById()`.

```javascript
const display = document.getElementById("display");

const minutesInput = document.getElementById("minutes");
const secondsInput = document.getElementById("seconds");

const startButton = document.getElementById("start");
const pauseButton = document.getElementById("pause");
const resetButton = document.getElementById("reset");
```

Cada variável representa um elemento da interface.

Dessa maneira, podemos acessar seus valores, modificar seus conteúdos e adicionar comportamentos.

### 6.2. Criando as variáveis de controle

Agora, precisamos armazenar algumas informações sobre o estado atual do timer.

```javascript
let remainingTime = 0;

let interval = null;

let isRunning = false;
```

Suas responsabilidades são:

| Variável | Função |
|---|---|
| `remainingTime` | Armazena o tempo restante em segundos. |
| `interval` | Armazena o identificador do intervalo. |
| `isRunning` | Indica se o timer está em execução. |

O valor `null` indica que não existe um intervalo ativo armazenado inicialmente.

### 6.3. Convertendo o tempo para segundos

O usuário fornecerá minutos e segundos separadamente.

Precisamos converter esses valores para uma unidade única.

```javascript
function getTimeInSeconds() {

    const minutes = Number(minutesInput.value);
    const seconds = Number(secondsInput.value);

    return (minutes * 60) + seconds;

}
```

Exemplo:

Se o usuário definir:

- 2 minutos;
- 30 segundos.

O resultado será:

```javascript
(2 * 60) + 30;

// Resultado: 150 segundos
```

Trabalhar com uma única unidade facilita os cálculos.

### 6.4. Formatando o tempo

O JavaScript armazenará o tempo em segundos, mas queremos apresentá-lo no formato `MM:SS`.

Para isso, criaremos uma função responsável pela conversão.

```javascript
function formatTime(totalSeconds) {

    const minutes = Math.floor(totalSeconds / 60);

    const seconds = totalSeconds % 60;

    const formattedMinutes = String(minutes).padStart(2, "0");

    const formattedSeconds = String(seconds).padStart(2, "0");

    return `${formattedMinutes}:${formattedSeconds}`;

}
```

Compreendendo os métodos:

**Math.floor()**

Arredonda um número para baixo, eliminando sua parte decimal.

Exemplo:

```javascript
Math.floor(125 / 60);

// Resultado: 2
```

**Operador de módulo (%)**

Retorna o resto de uma divisão.

Exemplo:

```javascript
125 % 60;

// Resultado: 5
```

**String.padStart()**

Adiciona caracteres no início de uma string até atingir determinado comprimento.

Exemplo:

```javascript
String(5).padStart(2, "0");

// Resultado: "05"
```

Assim, 125 segundos serão apresentados como `02:05`.

### 6.5. Atualizando o display

Agora, precisamos apresentar o tempo na interface.

```javascript
function updateDisplay() {

    display.textContent = formatTime(remainingTime);

}
```

O atributo `textContent` modifica o conteúdo textual de um elemento HTML.

Sempre que o tempo mudar, chamaremos essa função para atualizar a interface.

### 6.6. Iniciando o timer

Agora implementaremos a função responsável pela contagem regressiva.

```javascript
function startTimer() {

    if (isRunning) return;

    if (remainingTime <= 0) {

        remainingTime = getTimeInSeconds();

    }

    if (remainingTime <= 0) return;

    isRunning = true;

    interval = setInterval(() => {

        remainingTime--;

        updateDisplay();

        if (remainingTime <= 0) {

            clearInterval(interval);

            interval = null;

            isRunning = false;

            alert("Tempo encerrado!");

        }

    }, 1000);

}
```

Vamos analisar seu funcionamento.

**1. Verificação de execução**

```javascript
if (isRunning) return;
```

Impede que o usuário inicie vários intervalos simultaneamente.

**2. Recuperação do tempo**

```javascript
if (remainingTime <= 0) {
    remainingTime = getTimeInSeconds();
}
```

Caso o cronômetro esteja zerado, recuperamos o tempo definido nos campos de entrada.

**3. Alteração do estado**

```javascript
isRunning = true;
```

Indica que o timer está em execução.

**4. Criação do intervalo**

```javascript
interval = setInterval(() => {
    remainingTime--;
}, 1000);
```

A cada intervalo, diminuímos um segundo do tempo restante.

**5. Verificação do encerramento**

Quando o tempo chega a zero, interrompemos o intervalo e executamos uma ação.

### 6.7. Pausando o timer

Para pausar a contagem, basta interromper o intervalo sem modificar o tempo restante.

```javascript
function pauseTimer() {

    if (!isRunning) return;

    clearInterval(interval);

    interval = null;

    isRunning = false;

}
```

Observe que não modificamos `remainingTime`.

Isso permite retomar a contagem exatamente de onde ela foi interrompida.

### 6.8. Reiniciando o timer

A função de reinicialização deverá interromper qualquer intervalo ativo e recuperar o tempo definido pelo usuário.

```javascript
function resetTimer() {

    clearInterval(interval);

    interval = null;

    isRunning = false;

    remainingTime = getTimeInSeconds();

    updateDisplay();

}
```

Diferentemente da pausa, o reinício modifica o tempo restante.

---

## 7. Conectando os botões

As funções já estão desenvolvidas, mas ainda precisamos associá-las aos respectivos botões.

Utilizaremos `addEventListener()`.

```javascript
startButton.addEventListener("click", startTimer);

pauseButton.addEventListener("click", pauseTimer);

resetButton.addEventListener("click", resetTimer);
```

O método `addEventListener()` permite registrar uma função que será executada quando determinado evento ocorrer.

Neste caso, estamos utilizando o evento `click`.

### 7.1. Inicializando o display

Por fim, precisamos apresentar o tempo inicial assim que a página for carregada.

```javascript
remainingTime = getTimeInSeconds();

updateDisplay();
```

---

## 8. Código JavaScript completo

Abaixo está a implementação completa, reunindo todas as funções anteriores.

```javascript
const display = document.getElementById("display");

const minutesInput = document.getElementById("minutes");
const secondsInput = document.getElementById("seconds");

const startButton = document.getElementById("start");
const pauseButton = document.getElementById("pause");
const resetButton = document.getElementById("reset");

let remainingTime = 0;

let interval = null;

let isRunning = false;


function getTimeInSeconds() {

    const minutes = Number(minutesInput.value);
    const seconds = Number(secondsInput.value);

    return (minutes * 60) + seconds;

}


function formatTime(totalSeconds) {

    const minutes = Math.floor(totalSeconds / 60);

    const seconds = totalSeconds % 60;

    const formattedMinutes = String(minutes).padStart(2, "0");

    const formattedSeconds = String(seconds).padStart(2, "0");

    return `${formattedMinutes}:${formattedSeconds}`;

}


function updateDisplay() {

    display.textContent = formatTime(remainingTime);

}


function startTimer() {

    if (isRunning) return;

    if (remainingTime <= 0) {

        remainingTime = getTimeInSeconds();

    }

    if (remainingTime <= 0) return;

    isRunning = true;

    interval = setInterval(() => {

        remainingTime--;

        updateDisplay();

        if (remainingTime <= 0) {

            clearInterval(interval);

            interval = null;

            isRunning = false;

            alert("Tempo encerrado!");

        }

    }, 1000);

}


function pauseTimer() {

    if (!isRunning) return;

    clearInterval(interval);

    interval = null;

    isRunning = false;

}


function resetTimer() {

    clearInterval(interval);

    interval = null;

    isRunning = false;

    remainingTime = getTimeInSeconds();

    updateDisplay();

}


startButton.addEventListener("click", startTimer);

pauseButton.addEventListener("click", pauseTimer);

resetButton.addEventListener("click", resetTimer);


remainingTime = getTimeInSeconds();

updateDisplay();
```

---

## 9. Limitações e melhorias possíveis

O projeto apresentado é funcional para fins didáticos, mas possui algumas limitações.

### 9.1. Precisão temporal

O `setInterval()` não garante que sua função será executada exatamente a cada milissegundo ou segundo solicitado.

O navegador pode atrasar sua execução devido a:

- Sobrecarga do processamento.
- Outras tarefas na fila de execução.
- Aba em segundo plano.
- Limitações de gerenciamento de recursos.

Portanto, para aplicações que exigem maior precisão, não é recomendável depender exclusivamente da quantidade de execuções do `setInterval()`.

Uma abordagem mais robusta utiliza `Date.now()` para calcular o tempo efetivamente transcorrido.

### 9.2. Utilizando Date.now()

O método `Date.now()` retorna o instante atual em milissegundos desde 1º de janeiro de 1970, no padrão Unix Epoch.

Uma implementação mais precisa pode armazenar o instante em que o timer deverá terminar:

```javascript
const endTime = Date.now() + (remainingTime * 1000);
```

Depois, a cada atualização:

```javascript
remainingTime = Math.max(
    0,
    Math.ceil((endTime - Date.now()) / 1000)
);
```

Dessa maneira, mesmo que o navegador atrase uma atualização, o cálculo continuará considerando o tempo real transcorrido.

### 9.3. Melhorias futuras

Depois de compreender a implementação básica, você poderá desenvolver novas funcionalidades:

- [ ] Adicionar um botão de continuar.
- [ ] Criar um cronômetro progressivo.
- [ ] Adicionar horas ao formato de exibição.
- [ ] Implementar notificações sonoras.
- [ ] Criar uma barra de progresso.
- [ ] Permitir múltiplos timers simultâneos.
- [ ] Adicionar animações ao display.
- [ ] Salvar configurações utilizando `localStorage`.
- [ ] Criar uma interface responsiva.
- [ ] Implementar notificações do navegador.

---

## 10. Referências para aprofundamento

A documentação da Mozilla Developer Network (MDN) é uma excelente referência para estudar os recursos utilizados neste projeto.

- [MDN — setInterval()](https://developer.mozilla.org/en-US/docs/Web/API/Window/setInterval)
- [MDN — setTimeout()](https://developer.mozilla.org/en-US/docs/Web/API/Window/setTimeout)
- [MDN — clearInterval()](https://developer.mozilla.org/en-US/docs/Web/API/Window/clearInterval)
- [MDN — Date.now()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/now)
- [MDN — addEventListener()](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/addEventListener)
- [MDN — Math.floor()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math/floor)

**Conclusão:** um timer é um excelente exercício para compreender manipulação do DOM, funções, variáveis, eventos, intervalos temporais e controle de estado em JavaScript. Embora sua implementação básica seja relativamente simples, existem diversas possibilidades de aperfeiçoamento arquitetural e funcional.