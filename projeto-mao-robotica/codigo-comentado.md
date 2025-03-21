#include "Servo.h"  // Inclui a biblioteca para controle de servos

// Arrays para armazenar valores dos sensores, ângulos dos servos, pinos dos servos e pinos dos sensores
int Valor[5] = {0, 0, 0, 0, 0};
int Angulo[5] = {0, 0, 0, 0, 0};
int PinoServo[5] = {5, 6, 7, 8, 9};        // Pinos onde os servos estão conectados
int Pino_sensor[5] = {A0, A1, A2, A3, A4}; // Pinos analógicos onde os sensores estão conectados

Servo MeuServo[5]; // Cria um array de objetos Servo, um para cada dedo

void setup() {  
    Serial.begin(9600); // Inicializa a comunicação serial para monitoramento

    // Configura cada pino do sensor como entrada e conecta cada servo ao seu pino correspondente
    for (int i = 0; i < 5; i++) {
        pinMode(Pino_sensor[i], INPUT);     
        MeuServo[i].attach(PinoServo[i]);   
    }
}

void loop() {  
    for (int i = 0; i < 5; i++) {
        Valor[i] = analogRead(Pino_sensor[i]);         // Lê o valor analógico do sensor
        Angulo[i] = map(Valor[i], 0, 1023, 180, 0);    // Converte o valor lido para um ângulo (0 a 180 graus)
        Angulo[i] = constrain(Angulo[i], 0, 180);      // Garante que o valor do ângulo esteja no intervalo correto

        MeuServo[i].write(Angulo[i]);  // Move o servo para o ângulo calculado

        // Exibe os valores no monitor serial
        Serial.print("Dedo ");
        Serial.print(i + 1);
        Serial.print(" - Valor: ");
        Serial.print(Valor[i]);
        Serial.print(" - Angulo: ");
        Serial.println(Angulo[i]);
    }
    delay(1000); // Aguarda 1 segundo antes de repetir
}
