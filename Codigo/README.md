// Desenvolvedor: Gabriel Campos Amaral Ribeiro

// ==============================================
// IMPORTANTE PARA FUNCIONAMENTO CORRETO:
// 1. Selecione a placa "ESP32 Dev Module" na IDE do Arduino.
// 2. Instale as bibliotecas:
//    - ESP32Servo (por Kevin Harrington) -> para controlar servo motor
//    - MFRC522 (por Miguel Balboa ou similar) -> para leitor RFID
//    - LiquidCrystal_I2C (por Frank de Brabander ou compatível) -> para display LCD via I2C
// ==============================================

#include <SPI.h>               // Comunicação SPI (usada para se comunicar com o leitor RFID)
#include <MFRC522.h>           // Biblioteca para controlar o módulo RFID MFRC522
#include <ESP32Servo.h>        // Biblioteca feita especialmente para controlar servo motor com ESP32
#include <Wire.h>              // Comunicação I2C (necessária para o display LCD funcionar)
#include <LiquidCrystal_I2C.h> // Biblioteca que permite usar o display LCD 16x2 via comunicação I2C
#include <BluetoothSerial.h>   // Biblioteca Bluetooth Serial ESP32

LiquidCrystal_I2C lcd(0x27, 16, 2); // Cria o objeto LCD, com o endereço I2C (geralmente é 0x27) e tamanho 16 colunas x 2 linhas

#define SS_PIN 5               // Pino SDA do RFID conectado ao GPIO 5 - RFID
#define RST_PIN 22             // Pino RST do RFID conectado ao GPIO 22 - RFID
MFRC522 rfid(SS_PIN, RST_PIN); // Cria o objeto do RFID passando os pinos definidos - RFID

Servo servo; // Cria o objeto do servo motor
BluetoothSerial SerialBT; // Cria objeto Bluetooth Serial


// ====== DEFINIÇÃO DOS PINOS ======
const int buzzerPin = 13;      // Pino para buzzer (gera som)
const int servoPin = 14;       // Pino do servo motor
const int botaoPin = 15;       // Botão de saída (aciona a porta)
const int ledGreenPin = 25;    // LED verde (porta aberta)
const int ledRedPin = 26;      // LED vermelho (porta fechada)
const int toquePin = 32;       // Sensor de toque capacitivo


// ====== VARIÁVEIS ======
int contadorToques = 0;         
int tempoFechaPorta = 3000;      


// ====== UIDs AUTORIZADOS ======
byte uid1[] = {0x33, 0xE6, 0x76, 0x1A};  // Cartão branco
byte uid2[] = {0xD3, 0xD4, 0xBA, 0x0E};  // Chaveiro azul
byte uid3[] = {0x34, 0x3F, 0xF8, 0xA5};  // Cartão do ônibus


// ====== FUNÇÃO PARA COMPARAR O UID LIDO COM OS AUTORIZADOS ======
bool compararUID(byte *uidLido, byte *uidEsperado, byte tamanho) {
  for (byte i = 0; i < tamanho; i++) {
    if (uidLido[i] != uidEsperado[i]) {
      return false;             // UID diferente
    }
  }
  return true;                  // UID igual, autorizado
}


// ====== FUNÇÃO PARA ABRIR A PORTA ======
void abrirPorta() {
  mostrarMensagemLCD("ACESSO PERMITIDO", "PORTA ABERTA!");
  servo.write(30);              
  digitalWrite(ledRedPin, LOW); 
  digitalWrite(ledGreenPin, HIGH); 
  buzinar();                  
}


// ====== FUNÇÃO PARA FECHAR A PORTA ======
void fecharPorta() {
  // Contagem regressiva para fechamento
  for(int i = 3; i > 0; i--){
    String linha2 = "EM: " + String(i) + "!";
    mostrarMensagemLCD("PORTAS FECHANDO", linha2.c_str());
    avisar_fechamentoPorta();  // Pisca LED e buzina para avisar
    delay(1000);
  }
  servo.write(120);             
  digitalWrite(ledRedPin, HIGH); 
  digitalWrite(ledGreenPin, LOW); 
  mostrarMensagemLCD("APROXIME SEU", "CARTAO/CHAVEIRO");
}


// ====== FUNÇÃO PARA FAZER UM BEEP CURTO COM O BUZZER ======
void buzinar() {
  digitalWrite(buzzerPin, HIGH);
  delay(200);
  digitalWrite(buzzerPin, LOW);
}


// ====== AVISO DE FECHAMENTO COM LED E BUZZER ======
void avisar_fechamentoPorta(){
  for (int i = 0; i < 2; i++) {
    digitalWrite(ledGreenPin, LOW);  
    digitalWrite(ledRedPin, HIGH);  
    digitalWrite(buzzerPin, HIGH);   
    delay(100);
    digitalWrite(ledRedPin, LOW);    
    digitalWrite(buzzerPin, LOW);    
    delay(100);
  }
}


