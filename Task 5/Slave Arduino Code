
void setup() {
  Serial.begin(9600); // Start serial communication

  pinMode(11, OUTPUT); // Pedestrian Red LED
  pinMode(12, OUTPUT); // Pedestrian Green LED
  pinMode(13, INPUT_PULLUP); // Pedestrian button with pull-up resistor
  pinMode(2, OUTPUT); // Output pin to signal pedestrian green state to master
  pinMode(10, OUTPUT); // Indicator LED for button press
  pinMode(3, INPUT); // Input pin to read traffic green state from master
  pinMode(6, INPUT); // Input pin to read traffic red state from master

  // Default state: Pedestrian Red LED on
  digitalWrite(11, HIGH); // Pedestrian Red LED on
  digitalWrite(2, LOW);   // Ensure initial state is LOW for pedestrian green signal
  digitalWrite(10, LOW);  // Ensure indicator LED is off
}

void loop() {
  // Check if the pedestrian button is pressed
  if (digitalRead(13) == LOW) { 
    digitalWrite(10, HIGH); // Turn on indicator LED
    Serial.write('P'); // Send signal to master for pedestrian request
    delay(5000); // Small delay to debounce the button
    digitalWrite(10, LOW); // Turn off indicator LED after sending request
  }

  // Independent while loop to manage pedestrian green light
  while (digitalRead(6) == HIGH) { // HIGH on pin 6 means traffic red is on
    digitalWrite(11, LOW);  // Pedestrian Red LED off
    digitalWrite(12, HIGH); // Pedestrian Green LED on
    digitalWrite(2, HIGH);  // Signal to master that pedestrian green is on
    delay(2); // Small delay to avoid rapid looping
  }

  // After the while loop, traffic red has turned off
  // Turn off pedestrian green and reset signals
  digitalWrite(12, LOW); // Pedestrian Green LED off
  digitalWrite(2, LOW);  // Reset pedestrian green signal to LOW
  Serial.write('R'); // Signal to master that pedestrian green is off
  digitalWrite(11, HIGH); // Pedestrian Red LED on
}
