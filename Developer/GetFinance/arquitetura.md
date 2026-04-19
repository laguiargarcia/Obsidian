# Arquitetura — GetFinance

## Como Funciona
<!-- AUTO: atualizado pelo /obsidian -->
Pipeline de notebooks Jupyter em camadas. `ingestion/main.ipynb` orquestra a busca de dados da Pluggy API. ETL processa em 3 passos: landing → raw → cleansed → curated. FastAPI expõe os dados cleansed via DuckDB. Superset conecta ao mesmo DuckDB para dashboards interativos.

## Estrutura de Pastas
<!-- AUTO -->
```
GetFinance/
├── ingestion/          ← main.ipynb, functions.ipynb (Pluggy fetch + SparkSession)
├── etl/                ← notebooks ETL em camadas
│   ├── landing2raw.ipynb
│   ├── raw2cleansed.ipynb
│   └── cleansed2curated.ipynb
├── data/               ← Delta Lake storage
│   ├── raw/
│   ├── cleansed/
│   │   ├── transactions/
│   │   └── accounts/
│   └── getfinance.duckdb   ← DuckDB com views sobre Delta tables
├── api/                ← FastAPI (api.py)
├── infra/              ← Docker Compose (Superset + FastAPI)
│   ├── docker-compose.yml
│   ├── superset/
│   └── fastapi/
├── scripts/            ← utilitários (init_duckdb_container.py)
├── frontend/           ← scaffold (futuro)
├── exports/            ← arquivos exportados pela API
└── docs/
```

## Componentes
<!-- AUTO -->
| Arquivo | Papel |
|---|---|
| `ingestion/main.ipynb` | Orquestra busca de dados Pluggy |
| `ingestion/functions.ipynb` | Cliente Pluggy API — token cache (TTL 2h), SparkSession |
| `etl/landing2raw.ipynb` | Ingestão raw → Delta Lake |
| `etl/raw2cleansed.ipynb` | Limpeza: snake_case, type casting, DateType |
| `etl/cleansed2curated.ipynb` | Transformações finais (placeholder) |
| `api/api.py` | FastAPI — endpoints `/transactions`, `/accounts`, `/categories` |
| `infra/docker-compose.yml` | Sobe Superset + FastAPI em Docker |
| `scripts/init_duckdb_container.py` | Cria views DuckDB dentro do container Superset |

## Fluxo do Pipeline
<!-- AUTO -->
```
Pluggy API
  → ingestion/main.ipynb
  → etl/landing2raw.ipynb     → data/raw/
  → etl/raw2cleansed.ipynb    → data/cleansed/transactions + accounts
  → etl/cleansed2curated.ipynb → (futuro)

data/cleansed/
  → DuckDB (delta extension) → views: transactions, accounts
  → FastAPI /transactions /accounts /categories  (export CSV/JSON/Excel)
  → Superset (Docker)        → dashboards interativos
```

## DuckDB + Delta Lake
<!-- AUTO -->
`api/api.py` usa `duckdb.connect()` in-memory + `LOAD delta` para ler Delta tables diretamente via `delta_scan()`. O arquivo `data/getfinance.duckdb` é persistente e contém views criadas pelo script `init_duckdb_container.py` — usado pelo Superset.

Conexão Superset: `duckdb:////app/data/getfinance.duckdb`

## Decisões Técnicas
<!-- MANUAL: edite livremente -->

## TODO / Próximos Passos
<!-- MANUAL -->
