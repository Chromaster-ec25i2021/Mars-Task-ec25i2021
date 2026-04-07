# Mars-Task-ec25i2021
Created to complete task 1 of Mars


. Project Overview & Motivation
The Smart Collision Alert System is a proximity-sensing device designed to assist in automotive parking and obstacle avoidance.
The system utilizes ultrasonic sound waves to measure the distance between the sensor and an external object in real-time. 
Based on the calculated distance, the device provides a three-tiered feedback response: a green "safe" light, a yellow "warning" pulse
with an intermittent beep, and a red "danger" light with a continuous high-frequency alarm.

This project was selected because it represents a practical application of embedded systems found in modern vehicle safety technology. 
The implementation allows for the integration of multiple engineering concepts, including ultrasonic physics, Pulse Width Modulation (PWM) for color mixing, and conditional logic for safety thresholds.



2. Components and Their Roles

Arduino Uno R3: Serves as the central processing unit to interpret sensor data and control the output devices.


HC-SR04 Ultrasonic Sensor: Functions as the input device by sending and receiving ultrasonic pulses to determine proximity.

Common-Cathode RGB LED: Provides a visual status indicator by shifting colors between green, yellow, and red.

Piezo Buzzer: Acts as an auditory alert system that increases in intensity as the detected distance decreases.

220 Ohm Resistors: Used for current limiting to protect the LED components and Arduino pins from electrical damage.

Breadboard & Jumper Wires: Facilitate the physical connections and power distribution throughout the circuit.



3. Challenges and Solutions

Challenge: Component Overload and Current Limits During initial testing, the RGB LED was subjected to excessive current, \

eading to a "blasting" warning in the simulation environment. This was caused by an error in the physical layout where the resistors
were placed in the same electrical row as the LED legs, effectively bypassing the resistance.

Solution: The wiring was corrected by rotating the resistors to bridge across different rows on the breadboard.
This ensured that the 220 Ohm resistance was properly applied, limiting the current to a safe 20mA per pin.



Challenge: Distance Calculation Accuracy The raw data from the ultrasonic sensor is provided as a duration in microseconds, which does not directly represent distance.

Solution: A physical conversion formula was implemented to translate time into centimeters. By applying the speed of sound (0.034 cm/µs) and dividing the total duration
by two to account for the round-trip of the signal, the system achieved accurate distance readings.



Challenge: System Latency and Responsiveness Excessive delays in the code could prevent the sensor from detecting fast-moving objects in time to trigger an alert.

Solution: The main loop was optimized to use a minimal delay of 100ms. This maintains a high sampling rate, ensuring the visual and auditory feedback remains synchronized
with the object's movement without significant lag.
