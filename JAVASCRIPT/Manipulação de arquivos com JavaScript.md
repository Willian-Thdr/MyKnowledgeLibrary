# Guia: Manipulação de arquivos com JavaScript (Node.js)

## 1. Importando o módulo

O Node.js possui um módulo nativo chamado `fs`, portanto, não é necessário instalar dependências.

Utilizaremos a versão baseada em Promises:

```javascript
import fs from "node:fs/promises";
```

## 2. Criando e escrevendo arquivos

Para criar um arquivo e escrever conteúdo nele, utilizamos `writeFile()`.

```javascript
import fs from "node:fs/promises";

await fs.writeFile("arquivo.txt", "Olá, mundo!");
```

Se o arquivo não existir, ele será criado automaticamente.

Se já existir, seu conteúdo será sobrescrito.

### Escrevendo JSON

Para armazenar objetos JavaScript em arquivos JSON, utilizamos `JSON.stringify()`.

```javascript
const data = {
    username: "Willian-Thdr",
    repositories: 10,
    languages: ["JavaScript", "Python", "Java"]
};

await fs.writeFile(
    "data.json",
    JSON.stringify(data, null, 4)
);
```

O segundo e o terceiro argumentos de `JSON.stringify()` controlam a formatação:

- `null`: não substitui nenhuma propriedade.
- `4`: utiliza quatro espaços para identação.

## 3. Lendo arquivos

Para recuperar o conteúdo de um arquivo, utilizamos `readFile()`.

```javascript
const content = await fs.readFile("arquivo.txt", "utf-8");

console.log(content);
```

O parâmetro `"utf-8"` determina a codificação do texto retornado.

### Lendo JSON

Como o conteúdo de um JSON é armazenado como texto, precisamos convertê-lo novamente para um objeto JavaScript.

```javascript
const content = await fs.readFile("data.json", "utf-8");

const data = JSON.parse(content);

console.log(data.username);
```

## 4. Adicionando conteúdo sem apagar o anterior

Se você deseja acrescentar informações ao final de um arquivo, utilize `appendFile()`.

```javascript
await fs.appendFile("arquivo.txt", "\nNova informação!");
```

Diferentemente de `writeFile()`, essa operação preserva o conteúdo anterior.

## 5. Verificando se um arquivo existe

Uma maneira simples de verificar a existência de um arquivo é utilizar `access()`.

```javascript
try {
    await fs.access("data.json");

    console.log("O arquivo existe!");
} catch {
    console.log("O arquivo não existe!");
}
```

## 6. Criando diretórios

Para criar pastas, utilizamos `mkdir()`.

```javascript
await fs.mkdir("database", { recursive: true });
```

A propriedade `recursive: true` permite criar também os diretórios intermediários, caso necessário.

## 7. Excluindo arquivos

Para excluir um arquivo:

```javascript
await fs.unlink("arquivo.txt");
```

Para excluir um diretório:

```javascript
await fs.rmdir("database");
```

Observação: `rmdir()` exige que o diretório esteja vazio. Para remover diretórios e seus conteúdos, existe `fs.rm()`.

## 8. Exemplo prático: criando um sistema de armazenamento JSON

Este exemplo reúne os conceitos anteriores em uma pequena função de armazenamento.

```javascript
import fs from "node:fs/promises";

async function save_data(data) {
    try {
        await fs.mkdir("database", { recursive: true });

        await fs.writeFile(
            "database/data.json",
            JSON.stringify(data, null, 4),
            "utf-8"
        );

        console.log("Dados armazenados com sucesso!");

    } catch (error) {
        console.error("Erro ao armazenar dados:", error);
    }
}

const user_data = {
    username: "Willian-Thdr",
    repositories: [
        {
            name: "project-one",
            language: "JavaScript"
        },
        {
            name: "project-two",
            language: "Python"
        }
    ]
};

await save_data(user_data);
```

---

## 9. Referência rápida

| Método | Finalidade |
|---|---|
| `writeFile()` | Criar ou sobrescrever arquivos |
| `readFile()` | Ler arquivos |
| `appendFile()` | Acrescentar conteúdo |
| `access()` | Verificar acesso ou existência |
| `mkdir()` | Criar diretórios |
| `unlink()` | Excluir arquivos |
| `rm()` | Excluir arquivos ou diretórios |
| `rename()` | Renomear ou mover arquivos |
| `copyFile()` | Copiar arquivos |
| `readdir()` | Listar conteúdo de diretórios |
| `stat()` | Consultar informações de arquivos |

**Documentação oficial:** https://nodejs.org/api/fs.html