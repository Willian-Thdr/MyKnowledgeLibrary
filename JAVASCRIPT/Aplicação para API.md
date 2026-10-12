## Aplicação js para criar um localhost:

``` 
const http = require("http");  
const server = http.createServer((req, res) => {  
    if (req.url === "/version") {  
        res.writeHead(200, {  
            "Content-Type": "application/json"  
        });  
        res.end(JSON.stringify({  
            version: "1.0.0"  
        }));  
        return;  
    }  
    res.writeHead(404);  
    res.end("Not Found");  
});  

server.listen(3000, () => {  
    console.log("Servidor rodando em http://localhost:3000");  
});
``` 

## O mínimo para criar uma seria:

```
const http = require("http");  
const server = http.createServer();  
server.listen(3000);
```

## Mas isso não teria utilidade. Então usamos req e res para poder enviar requisições e enviar coisas a aplicação. Ficando assim:

```
const http = require("http");

const server = http.createServer((req, res) => {
    res.end("Olá!");
});

server.listen(3000);
```