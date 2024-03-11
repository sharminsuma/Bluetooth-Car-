// Bluetooth-Car-
//Two Wheel Bluetooth Car



#include "BluetoothSerial.h"
BluetoothSerial SerialBT;
int LED1 = 14, LED2 = 32, speed = 10;
int M1_front = 4, M1_back = 17, M1_pwm = 2;
int M2_front = 16, M2_back = 0, M2_pwm = 15;
int buttonState = 0;
int lastButtonState = 0;

void setup() {
  Serial.begin(9600);
  SerialBT.begin("Bluetooth RC Car");
  Serial.print("BT Started!");
  ledcSetup(0, 1000, 8);
  ledcAttachPin(M1_pwm, 0);
  ledcSetup(1, 1000, 8);
  ledcAttachPin(M2_pwm, 1);
  pinMode(LED1, OUTPUT);
  pinMode(LED2, OUTPUT);
  pinMode(M1_front, OUTPUT);
  pinMode(M1_back, OUTPUT);
  pinMode(M2_front, OUTPUT);
  pinMode(M2_back, OUTPUT);
}

void loop() {
  if (SerialBT.available()) {
    char x = SerialBT.read();
    Serial.print(x);
    if (x == 'F') motor(25 * speed, 25 * speed);
    else if (x == 'B') motor(-25 * speed, -25 * speed);
    else if (x == 'L') motor(-25 * speed, 25 * speed);
    else if (x == 'R') motor(25 * speed, -25 * speed);
    else if (x == 'G') motor(0, 25 * speed);
    else if (x == 'I') motor(25 * speed, 0);
    else if (x == 'H') motor(0, -25 * speed);
    else if (x == 'J') motor(-25 * speed, 0);
    else if (x == 'S') motor(0, 0);
    else if (x == 'W') {
      digitalWrite(LED1, 1);
      digitalWrite(LED2, 1);
    } else if (x == 'w') {
      digitalWrite(LED1, 0);
      digitalWrite(LED2, 0);
    } else if (x >= '0' && x <= '9') speed = x - '0';
    else if (x == 'q') speed = 10;
  }
}

void motor(int a, int b) {
  Serial.print("a = ");
  Serial.print(a);
  Serial.print(", b = ");
  Serial.println(b);
  if (a > 0) {
    digitalWrite(M2_front, 1);
    digitalWrite(M2_back, 0);
  } 
  
  else if (a = -a){
    digitalWrite(M2_front, 0);
    digitalWrite(M2_back, 1);
  }
  else {
    digitalWrite(M2_front, 0);
    digitalWrite(M2_back, 0);
  } 
  if (b > 0) {
    digitalWrite(M1_front, 1);
    digitalWrite(M1_back, 0);
  } 
  
  else if (b = -b){
    digitalWrite(M1_front, 0);
    digitalWrite(M1_back, 1);
  }
  ledcWrite(1, a);
  ledcWrite(0, b);
}

  


