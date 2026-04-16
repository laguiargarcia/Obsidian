# Arquitetura — GetFinance

## Como Funciona
<!-- AUTO: atualizado pelo /obsidian -->
O pipeline usa um padrão incomum de **code injection**: `main.py` concatena os arquivos `functions.py` e `dataBase.py` como texto antes de cada script ETL, e executa a combinação via `subprocess.run`. Isso permite que os scripts em `etl/` usem tudo de `functions.py` e `dataBase.py` sem precisar importá-los explicitamente.

## Componentes
<!-- AUTO -->
| Arquivo | Papel |
|---|---|
| `main.py` | Runner do pipeline — valida arquivos, injeta scripts base, executa cada ETL |
| `functions.py` | Cliente da API Pluggy — cache de token (TTL 2h), listagem de contas, inicializa SparkSession |
| `dataBase.py` | Modelos ORM SQLAlchemy (tabela `Accounts`) |
| `etl/raw2cleansed.py` | ETL passo 1 — chama `list_accounts()`, lê `dados.json` com Spark |

## Fluxo do Pipeline
<!-- AUTO -->
```
main.py
  → injeta functions.py + dataBase.py em cada script ETL
  → subprocess.run(python -c "<combined_code>")
  → etl/raw2cleansed.py
     → list_accounts() → Pluggy API
     → lê dados.json com Spark
```

## Decisões Técnicas
<!-- MANUAL: edite livremente -->

## TODO / Próximos Passos
<!-- MANUAL -->

