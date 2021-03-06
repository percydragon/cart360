### Final Artifact
In the making of the final artifact, I have been having some technical difficulties. While having thought i had properly resolved an issue, I had in fact not taken into consideration that I probably had not solved it. Here is the documentation of that currently still unresolved issue.

**Code**
```
int fsrPin = 0;     // the FSR and 10K pulldown are connected to a0
int fsrReading;     // the analog reading from the FSR resistor divider
int mvmOne = 11; // the motor is connected to pin 5
int mvmTwo = 10;
int mvmThree = 9;
int mvmFour = 6;
int mvmFive = 5; // these are all the motors that are connected to the arduino
int data = 0;
int data_action = 0;
int mvmShake;

void setup() {
  // put your setup code here, to run once:
  pinMode(fsrPin, INPUT);
  pinMode(mvmOne, OUTPUT);
  pinMode(mvmTwo, OUTPUT);
  pinMode(mvmThree, OUTPUT);
  pinMode(mvmFour, OUTPUT);
  pinMode(mvmFive, OUTPUT);
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
  analogWrite(mvmOne, data_action);
  analogWrite(mvmTwo, data_action);
  analogWrite(mvmThree, data_action);
  analogWrite(mvmFour, data_action);
  analogWrite(mvmFive, data_action);


  // we'll need to change the range from the analog reading (0-1023) down to the range
  // used by analogWrite (0-255) with map!
  mvmShake = map(data, 0, 1023, 0, 255);
  // LED gets brighter the harder you press
  analogWrite(mvmOne, mvmShake);
  analogWrite(mvmTwo, mvmShake);
  analogWrite(mvmThree, mvmShake);
  analogWrite(mvmFour, mvmShake);
  analogWrite(mvmFive, mvmShake);

  delay(100);



}

```

Currently the issue is that only the pin connected to mvmOne is working properly, while the rest are not. I've been discussing the issue with my brother, as well as looking into similar issues online, and have found a possible solution [here](https://stackoverflow.com/questions/26048539/multiple-pins-within-a-function-argument). Hopefully it gives me the proper solution needed.

I'm thankful I waited before sewing, because if I had, I would not have been able to know if my project were actually properly working or not. So, before I sew everything up, I am making sure that the circuit itself is functioning as intended.

Here are videos of the issue with the circuit.

<video src="video1.mov" width="320" height="200" controls preload></video>

<video src="video2.mov" width="320" height="200" controls preload></video>


### Updates on Code
In attempting to figure out the issues with coin motors, and testing them all, it seems that all the coins are fried, and only one of the coin motors works, regardless of which pin i attach it to. Knowing this, I have decided to simply use the one coin motor, and move on as such. I documented this process to demonstrate that I did attempt to make multiple coins work together, but the issue is not with the code, but rather the electronics themselves. 

However, regardless of the friend motors, here are some resources I used in search of figuring out how to make multiple coin motors work.

The idea would be to have an array, and use port manipulation to have multiple coins working at once, but since the ports aren't working, I cannot employ this method.

[Port Manipulation](https://www.arduino.cc/en/Reference/PortManipulation) [Multiple Pins Array](https://stackoverflow.com/questions/26048539/multiple-pins-within-a-function-argument)

here is the code I used to figure out that the other coins were fried.

```
int fsrPin = 0;     // the FSR and 10K pulldown are connected to a0
int fsrReading;     // the analog reading from the FSR resistor divider

int mvmFour = 4;

int data = 0;
int data_action = 0;
int mvmShake;

void setup() {
  // put your setup code here, to run once:
  pinMode(fsrPin, INPUT);


  pinMode(mvmFour, OUTPUT);

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

  analogWrite(mvmFour, data_action);


  // we'll need to change the range from the analog reading (0-1023) down to the range
  // used by analogWrite (0-255) with map!
  mvmShake = map(data, 0, 1023, 0, 255);
  // LED gets brighter the harder you press

  analogWrite(mvmFour, mvmShake);


  delay(100);



}
```

I simply moved the coin that was still working to a different pin, and the coin vibrated, so, in conclusion, all my other coins are simply fried. I'm thankful, at least, that one of the coins still works, and that I can properly finish this project, and have something to present, rather than nothing at all.
