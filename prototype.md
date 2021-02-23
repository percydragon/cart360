### Arduino System
Below are the two versions of the code used for the Arduino System, both the original version and the version that was modified by Ellio after our discussion on Feb 1, 2021.

**original code**
```
/ FSR simple testing sketch. Connect one end of FSR to power, the other end to Analog 0.
Then connect one end of a 10K resistor from Analog 0 to ground
/

/ FSR testing sketch.
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
```


**updated by Ellio**
```
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
The reasons for the modification made by Ellio was so that the could would not simply take one instance and read it, but multiple instance of the input.

### Images and Videos of Prototype
Listed below are images of the prototype

![Image of Arduino](/cart360/CIRCUIT.jpg)

<video src="video0.mov" width="320" height="200" controls preload></video>



### Images of Fabric considered for project

![Image of Scarf 1](https://cdn.discordapp.com/attachments/623295778412167180/805869798859866162/IMG_8030.jpg)

The fabric depicted here is far to sheer to be able to support the motors needed for the vibration.

![Image of Scarf 2](https://cdn.discordapp.com/attachments/623295778412167180/805869807407726632/IMG_8031.jpg)

This scarf here would not be suitable for an all around scarf, as the fabric is far too thick to be worn in the summer, it would be far better suited for a winter scarf, since that's the scarf's original purpose is.

![Image of Scarf 3](https://cdn.discordapp.com/attachments/623295778412167180/805869807449931826/IMG_8032.jpg)

The scarf depicted here would be the perfect type of scarf to use for the project, but I'd rather not ruin one of my own personal scarves. Secondly, I think that the scarf would require to be double layered so that the motors can be secured safely into the scarf.

![Image of Fabric](https://cdn.discordapp.com/attachments/623295778412167180/805869808797089822/IMG_8033.jpg)

Shown are there selected fabrics for the project. The purple fabric would be used to keep the motors solidly in place, as its a a much more rigid fabric, compared to the pink fabric, that's more cute and has a bird print pattern on it.

With these layers, the motors would be secure, and as discusse with Ellio, there would be some soft of stuffing to keep the motors secured. The FSR would be at one end of the scarf, and would also be safe secured and accessible to the user.

#### Links used
[Electronic Clinic](http://www.electroniclinic.com/arduino-micro-vibration-motor-arduino-vibration-motor-code-interfacing/)

[Instructables](https://www.instructables.com/Interfacing-Force-Sensitive-Resistor-to-Arduino/)
