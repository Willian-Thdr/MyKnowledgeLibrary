# SQLite — Guia de Estudos do Básico ao Intermediário

## 1. O que é SQLite?

SQLite é um sistema de gerenciamento de banco de dados relacional que armazena informações em um arquivo local, sem exigir um servidor separado.

- **SQLite:** sistema de banco de dados.
- **SQL:** linguagem usada para consultar e manipular dados.
- **Tabela:** estrutura que organiza informações em linhas e colunas.
- **Registro:** uma linha da tabela.
- **Coluna:** atributo de um registro.
- **Banco de dados:** conjunto organizado de tabelas e outros objetos relacionados.

### Principais aplicações

- Armazenamento de configurações de programas.
- Cadastro de usuários, livros, produtos e tarefas.
- Aplicações desktop.
- Aplicações móveis.
- Protótipos e projetos pessoais.
- Armazenamento local de dados em ferramentas de desenvolvimento.
- Aplicações web de pequeno e médio porte, dependendo da carga de trabalho e do padrão de acesso.

---

# 2. Criando um banco de dados

O SQLite cria o arquivo do banco quando uma conexão é aberta para um arquivo inexistente.

```python
import sqlite3

conexao = sqlite3.connect("aplicacao.db")
cursor = conexao.cursor()

conexao.close()
```

Nesse exemplo:

- `sqlite3` importa a biblioteca de integração do Python.
- `connect()` abre ou cria o banco de dados.
- `cursor()` cria um objeto que executa comandos SQL.
- `close()` encerra a conexão.

**Aplicação:** criar o armazenamento persistente de um programa.

---

# 3. Criando tabelas — CREATE TABLE

Uma tabela define a estrutura dos dados que serão armazenados.

```sql
CREATE TABLE IF NOT EXISTS usuarios (
    id INTEGER PRIMARY KEY,
    nome TEXT NOT NULL,
    email TEXT UNIQUE,
    idade INTEGER
);
```

### Elementos utilizados

- `CREATE TABLE`: cria uma tabela.
- `IF NOT EXISTS`: evita erro caso a tabela já exista.
- `INTEGER`: valor inteiro.
- `TEXT`: texto.
- `REAL`: número de ponto flutuante.
- `BLOB`: dados binários.
- `PRIMARY KEY`: identifica unicamente cada registro.
- `NOT NULL`: impede valores nulos.
- `UNIQUE`: impede valores duplicados naquela coluna.

SQLite também admite `NULL`, que representa ausência de valor.

### Aplicação

Em um sistema de usuários, a tabela pode armazenar nome, e-mail e idade.

**Observação:** SQLite utiliza tipagem dinâmica, com classes de armazenamento `NULL`, `INTEGER`, `REAL`, `TEXT` e `BLOB`. A declaração de um tipo nem sempre impõe as mesmas restrições encontradas em outros bancos de dados.

---

# 4. Inserindo dados — INSERT

O comando `INSERT` adiciona registros.

```sql
INSERT INTO usuarios (nome, email, idade)
VALUES ('Ana', 'ana@example.com', 22);
```

Inserindo vários registros:

```sql
INSERT INTO usuarios (nome, email, idade)
VALUES
    ('Carlos', 'carlos@example.com', 25),
    ('Marina', 'marina@example.com', 19),
    ('Pedro', 'pedro@example.com', 31);
```

### Aplicação

- Cadastrar usuários.
- Registrar produtos.
- Criar tarefas.
- Armazenar títulos de livros.

### Inserindo dados com Python

```python
cursor.execute(
    "INSERT INTO usuarios (nome, email, idade) VALUES (?, ?, ?)",
    ("Ana", "ana@example.com", 22)
)

conexao.commit()
```

Utilize `?` como marcador de parâmetro. Os valores são enviados separadamente do comando SQL, evitando a necessidade de concatenar dados diretamente na consulta.

---

# 5. Consultando dados — SELECT

O comando `SELECT` recupera informações.

```sql
SELECT * FROM usuarios;
```

