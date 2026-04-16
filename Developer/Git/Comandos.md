## Adição e Commit

| Comando | Descrição |
|--------|----------|
| `git add <arquivo>` | Adiciona um arquivo à staging area |
| `git add .` | Adiciona todos os arquivos modificados |
| `git commit -m "mensagem"` | Cria um commit com a mensagem |
| `git commit -am "mensagem"` | Adiciona e comita arquivos já monitorados |

---

## Iniciar e Clonar Repositórios

| Comando | Descrição |
|--------|----------|
| `git init` | Inicializa um repositório Git vazio |
| `git clone <url>` | Clona um repositório remoto |

---

## Branch

| Comando | Descrição |
|--------|----------|
| `git branch` | Lista as branches |
| `git branch <nome>` | Cria uma nova branch |
| `git checkout <nome>` | Muda para outra branch |
| `git checkout -b <nome>` | Cria e muda para a nova branch |
| `git merge <branch>` | Faz merge da branch atual com outra |

---

## Status e Histórico

| Comando | Descrição |
|--------|----------|
| `git status` | Mostra o status dos arquivos |
| `git log` | Exibe o histórico de commits |
| `git log --oneline` | Histórico resumido |

---

## Repositório Remoto

| Comando | Descrição |
|--------|----------|
| `git remote -v` | Lista os repositórios remotos |
| `git remote add origin <url>` | Adiciona repositório remoto |
| `git push origin <branch>` | Envia commits para o remoto |
| `git pull origin <branch>` | Baixa alterações do remoto |

---

## Desfazer e Resetar

| Comando | Descrição |
|--------|----------|
| `git checkout -- <arquivo>` | Desfaz mudanças não comitadas |
| `git reset HEAD <arquivo>` | Remove arquivo da staging |
| `git reset --soft HEAD~1` | Remove o último commit, mantendo alterações |
| `git reset --hard HEAD~1` | Remove o último commit e as alterações |
| `git clean -fd` | Remove arquivos não rastreados (⚠️ cuidado!) |

---

## Outros úteis

| Comando | Descrição |
|--------|----------|
| `git diff` | Mostra as diferenças nos arquivos |
| `git stash` | Guarda mudanças temporariamente |
| `git stash pop` | Recupera mudanças guardadas |
| `git tag` | Lista tags |
| `git tag <nome>` | Cria uma tag no commit atual |

---

## Configuração Inicial

| Comando                                          | Descrição                      |
| ------------------------------------------------ | ------------------------------ |
| `git config --global user.name "Seu Nome"`       | Define o nome do usuário       |
| `git config --global user.email "seu@email.com"` | Define o e-mail do usuário     |
| `git config --list`                              | Mostra as configurações atuais |