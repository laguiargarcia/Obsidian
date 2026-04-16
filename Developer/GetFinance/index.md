# GetFinance

## Visão Geral
<!-- AUTO: atualizado pelo /obsidian -->
Pipeline ETL em Python que busca dados financeiros da API Pluggy.ai (open banking brasileiro) e os processa com PySpark. Armazena dados em Delta Lake em camadas (raw → cleansed → curated).

## Stack
<!-- AUTO -->
- **Linguagem:** Python
- **Processamento de dados:** PySpark + Delta Lake
- **API:** Pluggy.ai (open banking)
- **Storage:** Delta Lake (`storage.py`)
- **Config:** python-dotenv

## Status
<!-- AUTO -->
Desenvolvimento ativo. Commits recentes:
- `70cb32e` update
- `dca5763` remove CLAUDE.md from .gitignore
- `2da0089` remove CLAUDE.md from repo
- `154675f` chore: remove dataBase.py and SQLAlchemy dependency
- `b107382` feat: add cleansed2curated placeholder ETL step
- `98e7a30` fix: remove unused lit import from test_cleansed.py
- `f1d6637` feat: rewrite raw2cleansed to use Delta Lake with type casting and snake_case
- `1b81b49` feat: add raw2raw ETL step to fetch and store accounts and transactions
- `7bfc840` feat: update pipeline to use storage.py and 3 ETL steps

## Minhas Notas
<!-- MANUAL: edite livremente -->

