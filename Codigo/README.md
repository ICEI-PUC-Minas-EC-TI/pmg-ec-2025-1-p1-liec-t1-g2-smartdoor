# SMART DOOR - Protótipo de Fechadura Eletrônica com ESP32

**Desenvolvedor:** Gabriel Campos Amaral Ribeiro

---

## 📖 Descrição do Projeto

Este é um **protótipo de sistema de controle de acesso** utilizando a placa **ESP32**, desenvolvido para simular o funcionamento de uma fechadura eletrônica.

O projeto integra diferentes tecnologias para controlar a abertura e fechamento de uma porta, utilizando:

- Leitura de cartões/chaveiros RFID autorizados.
- Ativação por sensor de toque capacitivo (3 toques consecutivos).
- Controle remoto via Bluetooth Serial.
- Botão físico para saída manual.

O sistema exibe mensagens em um display LCD I2C, emite alertas sonoros via buzzer e indica o status da porta com LEDs.

Este protótipo é ideal para simular o funcionamento em ambientes como portas de quarto ou espaços com baixo nível de segurança.

Para aplicações que exigem maior proteção, como portas de áreas sigilosas ou ambientes profissionais, são necessárias melhorias que serão desenvolvidas ao longo do curso.

---

## ⚙️ Funcionalidades do Protótipo

| Funcionalidade                     | Descrição                                                                                      |
|----------------------------------|------------------------------------------------------------------------------------------------|
| **Controle via RFID**             | Leitura dos cartões/chaveiros autorizados para simular a liberação de acesso.                  |
| **Sensor capacitivo para abertura** | Abre a porta ao detectar 3 toques consecutivos, como alternativa ao RFID.                      |
| **Bluetooth Serial**              | Recebe comandos `'1'` (abrir) e `'2'` (fechar) para controle remoto via app Android.           |
| **Botão físico para saída**       | Permite abrir a porta manualmente via botão conectado ao ESP32.                                |
| **Display LCD 16x2 I2C**          | Exibe mensagens simulando o status da porta e interações do usuário.                          |
| **Buzzer para alertas sonoros**   | Emite sons para indicar permissões, erros e avisos.                                           |
| **Indicadores LED**               | LEDs indicam visualmente o estado da porta (aberta ou fechada).                               |
| **Fechamento automático**         | Porta fecha automaticamente após tempo configurável (padrão: 3 segundos).                     |

---

## 📋 Componentes Utilizados

| Componente                  | Modelo / Tipo                | Função no protótipo                     |
|----------------------------|-----------------------------|----------------------------------------|
| **Placa**                  | ESP32 Dev Module            | Controlador do sistema                  |
| **Leitor RFID**            | MFRC522                    | Simula leitura de cartões/chaveiros    |
| **Servo Motor**            | SG90 ou similar             | Simula abertura e fechamento da porta  |
| **Display LCD**            | 16x2 com I2C (0x27)         | Mostra mensagens do sistema             |
| **Sensor de Toque**        | Capacitivo (ex: TTP223)      | Entrada alternativa para abertura      |
| **Buzzer**                 | Piezo buzzer                 | Simula alertas sonoros                  |
| **LED Verde e Vermelho**   | LEDs comuns                  | Indicadores visuais da porta            |
| **Botão Físico**           | Push button                 | Simula botão de saída                    |
| **Cabos e Protoboard**     | -                           | Conexões entre componentes              |

---

## 🔌 Diagrama de Conexões

| Dispositivo             | Pino ESP32 GPIO  | Observações                            |
|------------------------|------------------|--------------------------------------|
| RFID - SDA (SS)        | 5                | Comunicação SPI                      |
| RFID - RST             | 22               | Reset do módulo RFID                 |
| Servo Motor            | 14               | Controle do servo motor              |
| Buzzer                 | 13               | Saída para buzzer                    |
| Botão Saída            | 15               | Entrada com pull-up interno          |
| LED Verde              | 25               | Saída para LED verde                 |
| LED Vermelho           | 26               | Saída para LED vermelho              |
| Sensor Toque Capacitivo| 32               | Entrada para sensor capacitivo       |
| LCD I2C - SDA          | 33               | Comunicação I2C                     |
| LCD I2C - SCL          | 27               | Comunicação I2C                     |

