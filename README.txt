WIRELESS NOTICE BOARD USING BLUETOOTH MODULE.


OBJECTIVE:
The main objective of this project is to develop a wireless notice board that 
displays messages send from the user’s mobile.
The message received by the module is sent to the microcontroller that 
further displays it on a electronic notice board.



CIRCUIT CONNECTION EXPLANATION:

In the LCD from the 16th pin which is k to D4 is connected to the analog side of the arduino board from A0 to A5.
In the LCD the VDD pin is connected to 5V pin in arduino board.
The V0 is given to ground in arduino board.
The RS and RW pins are connected to the 5th and 4th pin of the arduino respectively and the E pin is given to the number 3 of arduino.
BLUETOOTH MODULE TO ARDUINO:  
The Vcc pin in the bluetooth module is connected to the 3.3V pin of arduino.
GND of the bluetooth is given to the GND of arduino.
Tx of the bluetooth is given to the Rx of the arduino.
Rx of the bluetooth is given to the Tx of the arduino.
Arduino Bluetooth Control Application has to be downloaded to connect with the bluetooth module.
After pairing the HC-05 bluetooth module to the user's phone, the message can be sent from the user mobile and then it will be received by the module
and it will be displayed in the LCD.




CODE EXPLANATION:

#include <LiquidCrystal.h>  // import the LCD Header File

char str[34],L=2;
int temp=0,i=0;
int Pass=0,p=0;
 int c,x,d;       // Initial declaration
const int rs = 5, en = 3, d4 = A5, d5 = A4, d6 = A3, d7 = A2;
LiquidCrystal lcd(rs, en, d4, d5, d6, d7);   // creation of LCD Object and Pass pin number of Arduino to LCD

void setup()
{
 Serial.begin(9600);     // Start the Serial Communication with the baud rate of 9600
  pinMode(A1,OUTPUT);     // set the pin A1 to output Mode
   
  digitalWrite(A1,LOW);    // set the pin A1 to low initially
  
  lcd.begin(16, 2);    // Iniatilize 2 rows and 16 Columns of lcd
  
 
}

void loop() 
{ 
  if(temp==1)
  {
    check();
     temp=0;
    i=0;
    delay(1000);
  }
  
}

void serialEvent() 
 {
      while (Serial.available()) 
      {
      char inChar=Serial.read();   // Read the string character by character
      str[i++]=inChar;     // store it in str
      delay(10);
      }
      
    temp=1;
   loop();
  Serial.write(str);
  lcd.setCursor(0, 0);  // Set the cursor to top left position
 lcd.print(str);   // print the string
  if(i>16)          //  if more than 16 characters then print in  2nd row
  {
    d=16;
    for (x=0;x<=17;x++)
    {
    lcd.setCursor(x,2);
    lcd.print(str[d]);  // print the string in LCD
    d++;
    }
  }
 }

void check()
{
if(!(strncmp(str,"1",1)))    // if enterd string is 1 ,then only LCD will ON 
  {
   digitalWrite(A1,50);     // set A1 pin to HIGH in order to ON LCD 
   lcd.clear(); 
  }  else if(!(strncmp(str,"2",1)))      // if enterd string is 2,then LCD will OFF 
  {
   digitalWrite(A1,LOW);  // set A1 pin to LOW in order to OFF LCD
   lcd.clear(); 
  }
}