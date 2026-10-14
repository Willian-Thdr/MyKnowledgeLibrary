# Estrutura básica de um projeto Python com SQLite

```text
meu_projeto/
│
├── main.py
│
├── database/
│   ├── __init__.py
│   ├── connection.py
│   └── schema.sql
│
├── data/
│   └── banco.db
│
└── .gitignore
```

## Função de cada arquivo

- **`main.py`** — arquivo principal. Executa o programa e conecta suas diferentes partes.
- **`database/`** — pasta que reúne os arquivos responsáveis pelo banco de dados.
- **`database/__init__.py`** — identifica a pasta como um pacote Python. Pode ficar vazio.
- **`database/connection.py`** — contém a função que abre a conexão com o banco SQLite.
- **`database/schema.sql`** — contém os comandos SQL para criar as tabelas e definir sua estrutura.
- **`data/`** — pasta que armazena o arquivo do banco.
- **`data/banco.db`** — arquivo SQLite que guarda os dados efetivos.
- **`.gitignore`** — define quais arquivos o Git deve ignorar, como ambientes virtuais, caches e bancos locais que não devem ser publicados.

## Como o código se organiza

1. `main.py` inicia o programa.
2. `connection.py` abre a conexão com o banco.
3. `schema.sql` define as tabelas que precisam existir.
4. `banco.db` armazena os registros.

**Observação:** nessa estrutura inicial, você pode executar as consultas SQL diretamente no `main.py`. Quando o projeto crescer, crie um arquivo `operations.py` para separar as operações do banco da lógica principal.

## Exemplo de códigos

### Main.py:
```
from database.connection import conectar

def main():
    conexao = conectar()

    try:
        cursor = conexao.cursor()

        cursor.execute("""
            SELECT name
            FROM sqlite_master
            WHERE type = 'table'
        """)

        tabelas = cursor.fetchall()

        print("Tabelas encontradas:", tabelas)

    finally:
        conexao.close()

if __name__ == "__main__":
    main()
```

### Conections.py

```

import sqlite3
from pathlib import Path

# Localização da raiz do projeto
BASE_DIR = Path(__file__).resolve().parent.parent

# Caminho do banco de dados
DB_PATH = BASE_DIR / "data" / "banco.db"

# Caminho do arquivo SQL
SCHEMA_PATH = BASE_DIR / "database" / "schema.sql"


def conectar():
    # Cria a pasta data caso ela não exista
    DB_PATH.parent.mkdir(parents=True, exist_ok=True)

    # Abre a conexão; cria o arquivo .db se necessário
    conexao = sqlite3.connect(DB_PATH)

    try:
        # Lê os comandos SQL do arquivo schema.sql
        schema = SCHEMA_PATH.read_text(encoding="utf-8")

        # Cria as tabelas definidas no arquivo
        conexao.executescript(schema)

        # Confirma as alterações
        conexao.commit()

        return conexao

    except Exception:
        conexao.close()
        raise
```

### schema.sql:

```
CREATE TABLE IF NOT EXISTS usuarios (
    id INTEGER PRIMARY KEY,
    nome TEXT NOT NULL,
    email TEXT NOT NULL UNIQUE
);

CREATE TABLE IF NOT EXISTS livros (
    id INTEGER PRIMARY KEY,
    titulo TEXT NOT NULL,
    autor TEXT NOT NULL
);
```

### init.py:

Ele não é obrigatório no programa. Mas se possuir um, ele terá:

```
from .connection import conectar
```

Sem o init, o main deve conter:

```
from database.connection import conectar
```

Caso o init esteja presente, o main possuirá:
```
from database import conectar
```