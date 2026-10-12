# Guia completo de unidades de medida do CSS

Referência de unidades CSS, equivalências, aplicações e exemplos para desenvolvimento web responsivo.

## 1. Unidades absolutas

Essas unidades possuem relações definidas entre si. Em telas, `px` é a unidade de referência mais utilizada.

| Unidade | Equivalência em CSS | Aplicações principais |
|---|---|---|
| `px` | 1 px | Bordas, ícones, sombras e detalhes precisos |
| `in` | 96 px | Medidas físicas e impressão |
| `cm` | 37,795 px aproximadamente | Impressão e documentos |
| `mm` | 3,7795 px aproximadamente | Impressão e documentos |
| `Q` | 0,9449 px aproximadamente | Medidas físicas; 1 Q = 1/4 mm |
| `pt` | 1,3333 px aproximadamente | Tipografia e impressão |
| `pc` | 16 px | Tipografia tradicional; 1 pc = 12 pt |

**Observação:** essas conversões são relações definidas pelo CSS. Um pixel CSS não corresponde necessariamente a um pixel físico do monitor.

## 2. Unidades relativas à tipografia

Essas unidades dependem do tamanho da fonte ou das características tipográficas.

| Unidade | Funcionamento | Aplicações principais |
|---|---|---|
| `em` | Em `font-size`, depende do tamanho da fonte do elemento pai; em outras propriedades, geralmente depende da fonte do próprio elemento | Espaçamentos proporcionais à tipografia |
| `rem` | Depende do tamanho da fonte do elemento raiz (`html`) | Fontes, margens, espaçamentos e dimensões consistentes |
| `ex` | Baseada na altura-x da fonte atual | Ajustes tipográficos específicos |
| `ch` | Baseada na largura do glifo `0` da fonte atual | Largura de campos e linhas de texto |
| `cap` | Baseada na altura das letras maiúsculas da fonte | Alinhamento tipográfico |
| `ic` | Baseada na dimensão do glifo ideográfico `水` da fonte | Tipografia de idiomas que utilizam caracteres ideográficos |
| `lh` | Baseada na altura da linha (`line-height`) do elemento | Espaçamentos proporcionais às linhas |
| `rlh` | Baseada na altura da linha do elemento raiz | Espaçamentos tipográficos globais |

### Exemplo

```css
html {
    font-size: 16px;
}

h1 {
    font-size: 2rem; /* 32px */
}

.card {
    padding: 1em;
    max-width: 65ch;
}
```

Se a fonte raiz tiver 16 px, `2rem` corresponderá a 32 px. Já `1em` dependerá do contexto tipográfico aplicável, e `65ch` corresponderá a aproximadamente 65 larguras do glifo `0`.

**Importante:** as unidades tipográficas, com exceção das relações que você definir explicitamente, não possuem uma conversão universal para pixels.

## 3. Unidades relativas à área de visualização (viewport)

Essas unidades dependem das dimensões da área de visualização do navegador.

| Unidade | Equivalência | Aplicações principais |
|---|---|---|
| `vw` | 1% da largura da viewport | Larguras e tipografia fluida |
| `vh` | 1% da altura da viewport | Alturas e dimensionamento vertical |
| `vmin` | 1% da menor dimensão da viewport | Elementos proporcionais à menor dimensão |
| `vmax` | 1% da maior dimensão da viewport | Elementos proporcionais à maior dimensão |

### Variantes modernas

| Unidade | Funcionamento |
|---|---|
| `svw`, `svh`, `svmin`, `svmax` | Utilizam a viewport pequena |
| `lvw`, `lvh`, `lvmin`, `lvmax` | Utilizam a viewport grande |
| `dvw`, `dvh`, `dvmin`, `dvmax` | Utilizam a viewport dinâmica, que pode mudar conforme a interface do navegador |

Essas variantes são especialmente úteis em dispositivos móveis, nos quais as barras do navegador podem aparecer ou desaparecer.

### Exemplo

```css
.hero {
    min-height: 100vh;
}

h1 {
    font-size: 5vw;
}

.mobile_panel {
    min-height: 100dvh;
}
```

**Atenção:** `100vh` nem sempre acompanha perfeitamente a área visível em navegadores móveis. `100dvh` pode ser mais apropriado quando você deseja acompanhar a viewport dinâmica.

## 4. Porcentagem (`%`)

A porcentagem não possui uma conversão universal para pixels. Sua referência depende da propriedade CSS.

| Propriedade | Referência típica |
|---|---|
| `width: 50%` | Largura do bloco de referência |
| `height: 50%` | Altura do bloco de referência, quando pode ser determinada |
| `font-size: 120%` | Tamanho da fonte do elemento pai |
| `margin-left: 10%` | Geralmente, largura do bloco de referência |
| `transform: translateX(50%)` | Largura da própria caixa transformada |
| `background-position: 50%` | Alinhamento relativo à área de posicionamento do fundo |

