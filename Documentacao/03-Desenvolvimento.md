# Desenvolvimento do Projeto

## Materiais

Os materiais utilizados no projeto foram:

- Placa ESP32 Dev Module como controlador principal.
- Módulo RFID MFRC522 para leitura de cartões e chaveiros.
- Servo motor SG90 para simular a trava da porta, substituindo a trava elétrica original.
- Display LCD 16x2 com interface I2C para exibir mensagens ao usuário.
- Sensor de toque capacitivo (ex: TTP223).
- Buzzer piezoelétrico para alertas sonoros.
- LEDs verde e vermelho para indicar o status da porta.
- Botão físico para simular a saída manual.
- Protoboard para montagem do circuito.

Observações importantes:
- O teclado original não foi utilizado, pois estava defeituoso e devido à limitação do número de portas do ESP32.
- A trava elétrica não pôde ser usada junto com o relé por limitações de tensão.
- A alimentação foi feita via USB do computador durante o desenvolvimento, com bateria como opção para uso externo.
- A montagem poderia ser melhorada com uma placa de circuito impresso para melhorar organização e estética, já que a protoboard apresentou dificuldades na padronização dos fios e disponibilidade limitada de cabos.

---

## Desenvolvimento

O desenvolvimento do projeto foi dividido em etapas que contemplaram a criação do aplicativo, a montagem do hardware, o desenvolvimento dos códigos e a integração entre app e hardware.

### Desenvolvimento do Aplicativo

#### Interface

O aplicativo foi desenvolvido no MIT App Inventor, uma plataforma visual que permite criar aplicativos Android de forma intuitiva, utilizando blocos de programação.

O app possui duas telas principais:
- Tela de entrada, usada para configurações iniciais;
- Tela de controle, onde o usuário pode enviar comandos para abrir ou fechar a porta.

Há também um indicador visual no app que informa o status da porta (aberta ou fechada), proporcionando feedback imediato ao usuário.

#### Código

O código do aplicativo foi desenvolvido utilizando a programação em blocos do MIT App Inventor, que facilita a construção da lógica de comunicação sem a necessidade de escrever código textual.

A comunicação entre o app e o ESP32 é feita via Bluetooth Serial padrão, enviando comandos simples:
- `'1'` para abrir a porta;
- `'2'` para fechar a porta.

O app também recebe mensagens do ESP32 para atualizar o indicador de status da porta, garantindo que o usuário esteja sempre informado.

Por enquanto, o app não possui mecanismos avançados de autenticação, tratamento de erros ou reconexão automática, sendo uma versão inicial focada na funcionalidade básica.

---

### Desenvolvimento do Hardware

#### Montagem

A montagem foi feita em protoboard, facilitando testes e ajustes.

Devido a problemas no teclado e limitações de portas, o teclado não foi utilizado.

A trava elétrica foi substituída por um servo motor devido à incompatibilidade de tensão com o relé.

A alimentação principal foi por USB do computador, com bateria disponível para uso externo.

Houve dificuldades para padronizar os fios, devido à falta de cabos nas cores e tamanhos adequados.

#### Desenvolvimento do Código

O código do ESP32 foi desenvolvido na Arduino IDE versão 2.3.6.

Foram utilizadas as bibliotecas ESP32Servo, MFRC522, LiquidCrystal_I2C e BluetoothSerial.

Inicialmente houve desafios para identificar as bibliotecas corretas para cada componente.

O código está estruturado em funções e procedimentos para garantir organização e legibilidade.

O desenvolvimento do código foi mais simples do que o esperado.

---

### Comunicação entre App e Hardware

A comunicação entre o aplicativo Android e o ESP32 ocorre via Bluetooth Serial clássico.

O app envia comandos de texto simples (`'1'` para abrir e `'2'` para fechar).

O ESP32 recebe os comandos, controla o servo, buzzer, LEDs e display, e envia de volta o status da porta para o app.

O protocolo é direto e sem complexidade.

Não foram observadas instabilidades na comunicação durante os testes.

O app atual para simulação é exclusivo para Android, desenvolvido no MIT App Inventor.

---

