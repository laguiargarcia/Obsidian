### Instalar pacotes

| Comando                           | Descrição                                                  |
| --------------------------------- | ---------------------------------------------------------- |
| `pip install <pacote1> <pacote2>` | Instala pacotes Python (ex: `pip install fastapi uvicorn`) |

---

### Gerar requirements.txt

| Comando | Descrição |
|--------|----------|
| `pip freeze > requirements.txt` | Gera um arquivo com todas as dependências instaladas e suas versões exatas |

---

### Exemplo de requirements.txt

O `freeze` gera o arquivo com as versões exatas de tudo que está instalado, incluindo dependências indiretas:

```txt
pacote1==1.0.0
pacote2==2.3.4
dependencia-indireta==0.9.1
...