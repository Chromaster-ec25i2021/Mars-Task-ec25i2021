### 🔗 Tinkercad Simulation Link
[Click here to view: Question 1 - Blinking LED with Multiple Intervals](https://www.tinkercad.com/things/eaQLO1O5Sxy-my-project)


//code explanation

The system is designed to provide real-time distance monitoring and visual-auditory alerts using an HC-SR04 ultrasonic sensor. 
The operational logic begins with the microcontroller generating a 10-microsecond trigger pulse, which prompts the sensor
to emit an ultrasonic burst. By measuring the duration it takes for the echo to reflect off an object and return to the receiver,
the program calculates the physical distance using the speed of sound  This calculation is expressed by the 
formula Distance = (Duration \times 0.034) / 2, where the division by two accounts for the round-trip travel of the sound wave.
Once the distance is determined, the microcontroller categorizes the data into three safety zones to drive the feedback hardware.


For distances greater than $30\text{ cm}$, the system remains in a "Safe" state, illuminating the RGB LED in green and keeping the
buzzer silent. As an object enters the "Warning" zone ($15\text{ cm}$ to $30\text{ cm}$), the LED shifts to yellow and the buzzer emits
a pulsed tone to alert the user. If the object falls below the $15\text{ cm}$ threshold, the system enters a "Danger" state, triggering a 
constant high-frequency alarm and a red LED signal. This multi-layered feedback loop ensures high situational awareness for collision avoidance applications.

//code


/* * Name: S. Mishal mouriya
 * Project: Smart Collision Alert System
 */


const int trig = 9;

const int echo = 10;

const int buz = 11;

const int R = 6, G = 5, B = 3;



void setup() 
{
  pinMode(trig, OUTPUT);
  
  pinMode(echo, INPUT);
  
  pinMode(buz, OUTPUT);

   pinMode(R, OUTPUT); pinMode(G, OUTPUT); pinMode(B, OUTPUT);
   
  Serial.begin(9600);
}

void loop()
{
  // Trigger the ultrasonic pulse
  
  digitalWrite(trig, LOW);
  
  delayMicroseconds(2);
  
  digitalWrite(trig, HIGH);

   delayMicroseconds(10);
   
  digitalWrite(trig, LOW);

  long duration = pulseIn(echo, HIGH);
  int dist = duration * 0.034 / 2; // Physics math for distance

  Serial.print("Dist: "); Serial.println(dist);

  if (dist > 30) 
  {
    // SAFE - Green
    setColor(0, 255, 0);
    noTone(buz);
  } 
  
  else if (dist > 15 && dist <= 30) 
  {
    // WARNING - Yellow/Blue
    setColor(255, 255, 0);
    tone(buz, 500, 100); // Pulse beep
  } 
  
  else 
  {
    // DANGER - Red
    setColor(255, 0, 0);
    tone(buz, 1000); // Constant alert
  }
  
  delay(100); 
  
}


// Helper function to handle RGB colors easily

void setColor(int red, int green, int blue)
{
  analogWrite(R, red);
  analogWrite(G, green);
  analogWrite(B, blue);
}