O asterisco representa todas as colunas.

Para selecionar apenas algumas:

```sql
SELECT nome, email FROM usuarios;
```

### Aplicações

- Exibir usuários cadastrados.
- Listar livros de uma biblioteca.
- Consultar produtos.
- Recuperar informações para uma interface.

**Boa prática:** em aplicações reais, prefira especificar as colunas necessárias em vez de utilizar `SELECT *` indiscriminadamente.

---

# 6. Filtrando dados — WHERE

O `WHERE` restringe os registros retornados.

```sql
SELECT * FROM usuarios
WHERE idade >= 18;
```

### Operadores de comparação

| Operador | Significado |
|---|---|
| `=` | Igual |
| `!=` ou `<>` | Diferente |
| `>` | Maior |
| `<` | Menor |
| `>=` | Maior ou igual |
| `<=` | Menor ou igual |

### Operadores lógicos

```sql
SELECT * FROM usuarios
WHERE idade >= 18 AND idade <= 30;
```

```sql
SELECT * FROM usuarios
WHERE idade < 18 OR idade > 60;
```

```sql
SELECT * FROM usuarios
WHERE NOT idade = 20;
```

### Aplicação

Criar filtros de pesquisa, selecionar usuários por idade ou localizar registros que atendam a condições específicas.

---

# 7. Pesquisas com LIKE

O operador `LIKE` permite pesquisar padrões de texto.

```sql
SELECT * FROM usuarios
WHERE nome LIKE 'A%';
```

Nesse caso, são retornados nomes que começam com A.

| Padrão | Significado |
|---|---|
| `'A%'` | Começa com A |
| `'%a'` | Termina com a |
| `'%ana%'` | Contém ana |
| `'_na'` | Três caracteres, terminando em na |

- `%` representa zero ou mais caracteres.
- `_` representa exatamente um caractere.

### Aplicação

Implementar uma busca simples por nomes, títulos ou descrições.

Para pesquisas textuais mais avançadas, o SQLite também oferece a extensão FTS5, quando disponível na compilação utilizada.

---

# 8. Ordenando resultados — ORDER BY

```sql
SELECT * FROM usuarios
ORDER BY idade ASC;
```

- `ASC`: ordem crescente.
- `DESC`: ordem decrescente.

Exemplo:

```sql
SELECT * FROM usuarios
ORDER BY nome DESC;
```

Também é possível ordenar por mais de uma coluna:

```sql
SELECT * FROM usuarios
ORDER BY idade DESC, nome ASC;
```

### Aplicação

- Listar produtos do mais barato ao mais caro.
- Mostrar tarefas por prioridade.
- Organizar livros alfabeticamente.
- Exibir registros recentes primeiro, utilizando uma coluna de data apropriada.

---

# 9. Limitando resultados — LIMIT e OFFSET

```sql
SELECT * FROM usuarios
LIMIT 10;
```

Retorna no máximo dez registros.

Para ignorar os primeiros registros:

```sql
SELECT * FROM usuarios
LIMIT 10 OFFSET 20;
```

Retorna até dez registros depois de pular os vinte primeiros.

### Aplicação: paginação

Uma interface pode mostrar dez produtos por página, evitando carregar todos os registros de uma vez.

**Atenção:** combine `LIMIT` e `OFFSET` com `ORDER BY` para obter uma ordenação previsível. Em tabelas muito grandes, paginação por chave pode ser mais eficiente do que deslocamentos elevados.

---

# 10. Atualizando registros — UPDATE

```sql
UPDATE usuarios
SET idade = 23
WHERE id = 1;
```

O `UPDATE` altera os valores existentes.

É possível alterar mais de uma coluna:

```sql
UPDATE usuarios
SET nome = 'Ana Silva',
    idade = 24
WHERE id = 1;
```

### Aplicação

- Editar dados de usuários.
- Atualizar informações de produtos.
- Alterar o estado de uma tarefa.
- Modificar o título de um livro.

**Cuidado:** sem `WHERE`, todos os registros da tabela serão atualizados.

