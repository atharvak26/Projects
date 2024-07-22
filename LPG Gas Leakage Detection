#include<Servo.h>
#include <SoftwareSerial.h>

SoftwareSerial GSM(11, 10);
Servo s1;

int led = 6;
int led1 = 5;
int sw = 2;

char phone_no[] = "+919307525564";

void setup() {
  s1.attach(8);
  s1.write(0);
  pinMode(5, OUTPUT);
  pinMode(6, OUTPUT);
  pinMode(sw, INPUT);


  Serial.begin(9600); 
  // Setting the baud rate of Sim Module
  GSM.begin(9600);
  // Setting the baud rate of Serial Monitor (Arduino) 
  Serial.println("Ready");
  //pinMode(led1, HIGH);

  Serial.println("Initialising...");
  initModule("AT", "OK", 1000);
  //put your setup code here, to run once:

}

void loop() {

  if(digitalRead(sw) == LOW)
  {
      s1.write(140);
      digitalWrite(led1, HIGH);
      digitalWrite(led, HIGH);

      
      callUp(phone_no);
      SendMessage();
      callUp(phone_no);
      SendMessage();
  }
}

void initModule(String cmd, char *res, int t) {
  while (1) {
    Serial.println(cmd);
    GSM.println(cmd);
    delay(100);
    while (GSM.available() > 0) {
      if (GSM.find(res)) {
        Serial.println(res);
        delay(t);
        return;
      } else {
        Serial.println("Error");
      }
    }
    delay(t);
  }
}

void SendMessage()
{
  GSM.println("AT+CMGF=1");

  delay(1000);
  GSM.println("AT+CMGS=\"9307525564\"\r"); //

  delay(1000);
  GSM.println("Alert! Gas Leak Detected ");

  delay(100);
  Serial.println("Msg Sent");
  GSM.println((char)26);
  delay(1000);
}

void callUp(char *number)
{
  GSM.print("ATD + "); 
  GSM.print(number);
  GSM.println(";");
  
  delay(10000);
  GSM.println("ATH");
  delay(100);
  Serial.println("Called");
}
