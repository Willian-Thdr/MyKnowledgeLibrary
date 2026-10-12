# 🎬 Animações 2D — CSS + JavaScript

# 1. 📈 Aumentar / Diminuir

### CSS

```css
.elemento {
    transform: scale(1);
    transition: transform 0.3s ease;
}

.elemento:hover {
    transform: scale(1.1);
}
```

| Código | O que faz |
|---|---|
| `scale(1)` | Tamanho normal |
| `scale(1.1)` | Aumenta 10% |
| `scale(0.8)` | Diminui para 80% |
| `transition` | Faz a mudança ser animada |

---

# 2. ↔️ Mover horizontalmente

### Para a direita

```css
.elemento {
    transform: translateX(100px);
}
```

`translateX(100px)` → move 100px para a direita.

### Para a esquerda

```css
.elemento {
    transform: translateX(-100px);
}
```

`translateX(-100px)` → move 100px para a esquerda.

### Animação

```css
.elemento {
    transform: translateX(0);
    transition: transform 0.5s ease;
}

.elemento:hover {
    transform: translateX(100px);
}
```

---

# 3. ↕️ Mover verticalmente

### Para baixo

```css
.elemento {
    transform: translateY(100px);
}
```

`translateY(100px)` → move para baixo.

### Para cima

```css
.elemento {
    transform: translateY(-100px);
}
```

`translateY(-100px)` → move para cima.

### Animação

```css
.elemento {
    transform: translateY(0);
    transition: transform 0.5s ease;
}

.elemento:hover {
    transform: translateY(-20px);
}
```

---

# 4. ↗️ Mover em duas direções

```css
.elemento {
    transform: translate(50px, -30px);
}
```

`translate(X, Y)`:

- `50px` → direita
- `-30px` → cima

### Exemplo

```css
.elemento:hover {
    transform: translate(50px, -30px);
}
```

---

# 5. 🔄 Girar

```css
.elemento {
    transform: rotate(45deg);
}
```

`rotate(45deg)` → gira 45 graus.

### Sentido contrário

```css
.elemento {
    transform: rotate(-45deg);
}
```

### Animação

```css
.elemento {
    transform: rotate(0deg);
    transition: transform 0.5s ease;
}

.elemento:hover {
    transform: rotate(180deg);
}
```

---

# 6. 🔃 Girar continuamente

```css
.elemento {
    animation: girar 2s linear infinite;
}

@keyframes girar {

    from {
        transform: rotate(0deg);
    }

    to {
        transform: rotate(360deg);
    }

}
```

| Código | O que faz |
|---|---|
| `animation` | Executa uma animação |
| `2s` | Duração |
| `linear` | Velocidade constante |
| `infinite` | Repete infinitamente |
| `360deg` | Uma volta completa |

---

# 7. 👻 Aparecer / Desaparecer

### CSS

```css
.elemento {
    opacity: 1;
    transition: opacity 0.3s ease;
}

.elemento.escondido {
    opacity: 0;
}
```

| Código | O que faz |
|---|---|
| `opacity: 1` | Totalmente visível |
| `opacity: 0` | Invisível |
| `transition` | Suaviza a mudança |

### JavaScript

```js
elemento.classList.toggle("escondido");
```

`toggle()` → adiciona a classe se ela não existir e remove se já existir.

---

# 8. ⬆️ Aparecer vindo de baixo

```css
.elemento {
    opacity: 0;
    transform: translateY(30px);

    transition:
        opacity 0.4s ease,
        transform 0.4s ease;
}

.elemento.visivel {
    opacity: 1;
    transform: translateY(0);
}
```

Resultado:

```text
    elemento escondido

         ↓

    ┌─────────┐
    │ elemento│
    └─────────┘
```

O elemento começa 30px abaixo e sobe para a posição original.

---

# 9. ⬇️ Aparecer vindo de cima

```css
.elemento {
    opacity: 0;
    transform: translateY(-30px);

    transition:
        opacity 0.4s ease,
        transform 0.4s ease;
}

.elemento.visivel {
    opacity: 1;
    transform: translateY(0);
}
```

---

# 10. ⬅️ Aparecer vindo da direita

```css
.elemento {
    opacity: 0;
    transform: translateX(50px);

    transition:
        opacity 0.4s ease,
        transform 0.4s ease;
}

.elemento.visivel {
    opacity: 1;
    transform: translateX(0);
}
```

---

# 11. ➡️ Aparecer vindo da esquerda

```css
.elemento {
    opacity: 0;
    transform: translateX(-50px);

    transition:
        opacity 0.4s ease,
        transform 0.4s ease;
}

.elemento.visivel {
    opacity: 1;
    transform: translateX(0);
}
```