---

# 11. Excluindo registros — DELETE

```sql
DELETE FROM usuarios
WHERE id = 1;
```

Remove o registro cujo identificador é 1.

Para excluir todos os registros:

```sql
DELETE FROM usuarios;
```

Esse comando mantém a tabela, mas remove seus registros.

Para remover a própria tabela:

```sql
DROP TABLE usuarios;
```

**Atenção:** `DELETE` e `DROP TABLE` são operações diferentes. Antes de executá-las em aplicações reais, confirme que a condição está correta e considere utilizar transações.

---

# 12. Valores nulos — NULL

`NULL` representa a ausência de um valor. Ele não é equivalente a zero, texto vazio ou `FALSE`.

Consulta correta:

```sql
SELECT * FROM usuarios
WHERE email IS NULL;
```

Para encontrar e-mails preenchidos:

```sql
SELECT * FROM usuarios
WHERE email IS NOT NULL;
```

Não utilize `email = NULL`, pois a comparação correta exige `IS NULL` ou `IS NOT NULL`.

### Aplicação

Identificar cadastros incompletos, informações opcionais e campos ainda não preenchidos.

---

# 13. Funções de agregação

As funções de agregação calculam valores a partir de vários registros.

```sql
SELECT COUNT(*) FROM usuarios;
```

Conta os registros.

```sql
SELECT AVG(idade) FROM usuarios;
```

Calcula a média das idades não nulas.

```sql
SELECT MIN(idade), MAX(idade)
FROM usuarios;
```

Retorna a menor e a maior idade.

```sql
SELECT SUM(idade)
FROM usuarios;
```

Calcula a soma das idades não nulas.

### Funções principais

| Função | Finalidade |
|---|---|
| `COUNT()` | Contar registros ou valores |
| `SUM()` | Somar valores |
| `AVG()` | Calcular média |
| `MIN()` | Encontrar o menor valor |
| `MAX()` | Encontrar o maior valor |

### Aplicação

Gerar estatísticas, calcular totais de vendas, contar tarefas concluídas ou obter métricas de utilização.

---

# 14. Agrupando dados — GROUP BY

O `GROUP BY` agrupa registros que possuem valores iguais em determinadas colunas.

Imagine uma tabela `pedidos` com uma coluna `cliente_id`:

```sql
SELECT cliente_id, COUNT(*) AS total_pedidos
FROM pedidos
GROUP BY cliente_id;
```

A consulta conta quantos pedidos cada cliente possui.

Para filtrar grupos, utilize `HAVING`:

```sql
SELECT cliente_id, COUNT(*) AS total_pedidos
FROM pedidos
GROUP BY cliente_id
HAVING COUNT(*) >= 3;
```

### Diferença entre WHERE e HAVING

- `WHERE`: filtra os registros antes do agrupamento.
- `HAVING`: filtra os grupos após o agrupamento.

### Aplicação

- Calcular vendas por produto.
- Contar tarefas por categoria.
- Descobrir quantos livros cada autor possui.
- Gerar relatórios estatísticos.

---

# 15. Chaves primárias e estrangeiras

## Chave primária — PRIMARY KEY

Uma chave primária identifica unicamente cada registro.

```sql
CREATE TABLE autores (
    id INTEGER PRIMARY KEY,
    nome TEXT NOT NULL
);
```

## Chave estrangeira — FOREIGN KEY

Uma chave estrangeira estabelece uma relação entre tabelas.

```sql
CREATE TABLE livros (
    id INTEGER PRIMARY KEY,
    titulo TEXT NOT NULL,
    autor_id INTEGER,
    FOREIGN KEY (autor_id) REFERENCES autores(id)
);
```

Nesse exemplo, `autor_id` relaciona cada livro a um autor.

### Por que isso é útil?

Imagine que um autor tenha dez livros. Em vez de repetir todas as informações do autor em cada livro, você armazena os dados do autor uma vez e referencia seu identificador.

Isso reduz redundâncias e facilita a manutenção.

