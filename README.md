# P.20.ino
motor con inversión de xiro en arduino
/*
Programa para simular unha ventá dun coche, de maneira
simplificada. O pulsador acciona o motor de subida ó ser premido. Unha
segunda pulsación acciona o motor de baixada. O percorrido do 
motor dura 7 segundos. Mentras os motores están accionados deben
responder ó accionamento do pulsador (responsive).

Entradas: Pulsador (dixital)
Saida: Relé (2x dixital)

Autor: Jéssica Suárez Parada
Data:06/02/2023
*/

#define motorArriba 12
#define motorAbaixo 11
#define pulsador 7

bool estado = 0;
int contador = 100; //Contador co numero de impulsos do motor

void setup(){
  pinMode(motorArriba, OUTPUT);
  pinMode(motorAbaixo,OUTPUT);
  pinMode(pulsador,INPUT);
  
  Serial.begin(9600);  //Velocidade de sincronismo das comunicacións
}

void loop() {
  //Lectura pulsador
  if(digitalRead(pulsador)) {
    estado = !estado;
    contador = 100;
    while(digitalRead(pulsador)) {
      delay(20);
    }
  }
  //Fin da lectura do pulsador
  
  Serial.println("Valor do contador: ");
  Serial.println(contador);
  Serial.print("  | Estado: ");
  Serial.print(estado);
  
  //Accionamento dos motores
  if(contador > 0){         //Conta o número de impulsos do motor
    if(estado == 0){
    digitalWrite(motorArriba, HIGH);
    digitalWrite(motorAbaixo, LOW);
    delay(70);
    contador--;
  }
  else{
    digitalWrite(motorArriba, LOW);
    digitalWrite(motorAbaixo, HIGH);
    delay(70);
    contador--;
  }
 }
  else{         //Se o motor non está accionado, espera 100 msg.
  }
     //Fin do accionamento de ambos motores
    //delay(80);
    if(contador == 0) {  //O contador está a 0 e apangase os motores
    digitalWrite(motorArriba, LOW);
    digitalWrite(motorAbaixo, LOW);
    delay(100);
  }
}
