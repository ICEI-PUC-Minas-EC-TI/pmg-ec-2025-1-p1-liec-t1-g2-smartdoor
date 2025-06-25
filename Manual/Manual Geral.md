# Manual de Operação – Protótipo SMART DOOR (Fechadura Eletrônica com ESP32)

> Este manual parte do princípio que o hardware já está montado e alimentado.

---

## 1. Inicialização do Sistema

1. Ligue a alimentação (via USB ou fonte 5V).  
2. No display LCD 16x2, aguarde a mensagem:  
   SMART DOOR – Pronto  
3. O LED vermelho permanecerá aceso, indicando que a porta está fechada.

---

## 2. Abertura da Porta

Disponível por quatro métodos:

### 2.1 Leitura de Cartão RFID

- Aproxime o cartão ou chaveiro RFID do leitor.  
- O LCD mostrará:  
  Lendo cartão...  
- Se autorizado:  
  - LCD:  
    Acesso Permitido  
    Porta Aberta!  
  - Buzzer: 1 beep curto  
  - LED verde aceso  
  - Servo destrava a porta  
- Se não autorizado:  
  - LCD:  
    Acesso Negado  
  - Buzzer: 3 beeps curtos  
  - LED vermelho pisca 3 vezes

### 2.2 Sensor Capacitivo (Toque)

- Toque três vezes seguidas no sensor capacitivo, com intervalo ≤ 1,5 s.  
- O LCD pode mostrar:  
  Toque 1   Toque 2   Toque 3  
- Após o terceiro toque, realiza o mesmo procedimento de abertura do item 2.1.

### 2.3 Comando Bluetooth Serial

- Emparelhe o smartphone com o ESP32 via app “Bluetooth Serial Terminal”.  
- Envie o caractere '1'.  
- O LCD mostrará:  
  Comando BT: Abrir  
  Porta Aberta!  
- LED verde aceso e buzzer com beep curto.

### 2.4 Botão Físico de Saída (Interno)

- Pressione o botão conectado ao GPIO 15.  
- Executa o mesmo fluxo de abertura (ideal para saída interna).

---

## 3. Fechamento da Porta

### 3.1 Fechamento Manual via Bluetooth

- Envie o caractere '2' pelo app Bluetooth.  
- LCD:  
  Comando BT: Fechar  
  Porta Fechada!  
- Buzzer: 1 beep longo  
- LED vermelho aceso  
- Servo retorna à posição de fechamento.

### 3.2 Fechamento Manual pelo Botão (Interno)

- Pressione novamente o botão de saída.  
- LCD:  
  Porta Fechada!  
- Buzzer e LED vermelho conforme acima.

### 3.3 Fechamento Automático

- Após tempo definido (ex: 5 s), o sistema inicia contagem:  
  Fechando em 3...  
  Fechando em 2...  
  Fechando em 1...  
- Durante a contagem:  
  - Buzzer: 2 beeps curtos  
  - LED vermelho pisca  
- Após contagem, servo fecha a porta, LED vermelho permanece aceso, LCD mostra “Porta Fechada!”.  

*Configuração:* tempo ajustável via variável TEMPO_FECHAMENTO_MS no código.

---

## 4. Indicadores Visuais e Sonoros

| Evento                             | LCD                       | Buzzer                   | LED               |
| ---------------------------------- | ------------------------- | ------------------------ | ----------------- |
| Sistema pronto                     | SMART DOOR – Pronto       | —                        | Vermelho estático |
| Acesso autorizado                  | Porta Aberta!             | 1 beep curto             | Verde estático    |
| Acesso negado                      | Acesso Negado             | 3 beeps curtos           | Vermelho pisca    |
| Comando BT recebido (abrir/fechar) | Comando BT: Abrir/Fechar  | 1 beep (longo p/ fechar) | Verde ou Vermelho |
| Aviso de fechamento automático     | Contagem regressiva (3–1) | 2 beeps curtos           | Vermelho pisca    |

---

## 5. Dicas de Uso

- Mantenha o cartão RFID a até 2 cm do leitor.  
- Toque no sensor capacitivo com a ponta do dedo, sem luvas.  
- Certifique-se de emparelhar o Bluetooth antes de usar o app.  
- Use o botão interno para abertura rápida ao sair por dentro.

---

## 6. Solução de Problemas

- Cartão RFID não reconhecido: verifique alimentação 3,3 V e conexões MOSI, MISO, SCK, SS, RST.  
- Toques no sensor não reconhecidos: cheque aterramento (GND) e evite interferências.  
- Bluetooth não conecta: refaça pareamento no celular e reinicie o ESP32.  
- Servo trava ou faz ruído: use alimentação externa 5 V com corrente ≥ 1 A.

---

Pronto! Agora você pode operar o seu protótipo SMART DOOR. Para dúvidas, consulte o código-fonte ou fale com a equipe de desenvolvimento.
