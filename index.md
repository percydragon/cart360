## Welcome to Percy Dragon's documentation

Below is the documentation of the prototype for CART 360 and what will become the final artifact.
While the title for the project itself has not been decided, I have temporarily called it "Vibrating Scarf".

### Arduino System

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
*original code*
/* FSR simple testing sketch.  <br>Connect one end of FSR to power, the other end to Analog 0.
Then connect one end of a 10K resistor from Analog 0 to ground
*/

/* FSR testing sketch.
Connect one end of FSR to 5V, the other end to Analog 0.
Then connect one end of a 10K resistor from Analog 0 to ground
Connect LED from pin 13 through a resistor to ground

int fsrPin = 0;     // the FSR and 10K pulldown are connected to a0
int fsrReading;     // the analog reading from the FSR resistor divider
int mvm = 5; // the motor is connected to pin 5
int data = 0;
int mvmShake;

void setup(void) {
  pinMode(fsrPin, INPUT);
  pinMode(mvm, OUTPUT);
  Serial.begin(9600);
}

void loop(void) {
  fsrReading = analogRead(fsrPin);

  Serial.print("Analog reading = ");
  Serial.print(fsrReading);     // the raw analog reading


  if (fsrReading == 0) {
    Serial.println(" - No pressure");
  } else if (fsrReading < 10) {
    Serial.println(" - Light touch");
  } else if (fsrReading < 50) {
    Serial.println(" - Light squeeze");
  } else if (fsrReading < 150) {
    Serial.println(" - Medium squeeze");
  } else {
    Serial.println(" - Big squeeze");
  }
  delay(1000);
}

void loop(void) {
  // put your main code here, to run repeatedly:
  data = analogRead(fsrReading);
  Serial.print("Analog reading = ");
  Serial.println(fsrReading);
  data = map(data, 0, 1023, 0,255);
  analogWrite(mvm, data);

  // we'll need to change the range from the analog reading (0-1023) down to the range
  // used by analogWrite (0-255) with map!
  mvmShake = map(fsrReading, 0, 1023, 0, 255);
  // LED gets brighter the harder you press
  analogWrite(mvm, mvmShake);

  delay(100);
}


*updated by Ellio*
int fsrPin = 0;     // the FSR and 10K pulldown are connected to a0
int fsrReading;     // the analog reading from the FSR resistor divider
int mvm = 11; // the motor is connected to pin 5
int data = 0;
int data_action = 0;
int mvmShake;

void setup() {
  // put your setup code here, to run once:
  pinMode(fsrPin, INPUT);
  pinMode(mvm, OUTPUT);
  Serial.begin(9600);
}

int sampleFSR() {
  int _t = 0;

    for(int i =0; i < 32; i++){
      _t += analogRead(fsrReading);
      delay(1);
      }
  return (_t/32);
}

void loop() {
  // put your main code here, to run repeatedly:
    //fsrReading = analogRead(fsrPin);
    data = sampleFSR();

  Serial.print("Analog reading = ");
  Serial.print(data);     // the raw analog reading


  if (data == 0) {
    Serial.println(" - No pressure");
  } else if (data < 10) {
    Serial.println(" - Light touch");
  } else if (data < 50) {
    Serial.println(" - Light squeeze");
  } else if (data < 150) {
    Serial.println(" - Medium squeeze");
  } else {
    Serial.println(" - Big squeeze");
  }
  delay(1000);

    // put your main code here, to run repeatedly:
//  data = sampleFSR();
  //Serial.print("Analog reading = ");
 // Serial.println(data);
  data_action = map(data, 0, 1023, 0,255);
  analogWrite(mvm, data_action);

  // we'll need to change the range from the analog reading (0-1023) down to the range
  // used by analogWrite (0-255) with map!
  mvmShake = map(data, 0, 1023, 0, 255);
  // LED gets brighter the harder you press
  analogWrite(mvm, mvmShake);

  delay(100);



}

```
