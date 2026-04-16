## ADB (Android Debug Bridge)

### Comandos básicos

| Comando | Descrição |
|--------|----------|
| `adb devices` | Lista dispositivos conectados |
| `adb -s IP:PORTA shell` | Acessa o shell de um dispositivo específico |
| `adb pair IP:PORTA` | Faz pareamento com o dispositivo |
| `adb connect IP:PORTA` | Conecta a um dispositivo via rede |

---

### Dispositivo: Z Flip 6

- **IP:** `192.168.0.112`
- **Porta:** `38037`
- **Endereço completo:** `192.168.0.112:38037`

#### Exemplos de uso

```bash
adb -s 192.168.0.112:38037 shell
adb connect 192.168.0.112:38037