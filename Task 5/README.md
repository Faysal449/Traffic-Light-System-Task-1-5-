# Traffic Light System Documentation

## Overview

This project implements a *Traffic Light System* with master and slave controllers to coordinate vehicular and pedestrian traffic. The master controller manages the traffic light states, while the slave handles pedestrian button input and synchronizes pedestrian light signals with the master. 

The project utilizes *Arduino* and leverages serial communication and GPIO for coordination.

---

## Master Controller

The master controls the *traffic lights* and communicates with the slave for *pedestrian light synchronization*.

### Code Explanation

#### Pin Assignments
cpp
const int carGreen = 8;    // Car green light
const int carYellow = 7;   // Car yellow light
const int carRed = 4;      // Car red light
const int pedGreen = 11;   // Pedestrian green light
const int pedRed = 12;     // Pedestrian red light
const int buttonPin = 13;  // Pedestrian button


- *Traffic Lights:*
  - carGreen, carYellow, carRed control vehicle signals.
  - pedGreen, pedRed manage pedestrian signals.
- *Button Input:*  
  - buttonPin: Reads pedestrian button press.

---

### TrafficLight Class
The *TrafficLight* class encapsulates the logic for managing states of traffic lights.

#### Key Components
1. *States:*
   cpp
   enum TrafficState { CAR_GREEN, CAR_YELLOW, CAR_RED_PED_GREEN, CAR_RED_PED_RED, CAR_RED_TO_YELLOW };
   
   Defines the states for vehicular and pedestrian lights:
   - *CAR_GREEN:* Cars move; pedestrians stop.
   - *CAR_YELLOW:* Transition for cars; pedestrians prepare.
   - *CAR_RED_PED_GREEN:* Pedestrians cross; cars stop.
   - *CAR_RED_PED_RED:* All red (safety pause).
   - *CAR_RED_TO_YELLOW:* Transition back to green for cars.

2. *Setup:*
   Initializes the pins and sets the default state:
   cpp
   void setup() {
       pinMode(carGreen, OUTPUT);
       pinMode(carYellow, OUTPUT);
       pinMode(carRed, OUTPUT);
       pinMode(pedGreen, OUTPUT);
       pinMode(pedRed, OUTPUT);
       pinMode(buttonPin, INPUT_PULLUP);
       setCarGreen();
   }
   

3. *Update Logic:*
   Based on the state, transitions occur after predefined intervals:
   cpp
   void update() {
       switch (state) {
           case CAR_GREEN:
               // Transition to CAR_YELLOW if button is pressed.
               break;
           case CAR_YELLOW:
               // Transition to CAR_RED_PED_GREEN after delay.
               break;
           ...
       }
   }
   

4. *Light Control Functions:*
   Manage individual light states:
   cpp
   void setCarGreen() { ... }
   void setCarYellow() { ... }
   void setCarRedPedGreen() { ... }
   

---

### Main Program Flow
1. *Setup:*
   Initialize the TrafficLight object:
   cpp
   TrafficLight trafficLight;
   void setup() {
       trafficLight.setup();
   }
   

2. *Loop:*
   Continuously updates the state machine:
   cpp
   void loop() {
       trafficLight.update();
   }
   

---

## Slave Controller

The slave handles *pedestrian input* and synchronizes pedestrian light states with the master.

### Code Explanation

#### Pin Assignments
cpp
pinMode(11, OUTPUT); // Pedestrian Red LED
pinMode(12, OUTPUT); // Pedestrian Green LED
pinMode(13, INPUT_PULLUP); // Pedestrian button with pull-up resistor
pinMode(2, OUTPUT); // Output to master for pedestrian green signal
pinMode(10, OUTPUT); // Indicator LED for button press
pinMode(3, INPUT);   // Input for traffic green state from master
pinMode(6, INPUT);   // Input for traffic red state from master


- *Pedestrian Signals:*
  - 11: Red LED for stop.
  - 12: Green LED for walk.
- *Communication Pins:*
  - 2: Outputs pedestrian green signal to master.
  - 3 & 6: Read master traffic light states.
- *Button and Indicator:*
  - 13: Pedestrian button.
  - 10: LED to indicate button press.

---

### Logic Breakdown
1. *Button Press Detection:*
   Sends a signal to the master when the pedestrian button is pressed:
   cpp
   if (digitalRead(13) == LOW) { 
       digitalWrite(10, HIGH); // Indicator LED on
       Serial.write('P');      // Notify master
       delay(5000);            // Debounce
       digitalWrite(10, LOW);  // Indicator LED off
   }
   

2. *Pedestrian Green Light:*
   Activates when traffic red is detected:
   cpp
   while (digitalRead(6) == HIGH) { 
       digitalWrite(11, LOW);  // Pedestrian Red off
       digitalWrite(12, HIGH); // Pedestrian Green on
       digitalWrite(2, HIGH);  // Notify master
   }
   

3. *Reset to Default:*
   When traffic red turns off, reset pedestrian signals:
   cpp
   digitalWrite(12, LOW); // Pedestrian Green off
   digitalWrite(2, LOW);  // Reset signal
   digitalWrite(11, HIGH); // Pedestrian Red on
   

---

### Main Program Flow
1. *Setup:*
   Initializes pins and sets default states:
   cpp
   void setup() {
       Serial.begin(9600);
       pinMode(11, OUTPUT);
       pinMode(12, OUTPUT);
       ...
   }
   

2. *Loop:*
   Detects button press and coordinates pedestrian lights:
   cpp
   void loop() {
       // Handle button press and pedestrian green logic
   }
   

---

## Features

### Synchronization
The master and slave communicate to ensure safe pedestrian crossings:
- *Master:* Controls traffic lights and receives pedestrian requests.
- *Slave:* Monitors pedestrian button and signals master for synchronization.

### Modular Design
The use of the TrafficLight class allows for scalable and modular traffic management.

### Safety Mechanisms
- *All Red State:* Ensures a safety pause before state transitions.
- *Input Debouncing:* Prevents erroneous button presses.

---

## Usage Instructions

1. *Setup:*
   - Connect LEDs, button, and communication pins according to the pin assignments.

2. *Programming:*
   - Upload the *master* code to the first Arduino.
   - Upload the *slave* code to the second Arduino.

3. *Operation:*
   - The system will default to vehicular green and pedestrian red.
   - Press the pedestrian button to request a crossing. The system will safely transition to pedestrian green.

---

## Future Improvements
- Add sensors for traffic density to optimize light timings.
- Implement wireless communication between master and slave for increased flexibility.
- Integrate with a monitoring system for remote traffic control.