**Importante:** no SQLite, as restrições de chave estrangeira precisam ser habilitadas em cada conexão:

```python
conexao.execute("PRAGMA foreign_keys = ON")
```

Faça isso antes de executar operações que dependam dessas restrições.

---

# 16. Relacionando tabelas — JOIN

O `JOIN` permite combinar informações de tabelas relacionadas.

Considere estas tabelas:

- `autores`: contém `id` e `nome`.
- `livros`: contém `id`, `titulo` e `autor_id`.

```sql
SELECT livros.titulo, autores.nome
FROM livros
JOIN autores
ON livros.autor_id = autores.id;
```

O resultado apresenta cada título acompanhado do nome de seu autor.

## Tipos principais de JOIN

- `INNER JOIN`: retorna os registros que possuem correspondência nas duas tabelas.
- `LEFT JOIN`: retorna todos os registros da tabela à esquerda, mesmo sem correspondência na tabela da direita.
- `CROSS JOIN`: combina cada registro de uma tabela com cada registro da outra.

Exemplo de `LEFT JOIN`:

```sql
SELECT autores.nome, livros.titulo
FROM autores
LEFT JOIN livros
ON autores.id = livros.autor_id;
```

Essa consulta também apresenta autores que não possuem livros correspondentes.

### Aplicação

- Relacionar usuários e publicações.
- Relacionar clientes e pedidos.
- Relacionar autores e livros.
- Relacionar categorias e produtos.

---

# 17. Eliminando duplicatas — DISTINCT

```sql
SELECT DISTINCT autor_id
FROM livros;
```

Retorna os identificadores de autores sem repetições.

### Aplicação

Descobrir quais categorias aparecem em uma tabela ou listar os autores que possuem livros cadastrados.

O `DISTINCT` considera a combinação das colunas selecionadas quando há mais de uma coluna na consulta.

---

# 18. Restrições de dados

Restrições ajudam a impedir que dados inválidos sejam armazenados.

```sql
CREATE TABLE produtos (
    id INTEGER PRIMARY KEY,
    nome TEXT NOT NULL,
    preco REAL NOT NULL CHECK (preco >= 0),
    codigo TEXT UNIQUE
);
```

### Restrições importantes

- `NOT NULL`: exige um valor.
- `UNIQUE`: impede duplicatas.
- `CHECK`: verifica uma condição.
- `PRIMARY KEY`: identifica o registro.
- `FOREIGN KEY`: garante a integridade de relações, quando habilitada.

### Aplicação

Impedir preços negativos, evitar códigos duplicados e assegurar que campos essenciais sejam preenchidos.

**Observação:** para valores monetários, prefira armazenar quantias em unidades inteiras mínimas, como centavos, em vez de depender de cálculos com números de ponto flutuante.

---

# 19. Índices — CREATE INDEX

Índices podem acelerar pesquisas em determinadas colunas.

```sql
CREATE INDEX idx_usuarios_email
ON usuarios(email);
```

Uma consulta por e-mail poderá se beneficiar desse índice:

```sql
SELECT * FROM usuarios
WHERE email = 'ana@example.com';
```

### Quando utilizar índices?

- Colunas utilizadas frequentemente em filtros.
- Colunas usadas em determinados `JOIN`.
- Colunas utilizadas na ordenação, quando o índice for adequado.
- Campos consultados repetidamente em tabelas grandes.

### Desvantagens

Índices ocupam espaço e podem tornar inserções, atualizações e exclusões mais lentas, porque precisam ser mantidos.

Não crie índices indiscriminadamente. Use `EXPLAIN QUERY PLAN` para investigar como o SQLite executa uma consulta.

---

# 20. Transações — BEGIN, COMMIT e ROLLBACK

Uma transação permite tratar várias operações como uma unidade de trabalho.

```sql
BEGIN TRANSACTION;

UPDATE contas
SET saldo = saldo - 100
WHERE id = 1;

UPDATE contas
SET saldo = saldo + 100
WHERE id = 2;

COMMIT;
```

