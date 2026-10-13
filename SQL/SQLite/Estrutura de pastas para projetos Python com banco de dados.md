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