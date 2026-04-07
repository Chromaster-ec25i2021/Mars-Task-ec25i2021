


//Link to Tinkercad circuit
[Click here to view the Tinkercad Simulation](https://www.tinkercad.com/things/i0ojHjmMpsN-ec25i2021-question-1)


//Explanation of code 


The circuit operates by utilizing the millis() function to track elapsed time without halting the processor's execution. 
Unlike the standard delay() function, which creates a "blocking" state that prevents other tasks from running, this approach 
allows the Arduino to manage multiple timing intervals for three separate 
LEDs simultaneously.
By continuously monitoring the system's uptime, the program can determine if specific durations—500ms, 1000ms, or 1500ms—have 
passed for each digital pin without one LED's timing affecting the others.

The core logic relies on a conditional check that calculates the difference between the current time and the last recorded timestamp for each pin.
When this difference reaches the predefined interval, the timestamp is updated to the current time, and the LED's state is flipped using a logical NOT operator. 
This process ensures that each LED toggles between HIGH and LOW independently, creating a non-blocking execution flow where all three blinking 
patterns occur in parallel at their respective frequencies.

// C++ code

unsigned long previousTime1 = 0;
unsigned long previousTime2 = 0;
unsigned long previousTime3 = 0;


int state1 = LOW;
int state2 = LOW;
int state3 = LOW;

void setup()
{
  pinMode(13, OUTPUT);
  pinMode(12, OUTPUT);
  pinMode(11, OUTPUT);
}

void loop() 
{
  unsigned long currentTime = millis();

  if (currentTime - previousTime1 >= 500)
  {
    previousTime1 = currentTime;
    state1 = !state1;
    digitalWrite(13, state1);
  }
  
  if (currentTime - previousTime2 >= 1000) 
  {
    previousTime2 = currentTime;
    state2 = !state2;
    digitalWrite(12, state2);
  }
  
  if (currentTime - previousTime3 >= 1500)
  {
    previousTime3 = currentTime;
    state3 = !state3;
    digitalWrite(11, state3);
  }
  
}