A intenção é transferir cem unidades monetárias de uma conta para outra.

- `BEGIN TRANSACTION`: inicia uma transação.
- `COMMIT`: confirma as alterações.
- `ROLLBACK`: desfaz as alterações ainda não confirmadas.

Se ocorrer um erro, a aplicação pode reverter as operações da transação.

### Aplicação

- Transferências entre contas.
- Processamento de pedidos.
- Atualizações de vários registros relacionados.
- Operações que precisam preservar a consistência dos dados.

**Importante:** uma implementação financeira real também deve validar saldo suficiente, existência das contas e concorrência entre operações.

---

# 21. Tratando erros e utilizando Python com segurança

Exemplo de integração entre Python e SQLite:

```python
import sqlite3

conexao = sqlite3.connect("aplicacao.db")

try:
    conexao.execute("PRAGMA foreign_keys = ON")

    conexao.execute("""
        CREATE TABLE IF NOT EXISTS tarefas (
            id INTEGER PRIMARY KEY,
            titulo TEXT NOT NULL,
            concluida INTEGER NOT NULL DEFAULT 0
                CHECK (concluida IN (0, 1))
        )
    """)

    conexao.execute(
        "INSERT INTO tarefas (titulo) VALUES (?)",
        ("Estudar SQLite",)
    )

    conexao.commit()

except sqlite3.Error as erro:
    conexao.rollback()
    print(f"Erro no banco de dados: {erro}")

finally:
    conexao.close()
```

### Conceitos importantes

- `try`: executa um bloco que pode produzir um erro.
- `except`: trata o erro capturado.
- `finally`: executa a etapa final, como fechar a conexão.
- `sqlite3.Error`: classe-base para erros do SQLite na biblioteca Python.
- `rollback()`: reverte alterações pendentes da transação.
- `execute()`: executa uma instrução SQL.
- `fetchone()`: recupera um registro.
- `fetchall()`: recupera todos os registros restantes.
- `commit()`: confirma as alterações pendentes.

**Boa prática:** prefira gerenciar conexões com `with sqlite3.connect(...) as conexao:` quando o objetivo for delimitar a transação. No Python, esse gerenciador confirma ou reverte a transação conforme o resultado, mas não fecha automaticamente a conexão; feche-a explicitamente quando necessário.

---

# 22. Funções de texto e manipulação de valores

SQLite possui funções internas que podem ser utilizadas nas consultas.

```sql
SELECT UPPER(nome) FROM usuarios;
```

Converte o texto para letras maiúsculas.

```sql
SELECT LOWER(nome) FROM usuarios;
```

Converte o texto para letras minúsculas.

```sql
SELECT LENGTH(nome) FROM usuarios;
```

Retorna o comprimento do texto em caracteres Unicode, com ressalvas para determinadas representações e valores.

```sql
SELECT TRIM(nome) FROM usuarios;
```

Remove espaços e outros caracteres de espaço em branco definidos pela função nas extremidades do texto.

```sql
SELECT COALESCE(email, 'Não informado')
FROM usuarios;
```

Retorna o primeiro argumento que não seja `NULL`.

### Aplicação

Normalizar apresentações de dados, fornecer valores alternativos e preparar resultados para relatórios.

---

# 23. Expressões condicionais — CASE

O `CASE` permite produzir resultados diferentes conforme uma condição.

```sql
SELECT
    nome,
    idade,
    CASE
        WHEN idade < 18 THEN 'Menor de idade'
        WHEN idade < 60 THEN 'Adulto'
        ELSE 'Idoso'
    END AS faixa_etaria
FROM usuarios;
```

### Aplicação

- Classificar produtos por faixa de preço.
- Separar tarefas por estado.
- Categorizar usuários.
- Criar relatórios com classificações calculadas.

---

# 24. Valores padrão — DEFAULT

A cláusula `DEFAULT` define um valor utilizado quando a inserção não fornece um valor para a coluna.

