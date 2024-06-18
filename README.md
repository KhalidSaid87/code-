# code-
for the project
#include <Servo.h>

const int trigPin = 2;
const int echoPin = 3;

float duration, distance;

#define PIN_RELAY_1  4 
#define PIN_RELAY_2  5 
#define PIN_RELAY_3  6
#define PIN_RELAY_4  7

int servoPin1 = 8; 
int servoPin2 = 9;
const int camera = 10;
const int warning = 11;
// Create a servo object 
Servo Servo1; 
Servo Servo2;

void setup() {
  Servo1.attach(servoPin1);
  Servo2.attach(servoPin2); 

  pinMode(PIN_RELAY_1, OUTPUT);
  pinMode(PIN_RELAY_2, OUTPUT);
  pinMode(PIN_RELAY_3, OUTPUT);
  pinMode(PIN_RELAY_4, OUTPUT);
  pinMode(camera, OUTPUT);
  pinMode(warning, OUTPUT);
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);
  Serial.begin(9600);
}

void loop() {
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);

  duration = pulseIn(echoPin, HIGH);
  distance = (duration*.0343)/2;
  Serial.print("Distance: ");
  Serial.println(distance);
  delay(100);

  if(distance <=200 && distance >=150){
    digitalWrite(PIN_RELAY_1, HIGH);
    digitalWrite(camera, HIGH);
  }

  else if(distance <=149 && distance >= 100){
    digitalWrite(warning, LOW);

  }

  else if(distance <=99 && distance >=50){
    digitalWrite(PIN_RELAY_2, HIGH);

  }

  else if(distance <49){
    Servo1.write(90);
    Servo2.write(90);

    digitalWrite(PIN_RELAY_3, HIGH);
    digitalWrite(PIN_RELAY_4, HIGH);

  }

  else{
    digitalWrite(PIN_RELAY_1, LOW);
    digitalWrite(PIN_RELAY_2, LOW);
    digitalWrite(PIN_RELAY_3, LOW);
    digitalWrite(PIN_RELAY_4, LOW);
    digitalWrite(warning, HIGH);
    digitalWrite(camera, LOW);

    Servo1.write(0);
    Servo2.write(0);
  }
}