---

# 12. 🔍 Abrir aumentando

```css
.elemento {
    opacity: 0;
    transform: scale(0.8);

    transition:
        opacity 0.3s ease,
        transform 0.3s ease;
}

.elemento.aberto {
    opacity: 1;
    transform: scale(1);
}
```

O elemento começa menor e cresce até o tamanho normal.

---

# 13. 🔎 Fechar diminuindo

```css
.elemento {
    transform: scale(1);
    opacity: 1;

    transition:
        transform 0.3s ease,
        opacity 0.3s ease;
}

.elemento.fechando {
    transform: scale(0.8);
    opacity: 0;
}
```

---

# 14. 📐 Expandir horizontalmente

```css
.elemento {
    width: 100px;

    transition: width 0.5s ease;
}

.elemento.expandido {
    width: 300px;
}
```

O elemento passa de:

```text
[████████]
```

para:

```text
[████████████████████████]
```

---

# 15. 📏 Expandir verticalmente

```css
.elemento {
    height: 50px;

    transition: height 0.5s ease;
}

.elemento.expandido {
    height: 200px;
}
```

---

# 16. 📦 Expandir usando `max-height`

Útil para menus, textos e painéis.

```css
.elemento {
    max-height: 0;
    overflow: hidden;

    transition: max-height 0.5s ease;
}

.elemento.aberto {
    max-height: 500px;
}
```

`overflow: hidden` → impede o conteúdo de aparecer fora da área.

---

# 17. 📦 Expandir automaticamente com JavaScript

Quando você não sabe a altura do conteúdo:

```js
if (elemento.style.maxHeight) {

    elemento.style.maxHeight = null;

} else {

    elemento.style.maxHeight =
        elemento.scrollHeight + "px";

}
```

`scrollHeight` → altura real necessária para mostrar todo o conteúdo.

---

# 18. 🖱️ Aumentar ao passar o mouse

```css
.elemento {
    transition: transform 0.2s ease;
}

.elemento:hover {
    transform: scale(1.05);
}
```

---

# 19. 🖱️ Levantar ao passar o mouse

```css
.elemento {
    transition: transform 0.2s ease;
}

.elemento:hover {
    transform: translateY(-10px);
}
```

Muito usado em cards.

---

# 20. 🖱️ Levantar + aumentar

```css
.elemento {
    transition: transform 0.3s ease;
}

.elemento:hover {
    transform:
        translateY(-10px)
        scale(1.05);
}
```

Combina duas transformações.

---

# 21. 🎯 Pressionar botão

```css
.botao {
    transition: transform 0.1s ease;
}

.botao:active {
    transform: scale(0.95);
}
```

`:active` → estado enquanto o elemento está sendo pressionado.

---

# 22. ↘️ Inclinar

```css
.elemento {
    transform: skew(10deg);
}
```

`skew()` → inclina o elemento.

### Horizontal

```css
transform: skewX(10deg);
```

### Vertical

```css
transform: skewY(10deg);
```

---

# 23. 💥 Pulsar

```css
.elemento {
    animation: pulsar 1.5s infinite;
}

@keyframes pulsar {

    0% {
        transform: scale(1);
    }

    50% {
        transform: scale(1.1);
    }

    100% {
        transform: scale(1);
    }

}
```

O elemento cresce e volta ao tamanho original continuamente.

---

# 24. 🫨 Tremer

```css
.elemento {
    animation: tremer 0.4s;
}

@keyframes tremer {

    0% {
        transform: translateX(0);
    }

    25% {
        transform: translateX(-5px);
    }

    50% {
        transform: translateX(5px);
    }

    75% {
        transform: translateX(-5px);
    }

    100% {
        transform: translateX(0);
    }

}
```

Útil para indicar erro em um formulário.

---

# 25. 🪂 Quicar

```css
.elemento {
    animation: quicar 1s;
}

@keyframes quicar {

    0% {
        transform: translateY(0);
    }

    30% {
        transform: translateY(-30px);
    }

    50% {
        transform: translateY(0);
    }

    70% {
        transform: translateY(-15px);
    }

    100% {
        transform: translateY(0);
    }

}
```

---

# 26. 🌊 Flutuar

```css
.elemento {
    animation: flutuar 2s ease-in-out infinite;
}

@keyframes flutuar {

    0% {
        transform: translateY(0);
    }

    50% {
        transform: translateY(-10px);
    }

    100% {
        transform: translateY(0);
    }

}
```

---

# 27. 🎞️ Animação com vários movimentos

