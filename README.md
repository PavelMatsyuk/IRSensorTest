//# IRSensorTest
//Testing an IR Sensor on an Arduino Uno

const int pinIRd = A2; //setting pinout variables
const int pinIRa = A0;
const int pinLED = 9;
const int pinLED2 = 5;

int IRvalueA = 0; //setting initial values. necessary?
int IRvalueD = 0;
int Count = 0;

unsigned long timeInt = 0; //using unsinged longs to track the timer
unsigned long starttime = 0;
unsigned long endtime = 0;


void setup() {
  // put your setup code here, to run once:
Serial.begin(9600); //starts output to the serial console
pinMode(pinIRd, INPUT); //telling the arduino what the pins are supposed to do
pinMode(pinIRa, INPUT);
pinMode(pinLED, OUTPUT);
pinMode(pinLED2, OUTPUT);
}

void loop() {
  // Main code here, infinte while loop
IRvalueA = analogRead(pinIRa); //specifies the Analog read pinout on the Arduino
IRvalueD = digitalRead(pinIRd); //specifies the digigal read pinout on the Arduino.

digitalWrite(pinLED2, LOW); //turns the LED off. The LED only turns on when the if condition is true

if (IRvalueA < 500) { //Using the analog value to enter the loop.
  endtime = millis();
  timeInt = endtime - starttime;
  starttime = endtime;
  Count++; //this tracks events.  I plan on using this to count rotations of the bike wheel
  delay(100);
}

Serial.print("Analog Reading = "); //outputs the desired text to the console
Serial.print(IRvalueA);
Serial.print("\t Time Interval = ");
Serial.print(timeInt);
Serial.print("\t Count = ");
Serial.println(Count);
}
