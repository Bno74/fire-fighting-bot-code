#include <Servo.h>

// Pin definitions
const int motor1Pin1 = 1; // IN1
const int motor1Pin2 = 2; // IN2
const int motor2Pin1 = 3; // IN3
const int motor2Pin2 = 4; // IN4
const int flameSensorPin = 5; // D0 from flame sensor
const int relayPin = 6; // Relay IN pin
const int buzzerPin = 7; // Buzzer
const int servoPin = 9; // Servo motor

Servo waterPumpServo;

void setup() {
    // Initialize motor control pins
    pinMode(motor1Pin1, OUTPUT);
    pinMode(motor1Pin2, OUTPUT);
    pinMode(motor2Pin1, OUTPUT);
    pinMode(motor2Pin2, OUTPUT);
    
    // Initialize other components
    pinMode(flameSensorPin, INPUT);
    pinMode(relayPin, OUTPUT);
    pinMode(buzzerPin, OUTPUT);

    // Initialize the servo
    waterPumpServo.attach(servoPin);
    waterPumpServo.write(0); // Set initial position of the servo
    digitalWrite(relayPin, LOW); // Ensure relay is off initially
}

void loop() {
    if (detectFlame()) {
        // If flame is detected, activate the firefighting sequence
        activateFirefighting();
    } else {
        // If no flame is detected, stop motors and turn off the relay
        stopMotors();
        digitalWrite(relayPin, LOW);
        noTone(buzzerPin); // Turn off buzzer
    }
}

bool detectFlame() {
    // Read the flame sensor value
    int flameSensorValue = digitalRead(flameSensorPin);
    return flameSensorValue == LOW; // Assuming LOW indicates flame detected
}

void activateFirefighting() {
    // Turn on the buzzer
    tone(buzzerPin, 1000); // 1 kHz sound

    // Start the motors
    moveForward();

    // Activate the water pump
    digitalWrite(relayPin, HIGH); // Turn on relay to activate pump
    waterPumpServo.write(90); // Rotate the servo to spray water
    delay(2000); // Spray water for 2 seconds
    waterPumpServo.write(0); // Reset servo position

    // Stop the motors after spraying water
    stopMotors();
}

626364656667686970717273747576777879808182
#include <Servo.h>

// Pin definitions
const int motor1Pin1 = 1; // IN1
const int motor1Pin2 = 2; // IN2
const int motor2Pin1 = 3; // IN3
const int motor2Pin2 = 4; // IN4
const int flameSensorPin = 5; // D0 from flame sensor
const int relayPin = 6; // Relay IN pin
const int buzzerPin = 7; // Buzzer
…    // Stop all motors
    digitalWrite(motor1Pin1, LOW);
    digitalWrite(motor1Pin2, LOW);
    digitalWrite(motor2Pin1, LOW);
    digitalWrite(motor2Pin2, LOW);
}

void moveForward() {
    // Move motors forward
    digitalWrite(motor1Pin1, HIGH);
    digitalWrite(motor1Pin2, LOW);
    digitalWrite(motor2Pin1, HIGH);
    digitalWrite(motor2Pin2, LOW);
626364656667686970717273747576777879808182
#include <Servo.h>

// Pin definitions
const int motor1Pin1 = 1; // IN1
const int motor1Pin2 = 2; // IN2
const int motor2Pin1 = 3; // IN3
const int motor2Pin2 = 4; // IN4
const int flameSensorPin = 5; // D0 from flame sensor
const int relayPin = 6; // Relay IN pin
const int buzzerPin = 7; // Buzzer
…    digitalWrite(motor2Pin2, LOW);
}

}

void stopMotors() {
    // Stop all motors
    digitalWrite(motor1Pin1, LOW);
    digitalWrite(motor1Pin2, LOW);
    digitalWrite(motor2Pin1, LOW);
    digitalWrite(motor2Pin2, LOW);
}
