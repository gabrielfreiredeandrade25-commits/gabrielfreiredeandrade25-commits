# Como criar um novo repositório **privado** para suas anotações SQL

Este projeto atual é o seu perfil.  
Para não misturar com commits do profile, o ideal é publicar as notas em outro repositório.

## Opção 1) Pelo site do GitHub (mais simples)

1. Acesse: https://github.com/new
2. Repository name: `sql-notes-postgresql` (ou outro nome que preferir).
3. Marque **Private**.
4. Clique em **Create repository**.

Depois, no seu computador:

```bash
git clone <URL_DO_NOVO_REPOSITORIO_PRIVADO>
cd <NOME_DO_NOVO_REPOSITORIO>
mkdir -p notes
```

Copie este arquivo de estudo para lá:

```bash
cp ../gabrielfreiredeandrade25-commits/notes/sql-glossario-postgresql.md notes/
```

Faça o primeiro commit:

```bash
git add .
git commit -m "docs: adiciona glossário SQL PostgreSQL"
git push origin main
```

## Opção 2) Via GitHub CLI (`gh`)

```bash
mkdir sql-notes-postgresql
cd sql-notes-postgresql
git init
mkdir -p notes
cp ../gabrielfreiredeandrade25-commits/notes/sql-glossario-postgresql.md notes/
git add .
git commit -m "docs: adiciona glossário SQL PostgreSQL"
gh repo create sql-notes-postgresql --private --source=. --remote=origin --push
```

## Estrutura sugerida do novo repositório

```text
sql-notes-postgresql/
  notes/
    sql-glossario-postgresql.md
  README.md
```

Se quiser, eu também posso montar o `README.md` desse novo repositório para você em formato de caderno de estudos.
