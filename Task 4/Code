const int carGreen = 8;    // Car green light
const int carYellow = 7;   // Car yellow light
const int carRed = 4;      // Car red light
const int pedGreen = 11;   // Pedestrian green light
const int pedRed = 12;     // Pedestrian red light
const int buttonPin = 13;  // Pedestrian button

enum TrafficState { CAR_GREEN, CAR_YELLOW, CAR_RED_PED_GREEN, CAR_RED_PED_RED, CAR_RED_TO_YELLOW };

class TrafficLight {
  private:
    TrafficState state;
    unsigned long previousMillis;
    unsigned long interval;
    bool buttonPressed;

  public:
    TrafficLight() {
      state = CAR_GREEN;
      previousMillis = 0;
      interval = 0;
      buttonPressed = false;
    }

    void setup() {
      pinMode(carGreen, OUTPUT);
      pinMode(carYellow, OUTPUT);
      pinMode(carRed, OUTPUT);
      pinMode(pedGreen, OUTPUT);
      pinMode(pedRed, OUTPUT);
      pinMode(buttonPin, INPUT_PULLUP);  // Pull-up resistor to read button press
      setCarGreen();
    }

    void update() {
      unsigned long currentMillis = millis();

      if (digitalRead(buttonPin) == LOW) {
        buttonPressed = true;
      }

      switch (state) {
        case CAR_GREEN:
          if (buttonPressed) {
            interval = 5000; // 5 seconds delay before changing to yellow
            if (currentMillis - previousMillis >= interval) {
              setCarYellow();
              state = CAR_YELLOW;
              previousMillis = currentMillis;
              buttonPressed = false;  // Reset button state
            }
          }
          break;

        case CAR_YELLOW:
          interval = 2000; // 2 seconds for yellow light
          if (currentMillis - previousMillis >= interval) {
            setCarRedPedGreen();
            state = CAR_RED_PED_GREEN;
            previousMillis = currentMillis;
          }
          break;

        case CAR_RED_PED_GREEN:
          interval = 5000; // 5 seconds for pedestrian crossing
          if (currentMillis - previousMillis >= interval) {
            setCarRedPedRed();
            state = CAR_RED_PED_RED;
            previousMillis = currentMillis;
          }
          break;

        case CAR_RED_PED_RED:
          interval = 2000; // 2 seconds with all red before switching to yellow
          if (currentMillis - previousMillis >= interval) {
            setCarRedToYellow();
            state = CAR_RED_TO_YELLOW;
            previousMillis = currentMillis;
          }
          break;

        case CAR_RED_TO_YELLOW:
          interval = 2000; // 2 seconds of yellow before turning green
          if (currentMillis - previousMillis >= interval) {
            setCarGreen();
            state = CAR_GREEN;
            previousMillis = currentMillis;
          }
          break;
      }
    }

    void setCarGreen() {
      digitalWrite(carGreen, HIGH);
      digitalWrite(carYellow, LOW);
      digitalWrite(carRed, LOW);
      digitalWrite(pedGreen, LOW);
      digitalWrite(pedRed, HIGH);
    }

    void setCarYellow() {
      digitalWrite(carGreen, LOW);
      digitalWrite(carYellow, HIGH);
      digitalWrite(carRed, LOW);
      digitalWrite(pedGreen, LOW);
      digitalWrite(pedRed, HIGH);
    }

    void setCarRedPedGreen() {
      digitalWrite(carGreen, LOW);
      digitalWrite(carYellow, LOW);
      digitalWrite(carRed, HIGH);
      digitalWrite(pedGreen, HIGH);
      digitalWrite(pedRed, LOW);
    }

    void setCarRedPedRed() {
      digitalWrite(carGreen, LOW);
      digitalWrite(carYellow, LOW);
      digitalWrite(carRed, HIGH);
      digitalWrite(pedGreen, LOW);
      digitalWrite(pedRed, HIGH);
    }

    void setCarRedToYellow() {
      digitalWrite(carGreen, LOW);
      digitalWrite(carYellow, HIGH);
      digitalWrite(carRed, LOW);
      digitalWrite(pedGreen, LOW);
      digitalWrite(pedRed, HIGH);
    }
};

TrafficLight trafficLight;

void setup() {
  trafficLight.setup();
}

void loop() {
  trafficLight.update();
}