```sql
CREATE TABLE tarefas (
    id INTEGER PRIMARY KEY,
    titulo TEXT NOT NULL,
    concluida INTEGER NOT NULL DEFAULT 0
);
```

Ao inserir uma tarefa:

```sql
INSERT INTO tarefas (titulo)
VALUES ('Aprender SQL');
```

A coluna `concluida` receberá `0`.

### Aplicação

Definir valores iniciais para configurações, estados de tarefas e contadores.

---

# 25. Criando uma aplicação CRUD completa em Python

Este exemplo reúne criação de tabela, inserção, consulta, atualização e exclusão.

```python
import sqlite3

def conectar():
    return sqlite3.connect("biblioteca.db")

def criar_tabela():
    with conectar() as conexao:
        conexao.execute("""
            CREATE TABLE IF NOT EXISTS livros (
                id INTEGER PRIMARY KEY,
                titulo TEXT NOT NULL,
                autor TEXT NOT NULL,
                ano INTEGER
            )
        """)

def adicionar_livro(titulo, autor, ano):
    with conectar() as conexao:
        conexao.execute(
            """
            INSERT INTO livros (titulo, autor, ano)
            VALUES (?, ?, ?)
            """,
            (titulo, autor, ano)
        )

def listar_livros():
    with conectar() as conexao:
        return conexao.execute("""
            SELECT id, titulo, autor, ano
            FROM livros
            ORDER BY titulo
        """).fetchall()

def atualizar_livro(id_livro, novo_titulo):
    with conectar() as conexao:
        cursor = conexao.execute(
            "UPDATE livros SET titulo = ? WHERE id = ?",
            (novo_titulo, id_livro)
        )
        return cursor.rowcount

def excluir_livro(id_livro):
    with conectar() as conexao:
        cursor = conexao.execute(
            "DELETE FROM livros WHERE id = ?",
            (id_livro,)
        )
        return cursor.rowcount

criar_tabela()

adicionar_livro(
    "Dom Casmurro",
    "Machado de Assis",
    1899
)

for livro in listar_livros():
    print(livro)
```

As funções de atualização e exclusão retornam o número de linhas afetadas, o que permite verificar se um identificador correspondeu a algum registro.

O exemplo é adequado para estudo. Em uma aplicação real, também seria necessário tratar entradas inválidas, evitar inserções duplicadas quando isso for relevante e organizar melhor as responsabilidades do programa.

---

# 26. Backup e manutenção

Um banco de dados precisa ser preservado e mantido corretamente.

### Backup com Python

```python
import sqlite3

origem = sqlite3.connect("biblioteca.db")
destino = sqlite3.connect("biblioteca_backup.db")

try:
    origem.backup(destino)
finally:
    destino.close()
    origem.close()
```

A API de backup do SQLite permite criar uma cópia consistente do banco mesmo quando há outras conexões utilizando o arquivo.

### Verificando a integridade

```sql
PRAGMA integrity_check;
```

Essa instrução verifica aspectos estruturais da integridade do banco.

### Consultando a estrutura de uma tabela

```sql
PRAGMA table_info(livros);
```

Retorna informações sobre as colunas da tabela.

### Aplicação

- Criar cópias de segurança.
- Investigar problemas de integridade.
- Examinar a estrutura de tabelas.
- Diagnosticar o funcionamento do banco.

---

# 27. Recursos intermediários adicionais

Depois de dominar o CRUD e os relacionamentos, estude também:

## Subconsultas

Permitem utilizar o resultado de uma consulta dentro de outra.

```sql
SELECT nome
FROM usuarios
WHERE idade > (
    SELECT AVG(idade)
    FROM usuarios
);
```

Retorna usuários com idade superior à média da tabela.

## CTE — Common Table Expressions

Uma CTE cria um resultado nomeado temporário durante a execução de uma consulta.

```sql
WITH adultos AS (
    SELECT *
    FROM usuarios
    WHERE idade >= 18
)
SELECT nome
FROM adultos;
```

## UPSERT

Permite inserir um registro ou tratar um conflito de unicidade.

