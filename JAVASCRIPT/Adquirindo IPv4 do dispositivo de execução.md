# Adquirindo IPv4 do dispositivo de execução

## Contexto

Em determinadas aplicações, o uso da internet local é necessário. Para um dev solo ou para uma empresa grande que está desenvolvendo um site, um link conectado a internet local é necessário para testar a aplicação web em diversos dispositivos locais sem generalizar o acesso antecipadamente para outras pessoas.  
Assim também como o uso de IPv4 é importante para conexões entre pessoas em uma rede de comunicação fechada - caso o projeto seja um programa de mensagens limitado a rede local - e tantos outros serviços, como um assistente doméstico - estilo a Alexa da Amazon - paineis de controle industrial e tantas outras aplicações privadas

## Exemplo

Abaixo estará um simples exemplo, em JavaScript, de como pegar o IPv4 da máquina no qual o código está sendo executado. A partir da variável que é atribuída o valor do IPv4, podemos fazer dos mais diversos tipos de aplicações:

```
const os = require("os");

let ipv4 = get_ipv4();

function get_ipv4() {
    const interfaces = os.networkInterfaces();

    for (const name of Object.keys(interfaces)) {
        for (const net of interfaces[name]) {
            if (net.family === "IPv4" && !net.internal) {
                return net.address;
            }
        }
    }
}
```

A biblioteca `os`, é um módulo nativo do Node.js que permite consultar informações sobre o sistema operacional no qual o código está sendo executado. `os` vem de "Operating System", que significa "Sistema Operacional" em inglês.  
Com ela, podemos consultar informações como o sistema operacional usado, interfaces de rede e seus endereços de IP, a quantidade de memória disponível e entre outras coisas. Para importala, usamos o `const os = require("os");`, mas em versões mais atuais do Node.js podemos escrever `const os = require("node:os");`.