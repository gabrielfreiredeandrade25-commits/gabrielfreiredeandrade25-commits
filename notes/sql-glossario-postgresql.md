# 📘 Glossário SQL (PostgreSQL) — Básico e Intermediário

Anotações organizadas para consulta rápida durante os estudos.

---

## Como acessar este material

### No GitHub
1. Acesse o repositório.
2. Entre na pasta `notes/`.
3. Abra o arquivo `sql-glossario-postgresql.md`.

### Localmente (no computador)
1. Clone o repositório:
   ```bash
   git clone <URL_DO_REPOSITORIO>
   ```
2. Entre na pasta:
   ```bash
   cd <NOME_DO_REPOSITORIO>
   ```
3. Abra o arquivo `notes/sql-glossario-postgresql.md` no VS Code, Cursor ou editor de texto.

---

## 1) Comandos base de consulta

- **SELECT**: seleciona colunas que você quer ver no resultado.
- **FROM**: define de qual tabela (ou conjunto de dados) os dados serão lidos.
- **WHERE**: filtra linhas com base em uma condição.
- **ORDER BY**: ordena o resultado (ASC crescente / DESC decrescente).
- **LIMIT**: restringe a quantidade de linhas retornadas (ótimo para explorar dados grandes).

Exemplo:

```sql
SELECT nome, salario
FROM funcionarios
WHERE salario > 3000
ORDER BY salario DESC
LIMIT 10;
```

## 2) Operadores e filtros

- **=**: igual.
- **<>** ou **!=**: diferente.
- **>**, **<**, **>=**, **<=**: comparações numéricas.
- **IN (...)**: verifica se o valor está em uma lista.
- **BETWEEN x AND y**: intervalo (inclui extremos).
- **LIKE**: busca por padrão (`%` para vários caracteres, `_` para um).
- **IS NULL / IS NOT NULL**: valida valores nulos.

Exemplo:

```sql
SELECT *
FROM pedidos
WHERE status IN ('enviado', 'entregue')
  AND data_pedido BETWEEN '2026-01-01' AND '2026-03-31';
```

## 3) Funções de agregação

- **COUNT()**: conta linhas.
- **SUM()**: soma valores.
- **MIN()**: menor valor.
- **MAX()**: maior valor.
- **AVG()**: média.
- **DISTINCT**: remove duplicidade antes do resultado/operação.
- **COUNT(DISTINCT coluna)**: conta valores únicos.
- **AS**: cria apelido (alias) temporário para coluna/tabela.

Exemplo:

```sql
SELECT
  departamento,
  COUNT(*) AS total_funcionarios,
  AVG(salario) AS media_salarial
FROM funcionarios
GROUP BY departamento;
```

## 4) Chaves (keys) — básicas e intermediárias

### Chaves básicas

- **PRIMARY KEY (PK)**: identifica cada registro de forma única e não permite `NULL`.
- **FOREIGN KEY (FK)**: cria relação entre tabelas, referenciando a PK (ou UNIQUE) de outra tabela.

### Chaves/constraints intermediárias

- **UNIQUE**: impede valores duplicados em uma coluna.
- **NOT NULL**: obriga preenchimento da coluna.
- **CHECK**: valida regra de negócio (ex.: salário > 0).
- **DEFAULT**: define valor padrão automático.
- **PRIMARY KEY composta**: PK formada por duas ou mais colunas.

Exemplo:

```sql
CREATE TABLE clientes (
  cliente_id SERIAL PRIMARY KEY,
  email TEXT UNIQUE NOT NULL,
  nome TEXT NOT NULL
);

CREATE TABLE pedidos (
  pedido_id SERIAL PRIMARY KEY,
  cliente_id INT NOT NULL,
  valor_total NUMERIC(10,2) CHECK (valor_total >= 0),
  criado_em TIMESTAMP DEFAULT NOW(),
  CONSTRAINT fk_pedido_cliente
    FOREIGN KEY (cliente_id) REFERENCES clientes(cliente_id)
);
```

## 5) Joins (intermediário essencial)

- **INNER JOIN**: traz somente registros com correspondência nas duas tabelas.
- **LEFT JOIN**: traz todos da esquerda + correspondências da direita.
- **RIGHT JOIN**: traz todos da direita + correspondências da esquerda.
- **FULL JOIN**: traz todos os registros de ambas, com ou sem correspondência.

Exemplo:

```sql
SELECT c.nome, p.pedido_id, p.valor_total
FROM clientes c
LEFT JOIN pedidos p ON c.cliente_id = p.cliente_id;
```

## 6) Dica de estudo prático

Ordem mental para escrever consultas:
1. **FROM/JOIN** (de onde vêm os dados)
2. **WHERE** (filtros)
3. **GROUP BY** (agrupamento, se houver)
4. **HAVING** (filtro de grupos)
5. **SELECT** (colunas finais)
6. **ORDER BY**
7. **LIMIT**