```sql
INSERT INTO usuarios (nome, email, idade)
VALUES ('Ana', 'ana@example.com', 22)
ON CONFLICT(email)
DO UPDATE SET idade = excluded.idade;
```

A coluna `email` precisa ter uma restrição de unicidade ou um índice único apropriado para esse tratamento de conflito.

## Views

Uma view é uma consulta salva que pode ser consultada como uma tabela virtual.

```sql
CREATE VIEW usuarios_adultos AS
SELECT id, nome, idade
FROM usuarios
WHERE idade >= 18;
```

Depois:

```sql
SELECT * FROM usuarios_adultos;
```

## Funções de janela

Permitem realizar cálculos entre linhas relacionadas sem reduzir necessariamente cada grupo a uma única linha.

```sql
SELECT
    nome,
    idade,
    RANK() OVER (ORDER BY idade DESC) AS posicao
FROM usuarios;
```

Esse recurso é útil para rankings e análises mais avançadas.

---

# 28. Ordem recomendada de estudo

## Nível 1 — Fundamentos

- [ ] Entender bancos relacionais, tabelas, linhas e colunas.
- [ ] Criar um banco de dados.
- [ ] Criar tabelas.
- [ ] Conhecer os tipos e as restrições.
- [ ] Inserir registros.
- [ ] Consultar registros.
- [ ] Filtrar com `WHERE`.
- [ ] Atualizar e excluir registros.

**Projeto:** lista de tarefas salva em SQLite.

## Nível 2 — Consultas e organização

- [ ] Utilizar `LIKE`, `ORDER BY`, `LIMIT` e `OFFSET`.
- [ ] Trabalhar com `NULL`.
- [ ] Utilizar funções de agregação.
- [ ] Agrupar com `GROUP BY` e `HAVING`.
- [ ] Criar índices.
- [ ] Utilizar `DISTINCT`.
- [ ] Conhecer `CASE` e `COALESCE`.

**Projeto:** catálogo de livros com filtros, pesquisas e estatísticas.

## Nível 3 — Relacionamentos e consistência

- [ ] Entender chaves primárias e estrangeiras.
- [ ] Criar relações entre tabelas.
- [ ] Utilizar `INNER JOIN` e `LEFT JOIN`.
- [ ] Trabalhar com transações.
- [ ] Tratar erros.
- [ ] Criar backups.
- [ ] Entender integridade referencial.

**Projeto:** sistema de biblioteca com autores, livros, usuários e empréstimos.

## Nível 4 — Intermediário

- [ ] Escrever subconsultas.
- [ ] Utilizar CTEs.
- [ ] Conhecer UPSERT.
- [ ] Criar views.
- [ ] Estudar funções de janela.
- [ ] Analisar consultas com `EXPLAIN QUERY PLAN`.
- [ ] Conhecer as limitações de concorrência do SQLite.
- [ ] Aprender a gerenciar conexões, transações e backups corretamente.

**Projeto:** sistema de gerenciamento de biblioteca com relatórios, filtros avançados e controle de empréstimos.

---

# 29. Referência oficial

A documentação oficial é a fonte principal para estudar a sintaxe e os recursos do SQLite:

- Documentação geral: https://www.sqlite.org/docs.html
- Linguagem SQL: https://www.sqlite.org/lang.html
- Tipos de dados: https://www.sqlite.org/datatype3.html
- Transações: https://www.sqlite.org/lang_transaction.html
- Índices: https://www.sqlite.org/lang_createindex.html
- Chaves estrangeiras: https://www.sqlite.org/foreignkeys.html
- Documentação de `sqlite3` para Python: https://docs.python.org/3/library/sqlite3.html

**Recomendação final:** não tente memorizar todos os comandos de uma vez. Crie pequenos programas, observe os resultados, provoque erros deliberadamente em um banco de teste e investigue o motivo. O domínio de banco de dados vem da compreensão de como os dados são estruturados, relacionados, consultados e protegidos — não apenas da memorização de sintaxe.
