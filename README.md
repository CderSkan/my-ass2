
#include <TFT.h>  // Arduino LCD library
#include <SPI.h>
#include <Keypad.h>

// pin definition for the Uno
#define cs   10
#define dc   9
#define rst  8
 int angle;
 int i=0;
 int j=0;
 String value;
// pin definition for the Leonardo
// #define cs   7
// #define dc   0
// #define rst  1
const byte ROWS = 4;
const byte COLS = 4;
char keys[ROWS][COLS] = {
  {'1','2','3','A'},
  {'4','5','6','B'},
  {'7','8','9','C'},
  {'*','0','#','D'}
};
byte rowPins[ROWS] = {7, 6, 5, 4};
byte colPins[COLS] = {3, 2, A3, A4};
Keypad keypad = Keypad(makeKeymap(keys), rowPins, colPins, ROWS, COLS);

// create an instance of the library
TFT TFTscreen = TFT(cs, dc, rst);

// char array to print to the screen
char sensorPrintout[4];

void setup() {
  // Put this line at the beginning of every sketch that uses the GLCD:
  TFTscreen.begin();
  TFTscreen.background(0, 0, 0);
  TFTscreen.stroke(255, 255, 255);
  TFTscreen.setTextSize(1);
  TFTscreen.text("Enter the angle\n ", 0, 0);
  TFTscreen.setTextSize(2);
}

void loop()
 {
  char key=keypad.getKey();
  String sensorVal=String(key);
  sensorVal.toCharArray(sensorPrintout, 4);
if(key){
if(key >='0' && key <='9')
{
Serial.println(key);  
   TFTscreen.text(sensorPrintout,i,20);
   i=i+20;
   TFTscreen.stroke(255, 255, 255);
  delay(250);
}
  else if (key =='A'){
      if (sensorVal.length() > 0)
      {
        value += sensorVal;
        angle=value.toInt();
      //servo.write(angle);
        j=j+1;
      }
  }
  else if (key =='B'){
    //for clear key
    i=0;
    front();

    }
    else if(key=='C')
    {
      //backspace

    }
    if(j==1)
    {
      duration();
    }
    
  }
 }
  void front()
  {
      TFTscreen.background(0, 0, 0);
      TFTscreen.stroke(255, 255, 255);
      TFTscreen.setTextSize(1); 
      TFTscreen.text("Enter the angle :\n ", 0, 0);
       TFTscreen.setTextSize(2);
  }

  void duration()
  {
   TFTscreen.begin();
  TFTscreen.background(0, 0, 0);
  TFTscreen.stroke(255, 255, 255);
  TFTscreen.setTextSize(1);
  TFTscreen.text("Enter the Duration:\n ", 0, 0);
  TFTscreen.setTextSize(2); 
  }


 

  