```css
.elemento {
    animation: movimento 2s ease-in-out;
}

@keyframes movimento {

    0% {
        transform: translateX(0) rotate(0deg);
    }

    25% {
        transform: translateX(100px) rotate(20deg);
    }

    50% {
        transform: translateX(200px) rotate(0deg);
    }

    75% {
        transform: translateX(100px) rotate(-20deg);
    }

    100% {
        transform: translateX(0) rotate(0deg);
    }

}
```

`@keyframes` permite definir vários estados da animação.

---

# 28. 🌀 Combinar escala + rotação + movimento

```css
.elemento {
    transition: transform 0.5s ease;
}

.elemento:hover {
    transform:
        translate(20px, -20px)
        rotate(10deg)
        scale(1.1);
}
```

---

# 29. 🎨 Animar cor

```css
.elemento {
    background: black;

    transition: background 0.3s ease;
}

.elemento:hover {
    background: white;
}
```

---

# 30. 🟢 Animar várias propriedades

```css
.elemento {
    opacity: 1;
    transform: scale(1);
    background: black;

    transition:
        opacity 0.3s ease,
        transform 0.3s ease,
        background 0.3s ease;
}

.elemento:hover {
    opacity: 0.8;
    transform: scale(1.05);
    background: gray;
}
```

---

# 31. 🔄 Abrir / fechar com JavaScript

### HTML

```html
<button id="botao">Abrir</button>

<div id="painel">
    Conteúdo
</div>
```

### CSS

```css
#painel {
    opacity: 0;
    transform: scale(0.8);

    pointer-events: none;

    transition:
        opacity 0.3s ease,
        transform 0.3s ease;
}

#painel.aberto {
    opacity: 1;
    transform: scale(1);

    pointer-events: auto;
}
```

### JavaScript

```js
const botao = document.getElementById("botao");
const painel = document.getElementById("painel");

botao.addEventListener("click", () => {

    painel.classList.toggle("aberto");

});
```

---

# 32. ➡️ Menu lateral

### CSS

```css
.menu {
    position: fixed;

    left: 0;
    top: 0;

    width: 250px;
    height: 100vh;

    transform: translateX(-100%);

    transition: transform 0.3s ease;
}

.menu.aberto {
    transform: translateX(0);
}
```

### JavaScript

```js
botao.addEventListener("click", () => {

    menu.classList.toggle("aberto");

});
```

O menu começa fora da tela:

```text
← [ MENU ]
```

e entra:

```text
[ MENU ] →
```

---

# 33. 🪟 Modal

### CSS

```css
.modal {
    position: fixed;

    inset: 0;

    display: flex;
    justify-content: center;
    align-items: center;

    background: rgba(0, 0, 0, 0.5);

    opacity: 0;
    pointer-events: none;

    transition: opacity 0.3s ease;
}

.modal.aberto {
    opacity: 1;
    pointer-events: auto;
}

.modal-conteudo {
    transform: scale(0.8);

    transition: transform 0.3s ease;
}

.modal.aberto .modal-conteudo {
    transform: scale(1);
}
```

---

# 34. ⚙️ Web Animations API

JavaScript pode criar uma animação diretamente:

```js
elemento.animate(

    [
        {
            opacity: 0,
            transform: "translateY(-30px)"
        },

        {
            opacity: 1,
            transform: "translateY(0)"
        }
    ],

    {
        duration: 500,
        easing: "ease-out",
        fill: "forwards"
    }

);
```

### Estrutura

```js
elemento.animate(
    [estados],
    [configuração]
);
```

---

# 35. ⏱️ Propriedades importantes de `transition`

```css
transition: transform 0.3s ease;
```

### Duração

```css
transition-duration: 0.3s;
```

### Curva

```css
transition-timing-function: ease;
```

### Atraso

```css
transition-delay: 0.5s;
```

### Tudo junto

```css
transition:
    transform 0.3s ease 0.1s;
```

Significa:

```text
transform
   ↓
0.3s de duração
   ↓
ease
   ↓
0.1s de atraso
```

---

# 36. 🧭 Curvas de animação

```css
ease
```

Suave no começo e no final.

```css
ease-in
```

Começa devagar.

```css
ease-out
```

Termina devagar.

```css
ease-in-out
```

Começa e termina devagar.

```css
linear
```

Velocidade constante.

---

# 37. 🎚️ Curva personalizada

```css
transition:
    transform 0.5s
    cubic-bezier(0.2, 0.8, 0.2, 1);
```

`cubic-bezier()` permite criar uma curva personalizada de velocidade.

---

# 38. 🎬 `@keyframes` básico

