## ADB via Wi-Fi (Configuração)

### Requisitos

- Android 11 ou superior no celular  
- PC com ADB instalado (versão recente que suporte `adb pair`)  
- Celular e PC conectados na mesma rede Wi-Fi  

---

### Passos para adicionar um novo celular

1. **Ativar opções de desenvolvedor no celular**

2. **Ativar depuração USB**

3. **Ativar depuração via rede (ADB Wireless)**  
   - Nas opções do desenvolvedor, ativar **Depuração via rede** (ou “ADB Wireless”)

4. **Parear o dispositivo via Wi-Fi no PC**  
   - No celular, aparecerá um **IP, porta e código PIN (ou QR code)**  
   - No PC, rodar:
     ```bash
     adb pair IP:PORTA
     ```

5. **Conectar via ADB**  
   - Após o pareamento:
     ```bash
     adb connect IP:PORTA
     ```
![[Pasted image 20260317191902.png|300]]
   - Confirmar conexão:
     ```bash
     adb devices
     ```