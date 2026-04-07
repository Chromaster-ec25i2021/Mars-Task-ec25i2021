
// 🔗 Tinkercad Simulation Link
[Click here to view: Question 3 - Reaction Time Tester](https://www.tinkercad.com/things/22BPO43Klcn-ec25i2021-question-3)


//Code Explanation

The operation of the reaction timer is governed by a state-machine approach that alternates between a randomized idle phase and an active measurement phase. 
Upon initialization, the microcontroller generates a random delay between $2000$ and $5000$ milliseconds, ensuring that the visual stimulus is unpredictable for the user.
Once this period concludes, the program illuminates an LED and captures the exact system uptime using the millis() function, transitioning the system into a waiting state to monitor for user input.

The detection of the user's response is facilitated by a digital pushbutton configured with the internal INPUT_PULLUP resistor. 
This configuration causes the input pin to read a logic HIGH state by default, which transitions to LOW when the physical button is 
depressed and the pin is shorted to ground. The microcontroller calculates the reaction speed by subtracting the stimulus timestamp from 
the response timestamp  outputting the resulting duration in milliseconds to the Serial Monitor
before resetting the cycle for subsequent testing.

//code

//S.Mishal Mouriya
//ec25i2021


int led = 13;

int btn = 2;

unsigned long start_t = 0;

bool waiting = false;


void setup() 
{
  pinMode(led, OUTPUT);
  
  pinMode(btn, INPUT_PULLUP); // Use internal resistor

  Serial.begin(9600);
  
  Serial.println("Wait for the LED... then CLICK!");
}



void loop()

{

  if (!waiting) 
  
  {
    // Wait for a random time between 2 and 5 seconds
    delay(random(2000, 5000)); 
    digitalWrite(led, HIGH);
    start_t = millis(); // Record the exact start time
    waiting = true;
  }

  


  // Check if button is pressed (LOW because of INPUT_PULLUP)

  
  if (waiting && digitalRead(btn) == LOW) 
  
  {
    unsigned long reaction_t = millis() - start_t;
    digitalWrite(led, LOW);    
    Serial.print("Reaction Time: ");
    Serial.print(reaction_t);
    Serial.println(" ms");    
    waiting = false; // Reset for next round
    delay(1000);     // Brief pause before next test
  }

  
}
