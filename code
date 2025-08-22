#include <Stepper.h>

double rad = 0.2;
double revConvFac = 1.0 / 28;
double stepsPerRevolution = 513;
int totalStepsMoved = 0;  // Track total steps moved
Stepper myStepper(stepsPerRevolution, 8, 10, 9, 11);

void setup() {
  myStepper.setSpeed(20);
  Serial.begin(9600);
  Serial.println("Enter volume in cubic inches or type 'Home': ");
}

void loop() {
  if (Serial.available() > 0) {
    String input = Serial.readStringUntil('\n');  // Read full input
    input.trim();  // Remove spaces and newlines

    if (input.equalsIgnoreCase("Home")) {
      myStepper.step(-totalStepsMoved);  // Move back to home
      totalStepsMoved = 0;  // Reset step counter
    } else {
      double volume = input.toFloat();  // Convert to double
      if (volume > 0) {
        Serial.print("Dispensing volume: ");
        Serial.println(volume);
        double length = volume / (3.1416 * rad * rad); 
        double revs = length / revConvFac;
        int steps = revs * stepsPerRevolution;
        myStepper.step(steps);
        totalStepsMoved += steps;  // Keep track of total movement
      } else {
        Serial.println("Invalid input. Enter a positive volume or 'Home'.");
      }
    }
  }
}
