// Solar Tracking and Soil Moisture Control System

#include <Servo.h>

// Solar Tracking System Variables
#define LDR1 A0
#define LDR2 A1
#define ERROR 10
int Spoint = 90;
Servo servo;

// Soil Moisture Control Variables
int waterPin = 6; // Input pin from soil sensor
int relayPin = 3; // Output pin for relay board

void setup() {
  // Initialize Servo Motor
  servo.attach(11);
  servo.write(Spoint);
  delay(1000);

  // Initialize Soil Moisture Sensor and Relay
  pinMode(relayPin, OUTPUT);
  pinMode(waterPin, INPUT);
}

void loop() {
  // Solar Tracking System Logic
  int ldr1 = analogRead(LDR1);
  int ldr2 = analogRead(LDR2);
  int value1 = abs(ldr1 - ldr2);
  int value2 = abs(ldr2 - ldr1);

  if ((value1 > ERROR) && (value2 > ERROR)) {
    if (ldr1 > ldr2) {
      Spoint = max(Spoint - 1, 0); // Ensure Spoint doesn't go below 0
    } 
    if (ldr1 < ldr2) {
      Spoint = min(Spoint + 1, 180); // Ensure Spoint doesn't exceed 180
    }
    servo.write(Spoint);
  }

  // Soil Moisture Control Logic
  int water = digitalRead(waterPin);
  if (water == HIGH) {
    digitalWrite(relayPin, LOW); // Turn off relay if water level is full
  } else {
    digitalWrite(relayPin, HIGH); // Turn on relay if water level is low
  }

  delay(400); // Delay for both tracking and moisture control
}