// ====== ALERTA DE ACESSO NEGADO (3 beeps) ======
void buzinar_erro() {
  for (int i = 0; i < 3; i++) {
    digitalWrite(buzzerPin, HIGH);
    delay(300);
    digitalWrite(buzzerPin, LOW);
    delay(200);
  }
}


// ====== SENSOR DE TOQUE PARA ABRIR A PORTA (APÓS 3 TOQUES) ======
void sensorToque() {
  if (digitalRead(toquePin) == HIGH) {
    contadorToques++;           

    if (contadorToques >= 3) {   // Após 3 toques consecutivos
      abrirPorta();
      mostrarMensagemLCD("ACESSO PERMITIDO", "PORTA ABERTA!");
      delay(tempoFechaPorta);
      fecharPorta();
      mostrarMensagemLCD("APROXIME SEU", "CARTAO/CHAVEIRO");
      contadorToques = 0;        
    }

    // Espera o dedo sair do sensor e evita toques acidentais
    while (digitalRead(toquePin) == HIGH);
    delay(1500);  
  }
}


// ====== MOSTRA MENSAGEM NO DISPLAY LCD ======
void mostrarMensagemLCD(const char* msg1, const char* msg2) {
  lcd.clear();               // Limpa o display
  lcd.setCursor(0, 0);       
  lcd.print(msg1);           
  lcd.setCursor(0, 1);      
  lcd.print(msg2);           
}


// ====== CONFIGURAÇÕES INICIAIS ======
void setup() {
  Serial.begin(115200); //Velocidade da comunicação serial

  //Bluetooth =========
  SerialBT.begin("SMART_DOOR"); // Inicia Bluetooth com o nome do dispositivo
  delay(1000);
  SerialBT.println("Bluetooth iniciado!");  // Mensagem inicial no BT

  pinMode(botaoPin, INPUT_PULLUP);  // Configura botão de saida

  // Inicialização do display I2C nos pinos GPIO 33 (SDA) e 27 (SCL)
  Wire.begin(33, 27);
  lcd.init();  // Inicializa o display LCD
  lcd.backlight(); // Liga a luz de fundo do LCD

  // Inicializa o leitor RFID com pinos padrão SPI para o ESP32 (SCK=18, MISO=19, MOSI=23, SS=5)
  SPI.begin(18, 19, 23, 5); 
  rfid.PCD_Init();// Inicializa o módulo RFID

  servo.attach(servoPin); // Define o pino do servo

  // Define os pinos de entrada e saída
  pinMode(toquePin, INPUT);       
  pinMode(buzzerPin, OUTPUT);     
  pinMode(ledRedPin, OUTPUT);    
  pinMode(ledGreenPin, OUTPUT);  

  // Estado inicial da porta
  servo.write(120);  // Posiciona servo para porta fechada
  digitalWrite(ledRedPin, HIGH);
  digitalWrite(ledGreenPin, LOW);
  mostrarMensagemLCD("APROXIME SEU", "CARTAO/CHAVEIRO");
}


// ====== LOOP PRINCIPAL ======
void loop() {

  //Comunicacao via Bluetooth
  if (SerialBT.available()) {  // Verifica se há algum dado recebido via Bluetooth
    char cmd = SerialBT.read(); // Lê o caractere recebido (ex: '1', '2')

    if (cmd == '1') {
      Serial.println("Portas abrindo!");
      abrirPorta();
    }else if (cmd == '2') {
      Serial.println("Portas fechando!");
      fecharPorta();
    }else{
      Serial.println("Comando não reconhecido");
    }
  }

  // Verifica se há cartão RFID presente e tenta ler o UID
  if (rfid.PICC_IsNewCardPresent() && rfid.PICC_ReadCardSerial()) {
    // Compara o UID do cartão lido com os autorizados
    if (compararUID(rfid.uid.uidByte, uid1, 4) || compararUID(rfid.uid.uidByte, uid2, 4) || compararUID(rfid.uid.uidByte, uid3, 4)) {
      Serial.println("Cartão autorizado! Acesso liberado.\n");
      abrirPorta();              
      delay(tempoFechaPorta);               
      fecharPorta();              

    } else {
      Serial.println("Cartão não autorizado!\n");
      buzinar_erro();            
      mostrarMensagemLCD(" ACESSO NEGADO!", " ");
      delay(2000);
    }

    rfid.PICC_HaltA(); // Para comunicação com cartão atual
    delay(2000);
    mostrarMensagemLCD("APROXIME SEU", "CARTAO/CHAVEIRO");
  }

  // Verifica se o sensor de toque foi ativado (sensor capacitivo)
  if (digitalRead(toquePin) == HIGH){
    sensorToque();
  }

  // Verifica se o botão físico foi pressionado (botão de saída)
  if (digitalRead(botaoPin) == LOW) {
    abrirPorta();
    delay(tempoFechaPorta);
    fecharPorta();
  }

}
