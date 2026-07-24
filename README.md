// Pin assignments
const int greenLED = 2;
const int yellowLED = 3;
const int redLED = 4;
const int buzzer = 6;        // Buzzer on D6
const int waterSensor = A0;  // Water sensor connected to A0

void setup() {
  pinMode(greenLED, OUTPUT);
  pinMode(yellowLED, OUTPUT);
  pinMode(redLED, OUTPUT);
  pinMode(buzzer, OUTPUT);
  pinMode(waterSensor, INPUT);
  Serial.begin(9600); // For Serial Monitor
}

void loop() {
  int waterLevel = analogRead(waterSensor); // Read water sensor
  
  // Print the sensor reading
  Serial.print("Water Level: ");
  Serial.println(waterLevel);

  // Decision making based on water level reading
  if (waterLevel < 200) {
    // No water: All OFF
    digitalWrite(greenLED, LOW); 
    digitalWrite(yellowLED, LOW);
    digitalWrite(redLED, LOW);
    digitalWrite(buzzer, LOW);
  }
  else if (waterLevel >= 200 && waterLevel < 300) {
    // Low water: Green ON
    digitalWrite(greenLED, HIGH); 
    digitalWrite(yellowLED, LOW); 
    digitalWrite(redLED, LOW); 
    digitalWrite(buzzer, LOW);
  }
  else if (waterLevel >= 300 && waterLevel < 330) {
    // Medium water: Yellow ON
    digitalWrite(greenLED, LOW); 
    digitalWrite(yellowLED, HIGH); 
    digitalWrite(redLED, LOW); 
    digitalWrite(buzzer, LOW);
  }
  else {
    // High water: Red ON + Buzzer ON
    digitalWrite(greenLED, LOW); 
    digitalWrite(yellowLED, LOW); 
    digitalWrite(redLED, HIGH); 
    digitalWrite(buzzer, HIGH);
  }
  
  delay(500); 
}