### Exemplo

```css
.container {
    width: 80%;
}
```

Se o bloco de referência tiver 1000 px de largura, o contêiner normalmente terá 800 px.

Entretanto, não presuma que toda propriedade que aceita `%` utilize a mesma referência.

## 5. Unidades relativas a contêineres (container query units)

Essas unidades permitem dimensionar elementos em relação a um contêiner de consulta, em vez de depender exclusivamente da janela do navegador.

| Unidade | Referência |
|---|---|
| `cqw` | 1% da largura do contêiner |
| `cqh` | 1% da altura do contêiner |
| `cqi` | 1% do tamanho do eixo inline do contêiner |
| `cqb` | 1% do tamanho do eixo block do contêiner |
| `cqmin` | 1% da menor dimensão entre os eixos inline e block |
| `cqmax` | 1% da maior dimensão entre os eixos inline e block |

### Exemplo

```css
.profile_panel {
    container-type: inline-size;
}

.profile_panel h2 {
    font-size: clamp(1rem, 5cqi, 2rem);
}
```

Essas unidades são úteis quando um componente precisa adaptar-se ao espaço que recebe, independentemente do tamanho total da tela.

Para que usem o contêiner esperado, normalmente é necessário configurar um ancestral com `container-type` apropriado.

## 6. Unidade de fração do CSS Grid (`fr`)

`fr` não é uma unidade geral de comprimento. Ela distribui o espaço disponível entre as trilhas de uma grade CSS Grid.

```css
.layout {
    display: grid;
    grid-template-columns: 1fr 2fr;
}
```

Nesse exemplo, as colunas recebem espaço flexível em uma proporção de aproximadamente 1:2, respeitando as restrições de dimensionamento da grade.

**Aplicação principal:** criar colunas proporcionais sem calcular manualmente suas larguras em pixels.

## 7. Funções de dimensionamento

Essas funções não são unidades de medida, mas combinam valores e unidades para produzir layouts flexíveis.

### `calc()`

Realiza cálculos com valores CSS compatíveis.

```css
.sidebar {
    width: calc(100% - 2rem);
}
```

### `min()`

Escolhe o menor valor entre os argumentos.

```css
.content {
    width: min(90%, 70rem);
}
```

### `max()`

Escolhe o maior valor entre os argumentos.

```css
.content {
    width: max(80%, 20rem);
}
```

### `clamp()`

Limita um valor entre um mínimo, um valor preferido e um máximo.

```css
h1 {
    font-size: clamp(1.75rem, 4vw, 3.5rem);
}
```

A fonte nunca será menor que `1.75rem` nem maior que `3.5rem`. Entre esses limites, `4vw` orientará seu tamanho.

## 8. Qual unidade utilizar?

| Objetivo | Opções recomendadas |
|---|---|
| Bordas e detalhes precisos | `px` |
| Tipografia consistente | `rem` |
| Espaçamentos proporcionais à fonte | `em` |
| Limitar a largura de linhas de texto | `ch` |
| Ocupar uma porcentagem do contêiner | `%` |
| Dimensionar em função da janela | `vw`, `vh`, `vmin`, `vmax` |
| Adaptar componentes ao próprio contêiner | `cqi`, `cqw` e outras `cq*` |
| Criar colunas proporcionais em Grid | `fr` |
| Definir tamanhos mínimos e máximos | `clamp()` |
| Adaptar a estrutura a diferentes larguras | Media queries e container queries |

## 9. Regras práticas para design responsivo

1. Não substitua todas as medidas fixas por relativas indiscriminadamente.
2. Utilize `rem` como ponto de partida para tipografia e espaçamentos consistentes.
3. Utilize `clamp()` quando precisar de crescimento fluido com limites.
4. Lembre-se de que `vw` e `vh` dependem da viewport, não da largura ou altura interna de um cartão.
5. Lembre-se de que `%` varia conforme a propriedade e sua referência de cálculo.
6. Utilize Flexbox e CSS Grid para estruturar layouts; unidades relativas não substituem essas ferramentas.
7. Utilize media queries para reorganizar a interface em determinadas larguras e container queries para adaptar componentes ao espaço disponível.
8. Teste telas estreitas, janelas baixas, zoom e textos maiores.
9. Evite larguras rígidas que provoquem rolagem horizontal desnecessária.
10. Priorize a legibilidade e a usabilidade, não apenas a capacidade de encolher os elementos.

## 10. Documentação para consulta

- MDN — Valores e unidades CSS: https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/Styling_basics/Values_and_units
- MDN — Comprimentos CSS: https://developer.mozilla.org/en-US/docs/Web/CSS/length
- MDN — Container queries: https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_containment/Container_queries
- MDN — CSS Grid Layout: https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_grid_layout
- MDN — Função `clamp()`: https://developer.mozilla.org/en-US/docs/Web/CSS/clamp
