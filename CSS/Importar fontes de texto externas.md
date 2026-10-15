# Importar fontes de texto externas

## Como fazer

O código para importar uma fonte externa para dentro de um `css` é simples. Fazemos da seguinte maneira:
```
@font-face {
    font-family: "MinhaFonte";
    src: url("./Assets/Fonts/MinhaFonte.woff2") format("woff2");
    font-weight: normal;
    font-style: normal;
}
```

Aqui, o trecho `font-family: "MinhaFonte";` é onde definimos o nome da fonte. `src: url("./Assets/Fonts/MinhaFonte.woff2") format("woff2");` é onde pegamos o diretório em que se localiza a fonte. já `font-weight` e `font-style` definimos seu peso respectivamente como normal ou negrito e como normal ou italico.  

## Fontes suportadas

Os formatos que o `css` aceita para importação são:

| Formato | Declaração format() | Características |  
|:---|:---:|:---|
| .woff2 |	"woff2" |	Recomendado para a web; geralmente oferece melhor compressão. |  
| .woff |	"woff" |	Formato web amplamente suportado. |  
| .ttf |	"truetype" |	TrueType; comum em arquivos de fontes instaláveis. |  
| .otf |	"opentype" |	OpenType; também muito utilizado em fontes instaláveis. |  
| .eot |	"embedded-opentype" |	Formato antigo, criado para compatibilidade com versões antigas do Internet Explorer. |  
| .svg |	"svg" |	Fontes SVG; suporte em navegadores modernos é limitado ou inexistente para esse uso. |