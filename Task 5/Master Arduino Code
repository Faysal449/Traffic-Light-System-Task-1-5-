
const int trafficRedPin = 4;
const int trafficYellowPin = 7;
const int trafficGreenPin = 8;
const int pedestrianGreenPin = 2; // Input pin to read pedestrian green state from slave
const int trafficGreenSignalPin = 3; // Output pin to signal traffic green state
const int trafficRedSignalPin = 6; // Signal to slave that red is active

void setup() {
  Serial.begin(9600); // Start serial communication

  pinMode(trafficRedPin, OUTPUT); 
  pinMode(trafficYellowPin, OUTPUT); 
  pinMode(trafficGreenPin, OUTPUT); 
  pinMode(pedestrianGreenPin, INPUT); 
  pinMode(trafficGreenSignalPin, OUTPUT); 
  pinMode(trafficRedSignalPin, OUTPUT); 
}

void loop() {
  // Main loop to check pedestrian state every 2 ms
  while (digitalRead(pedestrianGreenPin) == HIGH) {
    delay(2); // Check every 2 milliseconds if pedestrian light is on

    // Ensure the traffic green light cannot be on
    digitalWrite(trafficGreenPin, LOW);
    digitalWrite(trafficGreenSignalPin, LOW);
  }

  // Default traffic light sequence if pedestrian green is off

  // Green light phase
  digitalWrite(trafficGreenPin, HIGH); 
  digitalWrite(trafficGreenSignalPin, HIGH); 
  delay(5000); // Keep green on for 5 seconds
  digitalWrite(trafficGreenPin, LOW); 
  digitalWrite(trafficGreenSignalPin, LOW);

  // Yellow light transition
  digitalWrite(trafficYellowPin, HIGH); 
  delay(2000); // Yellow for 2 seconds
  digitalWrite(trafficYellowPin, LOW);

  // Red light phase
  digitalWrite(trafficRedPin, HIGH); 
  digitalWrite(trafficRedSignalPin, HIGH); 
  delay(5000); // Keep red on for 5 seconds
  digitalWrite(trafficRedPin, LOW); 
  digitalWrite(trafficRedSignalPin, LOW);

  // Brief yellow transition before returning to green
  digitalWrite(trafficYellowPin, HIGH); 
  delay(2000); 
  digitalWrite(trafficYellowPin, LOW);
}

void handlePedestrianRequest() {
  // Traffic light transition: Green to Yellow
  digitalWrite(trafficGreenPin, LOW); 
  digitalWrite(trafficGreenSignalPin, LOW);
  digitalWrite(trafficYellowPin, HIGH); 
  delay(2000); // Yellow for 2 seconds

  // Transition to Red
  digitalWrite(trafficYellowPin, LOW);
  digitalWrite(trafficRedSignalPin, HIGH); 
  digitalWrite(trafficRedPin, HIGH); 
  delay(7000); // Pedestrian crossing time

  // Brief yellow signal before switching back to green
  digitalWrite(trafficYellowPin, HIGH); 
  delay(2000);
  digitalWrite(trafficRedSignalPin, LOW); 
  digitalWrite(trafficYellowPin, LOW); 

  // Wait until pedestrian green is off before resuming normal traffic sequence
  while (digitalRead(pedestrianGreenPin) == HIGH) { 
    delay(1000);
  }
}
