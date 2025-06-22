# SMART DOOR - Protótipo de Fechadura Eletrônica com ESP32 (Código Arduino)

**Desenvolvedor:** Gabriel Campos Amaral Ribeiro

---

## 📖 Sobre o Código

Este código é um **protótipo de sistema de controle de acesso** desenvolvido para a placa **ESP32**, simulando uma fechadura eletrônica integrada com:

- Leitura de cartões/chaveiros RFID autorizados (3 UIDs pré-definidos).
- Sensor capacitivo que libera o acesso após 3 toques consecutivos.
- Controle remoto via Bluetooth Serial (comandos `'1'` para abrir e `'2'` para fechar).
- Botão físico para saída manual.
- Indicações visuais via display LCD I2C 16x2.
- Alertas sonoros com buzzer.
- LEDs indicativos de status da porta.
- Fechamento automático após tempo configurável.

O código é estruturado para facilitar entendimento e modificações, ideal para quem está aprendendo a integrar hardware e software em projetos com ESP32.

---

## ⚙️ Principais Funções do Código

| Função                   | Descrição                                                                                           |
|-------------------------|----------------------------------------------------------------------------------------------------|
| `compararUID()`          | Compara o UID lido do cartão RFID com UIDs autorizados.                                            |
| `abrirPorta()`           | Abre a porta (aciona servo, LEDs, buzzer e exibe mensagem no LCD).                                  |
| `fecharPorta()`          | Fecha a porta com contagem regressiva, alerta sonoro e visual, e atualização do LCD.               |
| `buzinar()`              | Emite beep curto para sinalização positiva.                                                       |
| `buzinar_erro()`         | Emite 3 beeps para sinalizar acesso negado.                                                       |
| `avisar_fechamentoPorta()`| Pisca LED e buzina para avisar fechamento iminente da porta.                                      |
| `sensorToque()`          | Lê sensor capacitivo e, após 3 toques, abre a porta.                                               |
| `mostrarMensagemLCD()`   | Atualiza mensagens no display LCD I2C.                                                            |

---

## 🔌 Pinos Definidos no Código

| Função                 | Pino ESP32 GPIO  |
|------------------------|------------------|
| RFID SDA (SS)          | 5                |
| RFID RST               | 22               |
| Servo Motor            | 14               |
| Buzzer                 | 13               |
| Botão saída            | 15               |
| LED Verde              | 25               |
| LED Vermelho           | 26               |
| Sensor Toque Capacitivo| 32               |
| LCD I2C SDA            | 33               |
| LCD I2C SCL            | 27               |

---

## 📋 Bibliotecas Usadas

- `SPI.h` — comunicação SPI para RFID  
- `MFRC522.h` — controle do leitor RFID MFRC522  
- `ESP32Servo.h` — controle de servo motor no ESP32  
- `Wire.h` — comunicação I2C para display LCD  
- `LiquidCrystal_I2C.h` — interface para display LCD via I2C  
- `BluetoothSerial.h` — comunicação serial via Bluetooth do ESP32  

---

## 🚀 Como Usar o Código

1. Configure a IDE Arduino para a placa **ESP32 Dev Module**.  
2. Instale as bibliotecas necessárias (listadas acima).  
3. Ajuste os UIDs das variáveis `uid1`, `uid2` e `uid3` para os cartões/chaveiros que pretende autorizar.  
4. Monte o circuito conforme o diagrama de pinos definido acima.  
5. Carregue o código na placa ESP32.  
6. Para controlar via Bluetooth, use o app Android **Bluetooth Serial Terminal** e envie `'1'` para abrir e `'2'` para fechar.  
7. O sensor capacitivo permite abrir a porta após 3 toques seguidos com intervalo de 1.5s.  
8. O botão físico pode ser usado para abrir a porta manualmente.  
9. O display LCD indica status e mensagens para o usuário.  

---

## ⚠️ Observações Importantes

- Este código é um protótipo educacional para simulação e aprendizado.  
- Funciona bem para portas de quarto ou espaços com baixo nível de segurança.  
- Para aplicações que demandem alta segurança, são necessárias melhorias de autenticação, criptografia e hardware mais robusto, que serão implementadas ao longo do curso conforme formos adquirindo conhecimento.
- O app **Bluetooth Serial Terminal** utilizado para controle Bluetooth funciona somente em Android.  

---

## 📚 Referências

Este projeto contou com o auxílio de:

- **ChatGPT (OpenAI)** — suporte para dúvidas e erros.  
  [https://chat.openai.com](https://chat.openai.com)  

- **Stack Overflow** — solução de dúvidas técnicas e exemplos.  
  [https://stackoverflow.com](https://stackoverflow.com)  

- **Documentação oficial Arduino** — referência para programação e uso da IDE.  
  [https://www.arduino.cc/en/Reference/HomePage](https://www.arduino.cc/en/Reference/HomePage)
---

Se precisar de ajuda ou quiser sugerir melhorias, fique à vontade para abrir issues ou pull requests no repositório!

---


---



