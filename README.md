hackathon
=========
#include <TinkerKit.h>

// creating the object 'pot' that belongs to the 'TKPotentiometer' class
TKPotentiometer pot(I0);
// creating the object 'led' that belongs to the 'TKLed' class 
TKLed led(11);  
TKThermistor therm(I2);
// creating the object 'pot' that belongs to the 'TKPotentiometer' class
TKPotentiometer pot2(I1);




int brightnessVal = 0;  // value read from the pot
int led_close_left = 10;           // the pin that the LED is attached to
int led_close_right = 9;  

int brightness = 0;    // how bright the LED is
float C;
float Steering_Angle = 0;



void setup() {
  // initialize serial communications at 9600 bps
  Serial.begin(9600);
//  pinMode(led, OUTPUT);
}




void loop() {
  // read the potentiometer's value:
  brightnessVal = pot.read();       
  //read temperature in celsius and storing to variable
  C = therm.readCelsius();      
   //displaying temp
//Serial.print("Analog reading: "); 
   // Reading the analog value from the thermistor
 // Serial.print(therm.read());
 Serial.print("\tC: ");
 Serial.print(C);
  Serial.println("" );
//  set the led brightness
led.brightness(brightnessVal);       

    Steering_Angle=pot2.read();
    Steering_Angle=((Steering_Angle)/512*90)-90;

  
  // print the results to the serial monitor:
  Serial.print("Steering Angle = " );                      
  Serial.println(Steering_Angle);  
  Serial.println("" ); 
   
  // print the results to the serial monitor:
  Serial.print("brightness = " );                      
  Serial.println(brightnessVal);  
Serial.println("" );
Serial.println("" );
 if  ((brightnessVal > 800) || ((Steering_Angle<-30) || (Steering_Angle>30)))
  {
     digitalWrite (led_close_right , HIGH);
     digitalWrite (led_close_left , HIGH);
  }
  else {
    digitalWrite (led_close_right, LOW);
    digitalWrite (led_close_left, LOW);
  }
 
  // wait 10 milliseconds before the next loop
  delay(100);                    
}

