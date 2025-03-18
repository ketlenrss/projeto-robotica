#include <Servo.h>  // Inclui a biblioteca Servo.h

Servo meuServo;  // Cria um objeto Servo

int pinoPot = A2;  // Define o pino do potenciômetro

void setup() {
  meuServo.attach(2);  // Define o pino do servo
  pinMode(pinoPot, INPUT);  // Define o pino do potenciômetro como entrada
}

void loop() {
  int leituraPot = analogRead(pinoPot);  // Lê o valor do potenciômetro
  int anguloServo = map(leituraPot, 0, 1023, 0, 180);  // Converte o valor para ângulo (0 a 180)
  meuServo.write(anguloServo);  // Move o servo para o ângulo correspondente
  delay(15);  // Pequeno atraso para suavizar o movimento
}
