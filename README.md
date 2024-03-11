// Bluetooth-Car-
//Two Wheel Bluetooth Car



#include "BluetoothSerial.h"
BluetoothSerial SerialBT;
int LED1 = 14, LED2 = 32;
int M1_front = 17, M1_back = 4, M1_pwm = 2;
int M2_front = 16, M2_back = 0, M2_pwm = 15;


int command; //Int to store app command state.
int speedCar = 255; // Initial car speed set 0 to 255.



void setup(){
 Serial.begin(9600);
 SerialBT.begin("Bluetooth RC Car"); Serial.print("BT Started!");
 ledcSetup(0,1000,8); ledcAttachPin(M1_pwm,0);
 ledcSetup(1,1000,8); ledcAttachPin(M2_pwm,1);
 pinMode(LED1, OUTPUT); pinMode(LED2, OUTPUT);
 pinMode(M1_front, OUTPUT); pinMode(M1_back, OUTPUT);
 pinMode(M2_front, OUTPUT); pinMode(M2_back, OUTPUT);
 Stop();
}



void forward()
{
  digitalWrite(17,HIGH);
  digitalWrite(16,HIGH);
}

void backward()
{
  digitalWrite(4,HIGH);
  digitalWrite(0,HIGH);
}
void left()
{
  digitalWrite(4,HIGH);
}
void right()
{
  digitalWrite(17,HIGH);
}

void ledon()
{
  digitalWrite(14,HIGH);
  digitalWrite(32,HIGH);
}

void ledoff()
{
  digitalWrite(14,LOW);
  digitalWrite(32,LOW);
}


void Stop()
{
  digitalWrite(17,LOW);
  digitalWrite(16,LOW);
  digitalWrite(4,LOW);
  digitalWrite(0,LOW);
}

void loop(){
  
if (Serial.available() > 0) {
  command = Serial.read();
  Stop();       //Initialize with motors stopped.

if (ledon) {digitalWrite(LED1, HIGH); digitalWrite(LED2, HIGH);}
if (ledoff) {digitalWrite(LED1, LOW); digitalWrite(LED2, LOW);}


switch (command) {
case 'F':forward();break;
case 'B':backward();break;
case 'L':left();break;
case 'R':right();break;
case 'S':Stop();break;
case '0':speedCar = 0;break;
case '1':speedCar = 25;break;
case '2':speedCar = 50;break;
case '3':speedCar = 75;break;
case '4':speedCar = 100;break;
case '5':speedCar = 125;break;
case '6':speedCar = 150;break;
case '7':speedCar = 175;break;
case '8':speedCar = 200;break;
case '9':speedCar = 225;break;
case 'q':speedCar = 255;break;
case 'W':ledon();break;
case 'w':ledoff();break;
}}}