```css
.elemento {
    animation: minhaAnimacao 2s;
}

@keyframes minhaAnimacao {

    from {
        transform: translateX(0);
    }

    to {
        transform: translateX(100px);
    }

}
```

---

# 39. 🔁 Configurações de `animation`

```css
.elemento {
    animation:
        minhaAnimacao
        2s
        ease-in-out
        0s
        infinite
        alternate;
}
```

Ordem:

```text
nome
 ↓
duração
 ↓
curva
 ↓
delay
 ↓
quantidade de repetições
 ↓
direção
```

---

# 40. 🔁 Direções de animação

```css
animation-direction: normal;
```

Executa normalmente.

```css
animation-direction: reverse;
```

Executa ao contrário.

```css
animation-direction: alternate;
```

Vai e volta.

```css
animation-direction: alternate-reverse;
```

Começa ao contrário e depois volta.

---

# 41. 🛑 Pausar animação

```css
.elemento:hover {
    animation-play-state: paused;
}
```

`paused` → pausa.

```css
animation-play-state: running;
```

`running` → executa.

---

# 42. 🧩 Transformações mais importantes

```css
transform: translateX(100px);
```

Move horizontalmente.

```css
transform: translateY(100px);
```

Move verticalmente.

```css
transform: translate(100px, 50px);
```

Move nos dois eixos.

```css
transform: scale(1.2);
```

Aumenta.

```css
transform: rotate(45deg);
```

Gira.

```css
transform: skew(10deg);
```

Inclina.

---

# 43. 🧱 Combinar transformações

```css
transform:
    translateX(50px)
    translateY(-20px)
    rotate(15deg)
    scale(1.1);
```

Você pode combinar várias transformações em um único `transform`.

---

# 44. 🎯 Mudar o ponto de origem da transformação

Por padrão:

```css
transform-origin: center;
```

Você pode mudar:

```css
transform-origin: left center;
```

ou:

```css
transform-origin: top left;
```

ou:

```css
transform-origin: bottom right;
```

Isso muda o ponto em torno do qual o elemento gira ou escala.

---

# 45. 🖱️ Abrir ao clicar usando `classList`

```js
elemento.classList.add("aberto");
```

Adiciona a classe.

```js
elemento.classList.remove("aberto");
```

Remove a classe.

```js
elemento.classList.toggle("aberto");
```

Adiciona ou remove automaticamente.

```js
elemento.classList.contains("aberto");
```

Verifica se a classe existe.

---

# 46. 🎮 Evento de clique

```js
botao.addEventListener("click", () => {

    elemento.classList.toggle("aberto");

});
```

Estrutura básica:

```text
usuário clica
     ↓
evento "click"
     ↓
JavaScript executa
     ↓
classe muda
     ↓
CSS percebe a mudança
     ↓
animação
```

---

# 47. 🧠 Padrão geral para criar animações

### CSS

```css
.elemento {
    /* estado inicial */

    opacity: 0;
    transform: translateY(20px);

    transition:
        opacity 0.3s ease,
        transform 0.3s ease;
}

.elemento.ativo {
    /* estado final */

    opacity: 1;
    transform: translateY(0);
}
```

### JavaScript

```js
elemento.classList.toggle("ativo");
```

Esse padrão resolve uma quantidade enorme de animações de interface.

---

# 📌 Resumo rápido

| Efeito | Código principal |
|---|---|
| Aumentar | `scale(1.1)` |
| Diminuir | `scale(0.9)` |
| Mover → | `translateX(100px)` |
| Mover ← | `translateX(-100px)` |
| Mover ↓ | `translateY(100px)` |
| Mover ↑ | `translateY(-100px)` |
| Girar | `rotate(45deg)` |
| Inclinar | `skew(10deg)` |
| Aparecer | `opacity: 1` |
| Desaparecer | `opacity: 0` |
| Suavizar | `transition` |
| Animação contínua | `animation` |
| Criar etapas | `@keyframes` |
| Alterar estado | `classList.toggle()` |
| Expandir | `height / max-height` |
| Altura real | `scrollHeight` |
| Ponto de origem | `transform-origin` |
| Pausar | `animation-play-state` |
| Animação via JS | `element.animate()` |

---

# ⭐ As 5 coisas para decorar primeiro

```css
transform: translateX(100px);
```

```css
transform: translateY(100px);
```

```css
transform: scale(1.1);
```

```css
transform: rotate(45deg);
```

```css
transition: transform 0.3s ease;
```

E em JavaScript:

```js
elemento.classList.toggle("ativo");
```

Com essas seis coisas você já consegue construir uma quantidade surpreendentemente grande de animações de interface.