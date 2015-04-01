
#include <SPI.h>
#include <boards.h>
#include <RBL_nRF8001.h>
#include <RBL_services.h> 




//--ACTORS------------------------------ 
const int bluetooth1 = 23;
const int actor2 = 22;
const int inverter3 = 25;
const int horn4 = 24;
const int sound5 = 27;
const int pump6 = 26;
const int motorvent7 = 29;
const int motorstop8 = 28;
const int lbett9 = 31;
const int lmitte10 = 30;
const int lbank11 = 33;
const int ltop12 = 32;
const int usbpower13 = 35;
const int lwerfer14 = 34;
const int ldeck15 = 37;
const int actor16 = 36;

//--SENSORS------------------------------

const int waterstate3 = 3; 
const int temp4 = 4;
const int oil5 = 5;
 

char button1Mem = 'a';
char button2Mem = 'b';
char button3Mem = 'c';
char button4Mem = 'd';
char button5Mem = 'e';
char button7Mem = 'g';
char alarm = 'x';

unsigned long previousMillis = 0; 

void setup()
{ 

  ble_begin();

  Serial1.begin(9600);
  /*
digitalWrite(bluetooth1,LOW);
   digitalWrite(actor2,LOW);
   digitalWrite(inverter3,LOW)
   digitalWrite(horn4,LOW);
   digitalWrite(sound5,LOW);
   digitalWrite(actor6,LOW);
   digitalWrite(motorvent7,LOW);
   digitalWrite(motorstop8,LOW);
   digitalWrite(lbett9,LOW);
   digitalWrite(lmitte10,LOW);
   digitalWrite(lbank11,LOW);
   digitalWrite(ltop12,LOW);
   digitalWrite(usbpower13,LOW);
   digitalWrite(lwerfer14,LOW);
   digitalWrite(ldeck15,LOW);
   digitalWrite(actor16,LOW);
   
   */
 
 
  pinMode(bluetooth1, OUTPUT);
  pinMode(actor2, OUTPUT);
  pinMode(inverter3, OUTPUT);
  pinMode(horn4, OUTPUT);
  pinMode(sound5, OUTPUT);
  pinMode(pump6, OUTPUT);
  pinMode(motorvent7, OUTPUT);
  pinMode(motorstop8, OUTPUT);
  pinMode(lbett9, OUTPUT);
  pinMode(lmitte10, OUTPUT);
  pinMode(lbank11, OUTPUT);  
  pinMode(ltop12, OUTPUT);  
  pinMode(usbpower13, OUTPUT); 
  pinMode(lwerfer14, OUTPUT); 
  pinMode(ldeck15, OUTPUT);  
  pinMode(actor16, OUTPUT);  

  pinMode(waterstate3, INPUT_PULLUP);
  pinMode(temp4, INPUT_PULLUP);
  pinMode(oil5, INPUT_PULLUP);

  digitalWrite(bluetooth1,HIGH);
  digitalWrite(actor2,HIGH);
  digitalWrite(inverter3,HIGH);
  digitalWrite(horn4,HIGH);
  digitalWrite(sound5,HIGH);
  digitalWrite(pump6,HIGH);
  digitalWrite(motorvent7,HIGH);
  digitalWrite(motorstop8,HIGH);
  digitalWrite(lbett9,HIGH);
  digitalWrite(lmitte10,HIGH);
  digitalWrite(lbank11,HIGH);
  digitalWrite(ltop12,HIGH);
  digitalWrite(usbpower13,HIGH);
  digitalWrite(lwerfer14,HIGH);
  digitalWrite(ldeck15,HIGH);
  digitalWrite(actor16,HIGH);
}

unsigned char buf[16] = {0};
unsigned char len = 0;

