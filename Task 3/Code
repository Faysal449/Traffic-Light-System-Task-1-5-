// Define a TrafficLight class
class TrafficLight {
private:
    int redPin;    // Pin for the red LED
    int yellowPin; // Pin for the yellow LED
    int greenPin;  // Pin for the green LED

public:
    // Constructor to initialize the pins
    TrafficLight(int red, int yellow, int green) {
        redPin = red;
        yellowPin = yellow;
        greenPin = green;
        pinMode(redPin, OUTPUT);
        pinMode(yellowPin, OUTPUT);
        pinMode(greenPin, OUTPUT);
    }

    // Method to turn the lights on/off
    void turnOff() {
        digitalWrite(redPin, LOW);
        digitalWrite(yellowPin, LOW);
        digitalWrite(greenPin, LOW);
    }

    void redLight() {
        turnOff();
        digitalWrite(redPin, HIGH);
    }

    void yellowLight() {
        turnOff();
        digitalWrite(yellowPin, HIGH);
    }

    void greenLight() {
        turnOff();
        digitalWrite(greenPin, HIGH);
    }
};

// Instantiate three traffic lights
TrafficLight trafficLight1(2, 3, 4); // Traffic light 1
TrafficLight trafficLight2(5, 6, 7); // Traffic light 2
TrafficLight trafficLight3(8, 9, 10); // Traffic light 3

void setup() {
    // Setup is done in the TrafficLight constructor
}

void loop() {
    // Traffic Light 1
    trafficLight1.redLight();
    delay(3000); // Red light for 3 seconds
    trafficLight1.yellowLight();
    delay(1000); // Yellow light for 1 second
    trafficLight1.greenLight();
    delay(3000); // Green light for 3 seconds

    // Traffic Light 2
    trafficLight2.redLight();
    delay(3000);
    trafficLight2.yellowLight();
    delay(1000);
    trafficLight2.greenLight();
    delay(3000);

    // Traffic Light 3
    trafficLight3.redLight();
    delay(3000);
    trafficLight3.yellowLight();
    delay(1000);
    trafficLight3.greenLight();
    delay(3000);
}
