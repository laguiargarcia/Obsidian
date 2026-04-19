# Referências — GetFinance

## APIs e Serviços
<!-- AUTO: atualizado pelo /obsidian -->
| Serviço | Link |
|---|---|
| Pluggy Dashboard | https://dashboard.pluggy.ai/applications |
| Pluggy Meu Perfil | https://meu.pluggy.ai/overview |
| Pluggy Docs | https://docs.pluggy.ai/docs/quick-pluggy-introduction |
| Pluggy Quickstart | https://github.com/pluggyai/quickstart |
| Apache Superset Docs | https://superset.apache.org/docs/intro |
| duckdb-engine (SQLAlchemy) | https://github.com/motherduck-ai/duckdb_engine |
| DuckDB Delta Extension | https://duckdb.org/docs/extensions/delta |

## Variáveis de Ambiente
<!-- AUTO -->
Definidas em `.env` (gitignored):
- `CLIENT_ID` — Pluggy client ID
- `CLIENT_SECRET` — Pluggy client secret
- `ITEM_IDS` — IDs de itens Pluggy separados por vírgula

Definidas em `infra/.env` (gitignored):
- `SUPERSET_SECRET_KEY` — chave Flask do Superset
- `SUPERSET_ADMIN_USERNAME` / `SUPERSET_ADMIN_PASSWORD` / `SUPERSET_ADMIN_EMAIL`

## Docker — Comandos Úteis
<!-- AUTO -->
```bash
# Primeira vez
sudo docker compose cp ../scripts/init_duckdb_container.py superset:/tmp/init.py
sudo docker compose exec superset superset db upgrade
sudo docker compose exec superset superset fab create-admin ...
sudo docker compose exec superset superset init
sudo docker compose exec superset python3 /tmp/init.py

# Uso normal
cd infra && sudo docker compose up -d
# Superset: http://localhost:8088
# FastAPI:  http://localhost:8000
```

## Minhas Referências
<!-- MANUAL: edite livremente -->
