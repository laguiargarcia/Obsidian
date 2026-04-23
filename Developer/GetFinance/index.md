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

### Setup (primeira vez)
```bash
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```
Criar `.env` na raiz:
```
CLIENT_ID=<pluggy client id>
CLIENT_SECRET=<pluggy client secret>
ITEM_IDS=<comma-separated pluggy item ids>
```

### 1. Pipeline (buscar dados)
```bash
cd ingestion
jupyter nbconvert --to notebook --execute --inplace main.ipynb
```
Busca contas e transações da Pluggy → grava Delta Lake em `etl/data/`.

### 2. API
```bash
# local
uvicorn api.api:app --reload

# ou via Docker (FastAPI + Superset)
cd infra && sudo docker compose up -d
# FastAPI:  http://localhost:8000
# Superset: http://localhost:8088
```

### 3. Frontend
```bash
cd frontend
npm install   # primeira vez
npm run dev
```
Acesse: `http://localhost:3000`

> "Atualizar dados" no navbar re-executa o pipeline completo.

## Minhas Notas
<!-- MANUAL: edite livremente -->