---

## 🛠️ Bibliotecas e Software Necessários

- **IDE:** Arduino IDE (versão recomendada >= 1.8.13)
- **Placa:** ESP32 Dev Module (instalar suporte ESP32 via Board Manager)
- **Bibliotecas:**
  - [ESP32Servo](https://github.com/khoih-prog/ESP32Servo) — controle servo com ESP32
  - [MFRC522](https://github.com/miguelbalboa/rfid) — leitor RFID
  - [LiquidCrystal_I2C](https://github.com/fdebrabander/Arduino-LiquidCrystal-I2C-library) — display LCD via I2C
  - **BluetoothSerial** — já incluso no core ESP32

---

## 🧩 Como Configurar e Testar o Protótipo

1. **Configurar IDE Arduino:**

   - Instale suporte ao ESP32 pela Board Manager (adicionando URL conforme documentação ESP32).
   - Selecione a placa `ESP32 Dev Module`.

2. **Instalar bibliotecas necessárias:**

   - Usando o Gerenciador de Bibliotecas do Arduino IDE, instale as bibliotecas listadas acima.

3. **Montar hardware conforme o diagrama.**

4. **Carregar o código:**

   - Copie o código fonte do projeto no Arduino IDE.
   - Ajuste UIDs para os cartões/chaveiros que deseja usar na simulação.
   - Confirme o endereço I2C do seu display.
   - Faça upload do código para a placa ESP32.

5. **Testar funcionalidades:**

   - Observe o display e o comportamento do servo, LEDs e buzzer.
   - Teste a aproximação de cartões autorizados.
   - Experimente o sensor capacitivo e o botão físico.
   - Utilize o app Android **Bluetooth Serial Terminal** para enviar comandos `'1'` (abrir) e `'2'` (fechar).

---

## 📲 Controle via Bluetooth

Para simular o controle remoto via Bluetooth, utilize o app **Bluetooth Serial Terminal** para Android:

- Pareie seu celular com o dispositivo **"SMART_DOOR"**.
- Envie `'1'` para abrir e `'2'` para fechar a porta.

**Nota:** Este app funciona apenas em Android. Outros sistemas podem precisar de apps compatíveis com Bluetooth Serial clássico.

---

## ⚠️ Considerações Importantes

Este projeto é um **protótipo para fins educacionais e de simulação**.

- Funciona bem para ambientes simples, como portas de quarto ou espaços com baixo nível de segurança.
- Para usos mais críticos, o sistema precisa de aprimoramentos de segurança, robustez, criptografia, autenticação rigorosa e outros recursos, que serão desenvolvidos ao longo do curso.
- Não utilize este protótipo como sistema definitivo em locais que exijam proteção avançada.

---

## 💡 Possíveis Melhorias Futuras

- Inclusão de autenticação mais segura (ex: criptografia RFID, biometria).
- Integração com sistemas de alarme e notificação remota.
- Registro e log de acessos.
- Uso de protocolos Bluetooth mais seguros (BLE com pairing).
- Melhoria mecânica e elétrica para aplicação em portas reais.

---

## 🙏 Agradecimentos

Este projeto foi desenvolvido com apoio de:

- **ChatGPT (OpenAI)** — para tirar dúvidas e ajudar no desenvolvimento do código e documentação.  
  [https://chat.openai.com](https://chat.openai.com)

- **Stack Overflow** — referência para soluções e dúvidas técnicas.  
  [https://stackoverflow.com](https://stackoverflow.com)

---

## 📞 Contato

Gabriel Campos Amaral Ribeiro  
[Seu E-mail ou LinkedIn]  

Sinta-se à vontade para contribuir com sugestões, dúvidas ou melhorias.

---

Obrigado por acompanhar este protótipo do **SMART DOOR**!  
Este é um projeto em constante evolução para aprendizado e experimentação.

---

