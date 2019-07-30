# Sensor de alarme
 Arduíno Uno

Este projeto de alarme é capaz de detectar movimentos em um ambiente disparando um sinal sonoro e acendendo um led. Pode ser usado por exemplo na porta de entrada da sua casa ou em algum cômodo e quando alguém passar por lá o alarme será disparado. Então se você necessita ser avisado da presença de alguém em um determinado lugar este projeto é uma opção interessante e fácil de fazer.

O sensor PIR é fácil de se encontrar, a maioria das lojas virtuais e físicas que vendem Arduinos e/ou componentes eletrônicos normalmente possuem este sensor. Só verifique se o sensor PIR que você pretende adquirir possui controle de sensibilidade da detecção de movimentos. Este que usei no projeto do alarme possui três pinos, controle de sensibilidade e controle de tempo que o sensor fica "ligado" quando detecta algum movimento.

Para desenvolver o projeto Alarme com Arduino e sensor de movimentos PIR você vai precisar de:

Arduino;
Sensor de movimentos/presença PIR;
Led;
Buzzer de 5 volts;
2 resistores de 220 ohms;
Protoboard;
Bateria de 9 volts;
Suporte para bateria com plug para ligar no Arduino;
Fios para interligar os componentes.


#Créditos
www.comofazerascoisas.com.br

Através deste esquema fica mais fácil de se ter uma visão geral, e de como montar corretamente o projeto.
Este esquema foi montado no software Fritzing.

<img src="https://github.com/ulissesbmatosc/Trabalho-Arduino--Sensor-de-alarme/blob/master/projeto-arduino-alarme.jpg">


Código Fonte

//Declaração das variáveis referentes aos pinos digitais.
int pinBuzzer = 7;
int pinSensorPIR = 8;
int pinLed = 9;
int valorSensorPIR = 0;
 
void setup() {
  Serial.begin(9600); //Inicializando o serial monitor
 
  //Definido pinos como de entrada ou de saída
  pinMode(pinBuzzer,OUTPUT);
  pinMode(pinSensorPIR,INPUT);
  pinMode(pinLed,OUTPUT);
}
 
void loop() {  
  //Lendo o valor do sensor PIR. Este sensor pode assumir 2 valores
  //1 quando detecta algum movimento e 0 quando não detecta.
  valorSensorPIR = digitalRead(pinSensorPIR);
   
  Serial.print("Valor do Sensor PIR: ");  
  Serial.println(valorSensorPIR);
   
  //Verificando se ocorreu detecção de movimentos
  if (valorSensorPIR == 1) {
    ligarAlarme();
  } else {
    desligarAlarme();
  }    
}
 
void ligarAlarme() {
  //Ligando o led
  digitalWrite(pinLed, HIGH);
   
  //Ligando o buzzer com uma frequencia de 1500 hz.
  tone(pinBuzzer,1500);
   
  delay(4000); //tempo que o led fica acesso e o buzzer toca
   
  desligarAlarme();
}
 
void desligarAlarme() {
  //Desligando o led
  digitalWrite(pinLed, LOW);
   
  //Desligando o buzzer
  noTone(pinBuzzer);
}