void loop()
{  


  if(Serial1.available() > 0); {
    

    
    char letter = Serial1.read();
    if (ble_available())
{
letter = ble_read();
}
    

    //BUTTON1--------------------------------------------------    
    if(letter == '1')
    {
      if(button1Mem  == 'a')
      {
        
        digitalWrite(inverter3,LOW);
        digitalWrite(usbpower13,LOW);   
        
        
        button1Mem  = '1';
        Serial1.println(button1Mem);
        Serial1.println(button2Mem);
        Serial1.println(button3Mem);
        Serial1.println(button4Mem);
        Serial1.println(button5Mem);
            ble_write('R');
            ble_write('E');
            ble_write('A');
            ble_write('D');
            ble_write('Y');
            ble_write('!');

      } 
      else
      {
        digitalWrite(lbett9, HIGH);  
        button1Mem  = 'a';
        Serial1.println(button1Mem);
            ble_write('S');
            ble_write('t');
            ble_write('a');
            ble_write('n');
            ble_write('d');
            ble_write('b');
            ble_write('y');
            ble_write(' ');
            ble_write('M');
            ble_write('o');
            ble_write('d');
            ble_write('e');
      

      }
    }

    //BUTTON2 MOTOR--------------------------------------------------    


    if(letter == '2')
    {
      if(button2Mem  == 'b'){
        digitalWrite(motorvent7, LOW);
        button2Mem = '2'; 
        Serial1.println(button2Mem); 
         

      }
      else if (button2Mem =='2'){
         digitalWrite(motorstop8, LOW);
        button2Mem = '7';
        previousMillis = millis();
      }

    }   
    if(button2Mem =='7'){
      Serial1.println('b');
      delay(100);
      Serial1.println('2');
      delay(100);
      if ((millis() - previousMillis) >= 2000) {  
        digitalWrite(motorvent7, HIGH);
        digitalWrite(motorstop8, HIGH);
        button2Mem = 'b';
        Serial1.println(button2Mem);
      }
    }



    //BUTTON3 LIGHT--------------------------------------------------    
    if(letter == '3')
    {
      if(button3Mem  == 'c')
      {
       digitalWrite(lbett9,LOW);   
        button3Mem  = '8'; 
        Serial1.println('3');        
      } 
      else if(button3Mem == '8'){
        digitalWrite(lmitte10,LOW);
        digitalWrite(lbank11,LOW);
        button3Mem  = '9';
        Serial1.println('3');  
      }
        else if(button3Mem == '9'){
        digitalWrite(lmitte10,LOW);
        digitalWrite(lbank11,LOW);
        digitalWrite(lbett9,HIGH);
        button3Mem  = '3';
        Serial1.println('3');  
      }
      else if(button3Mem == '3'){
         digitalWrite(lbett9, HIGH);
         digitalWrite(lmitte10,HIGH);
         digitalWrite(lbank11,HIGH);
         button3Mem  = 'c';
         Serial1.println(button3Mem); 
      
      }
    }

   
    //BUTTON4 TOPLIGHT--------------------------------------------------    
    if(letter == '4')
    {
      if(button4Mem  == 'd')
      {
        digitalWrite(ltop12,LOW);
        button4Mem  = '4'; 
        Serial1.println(button4Mem);

      } 
      else
      {
        digitalWrite(ltop12,HIGH);
        button4Mem  = 'd';
        Serial1.println(button4Mem);
      }
    }

   
    // HORN--------------------------------------------------    
    if(letter == '6')
    {
      digitalWrite(horn4,LOW);
      delay(200);
    } 
     else
    {
        digitalWrite(horn4,HIGH);
    }

   
    //BUTTON5 SOUND------------------------------------------------    
    if(letter == '5')
    {
      if(button5Mem  == 'e') {
        digitalWrite(sound5, LOW);
        digitalWrite(bluetooth1,LOW);     
        button5Mem  = '5';  
        Serial1.println(button5Mem);
      } 
      else {
        digitalWrite(sound5, HIGH);
        digitalWrite(bluetooth1,HIGH);
        button5Mem  = 'e';
        Serial1.println(button5Mem);
      }
    }
    

 
 
    //TEMP ALARM------------------------------------------------    
   

      if(digitalRead(temp4) == LOW){
        delay(200);
         if(digitalRead(temp4) == LOW){
        digitalWrite(motorstop8, LOW);
        if(alarm != 't')
        {
         alarm = 't';
         Serial1.println('t');
         ble_write('A');
         ble_write('L');
         ble_write('A');
         ble_write('R');
         ble_write('M');
         ble_write(' ');
         ble_write('T');
         ble_write('E');
         ble_write('M');
         ble_write('P');
         ble_write('!'); 
         delay(10);
        }
       }  
  }
       else
       {
        if(alarm == 't') 
        {
        alarm = 'x';
        Serial1.println('z');
        digitalWrite(motorstop8, HIGH);
         ble_write('R');
         ble_write('E');
         ble_write('A');
         ble_write('D');
         ble_write('Y');
         ble_write('!');
        }
       }
      
   //OIL ALARM------------------------------------------------ 
     
      if(digitalRead(oil5) == LOW){
       delay(200);
       if(digitalRead(oil5) == LOW){
       digitalWrite(motorstop8, LOW);
        if(alarm != 'o')
        {
         alarm ='o';
         Serial1.println('o');
         ble_write('A');
         ble_write('L');
         ble_write('A');
         ble_write('R');
         ble_write('M');
         ble_write(' ');
         ble_write('O');
         ble_write('I');
         ble_write('L');
         ble_write('!'); 
         delay(10);
        }
      }
      }
        else
        {
        if(alarm == 'o') 
        {
        alarm = 'x';
        Serial1.println('z');
        digitalWrite(motorstop8, HIGH);
         ble_write('R');
         ble_write('E');
         ble_write('A');
         ble_write('D');
         ble_write('Y');
         ble_write('!');
        }
       }
        
     
   //PUMP----------------------------------------------------------
   
   
   if(digitalRead(waterstate3) == LOW){
        delay(100);
        digitalWrite(pump6, LOW);
        if(alarm != 'p')
        {
         alarm = 'p';
         Serial1.println('p');
         ble_write('P');
         ble_write('U');
         ble_write('M');
         ble_write('P');
         ble_write('!'); 
         delay(10);
        }
       }  
       else
        {
        delay(10);
        if(alarm == 'p') 
        {
        alarm = 'x';
        Serial1.println('z');
        digitalWrite(pump6, HIGH);
         ble_write('R');
         ble_write('E');
         ble_write('A');
         ble_write('D');
         ble_write('Y');
         ble_write('!');
        }
       
       }

//PUMP---------------------

    if(letter == '7')
    {
      if(button7Mem  == 'g') {
        digitalWrite(pump6, LOW);     
        button7Mem  = '7';  
         ble_write('P');
         ble_write('U');
         ble_write('M');
         ble_write('P');
         ble_write(' ');
         ble_write('O');
         ble_write('N');
      } 
      else {
        digitalWrite(pump6, HIGH);
        button7Mem  = 'g';
          ble_write('P');
         ble_write('U');
         ble_write('M');
         ble_write('P');
         ble_write(' ');
         ble_write('O');
         ble_write('F');
         ble_write('F');
      }
    }
    



    //ALL OFF-------------------------------------------------------
    if(letter == 'x')
    {
      digitalWrite(bluetooth1,HIGH);
      digitalWrite(actor2,HIGH);
      digitalWrite(inverter3,HIGH);
      digitalWrite(horn4,HIGH);
      digitalWrite(sound5,HIGH);
      digitalWrite(pump6,HIGH);
      digitalWrite(motorvent7,HIGH);
      
      digitalWrite(lbett9,HIGH);
      digitalWrite(lmitte10,HIGH);
      digitalWrite(lbank11,HIGH);
      digitalWrite(ltop12,HIGH);
      digitalWrite(usbpower13,HIGH);
      digitalWrite(lwerfer14,HIGH);
      digitalWrite(ldeck15,HIGH);
      digitalWrite(actor16,HIGH);
      
      if(button2Mem == '2'){
      previousMillis = millis();
      digitalWrite(motorstop8, LOW);
      button2Mem = '7';
      }
      button3Mem = 'c';
      button4Mem = 'd';
      button5Mem = 'e';
      Serial1.println(button2Mem);
      Serial1.println(button3Mem);
      Serial1.println(button4Mem);
      Serial1.println(button5Mem);
      //Serial1.println(alarm);


    }  

  }
  
   ble_do_events();
}
