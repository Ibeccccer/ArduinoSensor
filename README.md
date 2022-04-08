# ArduinoSensor
Sensorgithub
#include <AnalogUVSensor.h>
/*
  ReadAnalogVoltage

  Reads an analog input on pin 0, converts it to voltage, and prints the result to the Serial Monitor.
  Graphical representation is available using Serial Plotter (Tools > Serial Plotter menu).
  Attach the center pin of a potentiometer to pin A0, and the outside pins to +5V and ground.

  This example code is in the public domain.

  https://www.arduino.cc/en/Tutorial/BuiltInExamples/ReadAnalogVoltage
*/
const int numReadings = 5;

int readings1[numReadings];     // the readings from the analog input
int readings2[numReadings];
int readings3[numReadings];
int readIndex1 = 0;              // the index of the current reading
int readIndex2 = 0;
int readIndex3 = 0;
int total1 = 0;                 // the running total
int total2 = 0;
int total3 = 0;
int average1 = 0;                // the average
int average2 = 0;
int average3 = 0;
int inputPin1 = A10;
int inputPin2 = A2;
int inputPin3 = A3;
// the setup routine runs once when you press reset:
void setup() {
  // initialize serial communication at 9600 bits per second:
  Serial.begin(9600);
}

// the loop routine runs over and over again forever:
void loop() {
  // read the input on analog pin 0:
  total1 = total1 - readings1[readIndex1];
  total2 = total2 - readings2[readIndex2];
  total3 = total3 - readings3[readIndex3];
  readings1[readIndex1] = analogRead(A10)-60;
  readings2[readIndex2] = analogRead(A4);
  readings3[readIndex3] = analogRead(A3);
  total1 = total1 + readings1[readIndex1];
  total2 = total2 + readings2[readIndex2];
  total3 = total3 + readings3[readIndex3];
  readIndex1 = readIndex1 + 1;
  readIndex2 = readIndex2 + 1;
  readIndex3 = readIndex3 + 1;
  if (readIndex1 >= numReadings) {
    readIndex1 = 0;
  }
  if (readIndex2 >= numReadings) {
    readIndex2 = 0;
  }
  if (readIndex3 >= numReadings) {
    readIndex3 = 0;
  }
  average1 = total1 / numReadings;
  average2 = total2 / numReadings;
  average3 = total3 / numReadings;
  // Convert the analog reading (which goes from 0 - 1023) to a voltage (0 - 5V):
  float V1 = average1 * (150 / 255.0); // Voltage1 = V1
  float V2 = average2 * (100 / 255.0);  // x30
  float V3 = average3 * (300 / 255.0);  //x300
  Serial.print(V1);
  Serial.print(",");
  Serial.print(V2);
  Serial.print(",");
  Serial.print(V3);
  Serial.println();
  Serial.print("V1=");
  Serial.print(average1);
  Serial.print(",");
  Serial.print("V2=");
  Serial.print(average2);
  Serial.print(",");
  Serial.print("V3=");
  Serial.print(average3);
  Serial.println();  
  delay(25);
}
