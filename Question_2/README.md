
//Tinkercad Simulation Link
[Click here to view: Question 2 - RGB and LED Control](https://www.tinkercad.com/things/ezPeDwJ7Bs5-question-2-ec25i2021)



//Explanation of code

Logic and OperationThe system logic is centered on the acquisition of an analog signal from a potentiometer, which serves as a user-controlled input 
to modulate two separate output behaviors. By utilizing the analogRead() function, the microcontroller samples a voltage between 
translates it into a digital integer ranging from $0$ to $1023$. This value is then processed through the map() function to determine a dynamic 
timing interval for a standard LED, effectively allowing the user to adjust the blinking speed in real-time by rotating the potentiometer knob.
To ensure the system remains responsive, the program implements a non-blocking timing mechanism using millis(), which permits the microcontroller 
to check the potentiometer state and update the RGB LED colors without pausing the execution flow. The color control is achieved through a series 
of conditional statements that divide the potentiometer's input range into three distinct segments. Depending on the current input value, the program
sends Pulse Width Modulation (PWM) signals to the red, green, or blue anodes of the RGB LED, facilitating a seamless transition between primary colors as the input voltage changes.



//code


//ec25i2021
//S.Mishal Mouriya

int knobPin = A0;

int r = 6, g = 5, b = 3; // RGB Pins
int led = 13;

unsigned long t_ref = 0; 
int state = 0;

void setup() 
{
  pinMode(r, OUTPUT);
  pinMode(g, OUTPUT);
  pinMode(b, OUTPUT);
  pinMode(led, OUTPUT);
}


void loop() 
{

  int val = analogRead(knobPin);
  
  
  // Handle the blinking LED speed
  
  int speed = map(val, 0, 1023, 100, 2000);
  unsigned long now = millis();
  

  if (now - t_ref >= speed)
  {
    t_ref = now;
    state = !state;
    digitalWrite(led, state);
  }
  

  

  // Handle RGB color shifts

  
  if (val < 340)
  {
    analogWrite(r, 255); analogWrite(g, 0); analogWrite(b, 0);
  } 
  
  else if (val < 680) 
  {
    analogWrite(r, 0); analogWrite(g, 255); analogWrite(b, 0);
  } 
  
  else 
  {
    analogWrite(r, 0); analogWrite(g, 0); analogWrite(b, 255);
  }

  
}
