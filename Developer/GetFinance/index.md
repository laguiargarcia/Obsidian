# GetFinance

## Visão Geral
<!-- AUTO: atualizado pelo /obsidian -->
Pipeline ETL em Python que busca dados financeiros da API Pluggy.ai (open banking brasileiro), processa com PySpark/Delta Lake e expõe via FastAPI + Apache Superset. Objetivo final: app multi-usuário onde cada pessoa conecta sua própria conta Pluggy e configura dashboards personalizados — similar ao Power BI, mas self-hosted.

## Stack
<!-- AUTO -->
- **Linguagem:** Python + Jupyter Notebooks
- **Ingestão:** Pluggy.ai API (open banking BR)
- **Processamento:** PySpark + Delta Lake
- **Query engine:** DuckDB (lê Delta Lake diretamente)
- **API:** FastAPI (`api/api.py`) — exporta CSV/JSON/Excel
- **Dashboard:** Apache Superset (Docker) — UI tipo PBI para usuários
- **Infra:** Docker Compose (`infra/docker-compose.yml`)
- **Config:** python-dotenv

## Visão de Produto
<!-- AUTO -->
```
Pluggy API → Spark ETL → Delta Lake → DuckDB → FastAPI → Superset (frontend)
```
Fases planejadas:
1. **Export API** ✅ — FastAPI lê Delta via DuckDB, exporta CSV/JSON/Excel
2. **Dashboard** 🔄 — Superset embedado, usuário constrói visões (em andamento)
3. **Frontend customizado** — Wrapper React/Next.js com Superset embedado
4. **Multi-usuário** — Auth, credenciais Pluggy por usuário, Delta paths por usuário
5. **Pipeline configurável** — Usuário escolhe contas, datas, categorias, camadas ETL

## Status
<!-- AUTO -->
Desenvolvimento ativo. Commits recentes:
- `29f5c0f` add MIT license
- `9a95511` update
- `a53ac80` update
- `70cb32e` update
- `dca5763` remove CLAUDE.md from .gitignore
- `154675f` chore: remove dataBase.py and SQLAlchemy dependency
- `b107382` feat: add cleansed2curated placeholder ETL step

Superset sendo configurado via Docker Compose — conectando ao DuckDB com delta extension.

## Como Rodar
<!-- AUTO -->

### Pré-requisitos
- `.env` na raiz com `CLIENT_ID`, `CLIENT_SECRET`, `ITEM_IDS`
- `venv` criado: `pip install -r requirements.txt`
- Docker instalado (para Superset/FastAPI)

### Pipeline ETL (Jupyter)
Rodar os notebooks em ordem:
```
1. ingestion/main.ipynb         ← busca dados da Pluggy API
2. etl/landing2raw.ipynb        ← ingestão → Delta Lake raw
3. etl/raw2cleansed.ipynb       ← limpeza → Delta Lake cleansed
4. etl/cleansed2curated.ipynb   ← transformações finais
```

### Serviços (Docker)
```bash
cd infra && sudo docker compose up -d
# Superset:  http://localhost:8088
# FastAPI:   http://localhost:8000
```

### Primeira vez (setup Superset)
```bash
sudo docker compose cp ../scripts/init_duckdb_container.py superset:/tmp/init.py
sudo docker compose exec superset superset db upgrade
sudo docker compose exec superset superset init
sudo docker compose exec superset python3 /tmp/init.py
```

## Minhas Notas
<!-- MANUAL: edite livremente -->
