# Desenvolvimento do Projeto

## Materiais

Os materiais utilizados no projeto foram:

- (1) Placa ESP32 Dev Module como controlador principal.
- (1) Módulo RFID MFRC522 para leitura de cartões e chaveiros.
- (1) Servo motor SG90 para simular a trava da porta, substituindo a trava elétrica original.
- (1) Display LCD 16x2 com interface I2C para exibir mensagens ao usuário.
- (1) Sensor de toque capacitivo (ex: TTP223).
- (1) Buzzer piezoelétrico para alertas sonoros.
- (2) LEDs verde e vermelho para indicar o status da porta.
- (1) Botão físico para simular a saída manual.
- (1) Protoboard para montagem do circuito.
- (2) Resistores de 4.7kΩ 

Observações importantes:
- O teclado original não foi utilizado, pois estava defeituoso e devido à limitação do número de portas do ESP32.
- A trava elétrica não pôde ser usada junto com o relé por limitações de tensão.
- A alimentação foi feita via USB do computador durante o desenvolvimento, com bateria como opção para uso externo.
---

## Desenvolvimento

O desenvolvimento do projeto foi dividido em etapas que contemplaram a criação do aplicativo, a montagem do hardware, o desenvolvimento dos códigos e a integração entre app e hardware.

### Desenvolvimento do Aplicativo

#### Interface

O aplicativo foi desenvolvido no MIT App Inventor, uma plataforma visual que permite criar aplicativos Android de forma intuitiva, utilizando blocos de programação.

O app possui duas telas principais:
- Tela de entrada, usada para configurações iniciais;
- Tela de controle, onde o usuário pode enviar comandos para abrir ou fechar a porta.

#### Código

O código do aplicativo foi desenvolvido utilizando a programação em blocos do MIT App Inventor, que facilita a construção da lógica de comunicação sem a necessidade de escrever código textual devido so uso da programação em blocos.

A comunicação entre o app e o ESP32 é feita via Bluetooth Serial padrão, enviando comandos simples após o botão ser pressionado:
- `'1'` para abrir a porta;
- `'2'` para fechar a porta.

Por enquanto, o app não possui mecanismos avançados de autenticação, tratamento de erros ou reconexão automática, sendo uma versão inicial focada na funcionalidade básica.

---

### Desenvolvimento do Hardware

#### Montagem

- A montagem foi realizada em protoboard para facilitar testes e ajustes durante o desenvolvimento.
- O teclado físico não foi utilizado devido a problemas no componente e limitações do número de portas disponíveis no ESP32.
- A trava elétrica original foi substituída por um servo motor, pois houve incompatibilidade da trava elétrica com o relé devido à tensão.
- A alimentação do sistema ocorreu principalmente via USB do computador, com bateria disponível para uso externo.
- Durante a montagem, houve dificuldades em padronizar os fios, causadas pela falta de cabos com cores e tamanhos adequados.
- Para futuras melhorias, recomenda-se o uso de uma placa de circuito impresso para aprimorar a organização e a estética do projeto.

#### Desenvolvimento do Código

- O código do ESP32 foi desenvolvido utilizando a Arduino IDE versão 2.3.6.
- Foram utilizadas as bibliotecas ESP32Servo, MFRC522, LiquidCrystal_I2C e BluetoothSerial para controlar os componentes.
- Inicialmente houve desafios para encontrar as bibliotecas corretas para cada componente, mas isso foi superado.
- O código foi estruturado em funções e procedimentos para manter a organização e facilitar a legibilidade.
- O desenvolvimento foi mais simples do que o esperado, permitindo a rápida implementação das funcionalidades básicas.

---

### Comunicação entre App e Hardware

- A comunicação entre o aplicativo Android e o ESP32 é realizada via Bluetooth Serial clássico.
- O app envia comandos simples:
  - `'1'` para abrir a porta;
  - `'2'` para fechar a porta.
- O ESP32 interpreta esses comandos e controla o servo motor, buzzer, LEDs e display LCD conforme o comando recebido.
- O protocolo de comunicação é simples e direto, sem mecanismos avançados de segurança ou controle de erros.
- Durante os testes, não foram observadas instabilidades na comunicação.
- O app utilizado para simulação foi desenvolvido no MIT App Inventor e é exclusivo para dispositivos Android.

---


