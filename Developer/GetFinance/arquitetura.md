# Arquitetura — GetFinance

## Como Funciona
<!-- AUTO: atualizado pelo /obsidian -->
O pipeline usa um padrão de **code injection**: `main.py` concatena `functions.py` e `storage.py` como texto antes de cada script ETL, e executa via `subprocess.run`. Scripts em `etl/` usam tudo de `functions.py` e `storage.py` sem importar explicitamente. SQLAlchemy foi removido — armazenamento migrado para Delta Lake.

## Componentes
<!-- AUTO -->
| Arquivo | Papel |
|---|---|
| `main.py` | Runner do pipeline — valida arquivos, injeta base scripts, executa cada ETL |
| `functions.py` | Cliente Pluggy API — cache de token (TTL 2h), listagem de contas/transações, SparkSession |
| `storage.py` | Helpers Delta Lake — `write_delta(df, path, mode)` e `read_delta(path)` |
| `etl/raw2raw.py` | ETL passo 1 — busca contas e transações da API, salva em Delta (raw) |
| `etl/raw2cleansed.py` | ETL passo 2 — lê raw, aplica type casting e snake_case, salva em Delta (cleansed) |
| `etl/cleansed2curated.py` | ETL passo 3 — placeholder, transformação cleansed → curated |

## Fluxo do Pipeline
<!-- AUTO -->
```
main.py
  → injeta functions.py + storage.py em cada script ETL
  → subprocess.run(python -c "<combined_code>")
  → etl/raw2raw.py       → Pluggy API → Delta (raw)
  → etl/raw2cleansed.py  → Delta (raw) → Delta (cleansed)
  → etl/cleansed2curated.py → Delta (cleansed) → Delta (curated)
```

## Decisões Técnicas
<!-- MANUAL: edite livremente -->

## TODO / Próximos Passos
<!-- MANUAL -->

