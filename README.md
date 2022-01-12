# fan
opensw project
/*#include "DHT.h"  //DHT 라이브러리
 
#define DHTPIN 2        // SDA 핀의 설정
#define DHTTYPE DHT11   // DHT22 센서종류 설정
int relay = 10;         //릴레이단자
 
DHT dht(DHTPIN, DHTTYPE);
 
void setup() {
  Serial.begin(9600); 
  Serial.println("DHT11 RELAY FAN !!!");
  dht.begin();
  pinMode (relay, OUTPUT); 
}
 
void loop() {
  float temp = dht.readTemperature();
 
  if (isnan(temp)) {
    //값 읽기 실패시 시리얼 모니터 출력
    Serial.println("Failed to read from DHT");
  } else {
    Serial.print("Temp: "); 
    Serial.print(temp);
    Serial.println(" *C");
    
    if(temp>=30) //30도 이상이면 선풍기 ON
    {
      digitalWrite (relay, HIGH);
    } else {
      digitalWrite (relay, LOW);
    }
  }
//delay(2000);*/

from flask import Flask, request
from flask import render_template
import RPi.GPIO as GPIO
import time
import Adafruit_DHT
import I2C_LCD_driver
import pymysql

for pin in control_pins:
    GPIO.setup(pin,GPIO.OUT)
    GPIO.output(pin,False)
stepcounter = 0
stepcount=4
seq=[[0,0,0,1],
     [0,0,1,0],
     [0,1,0,0],
     [1,0,0,0]] //서브모터 돌아가는 코드
