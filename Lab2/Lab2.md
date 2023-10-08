# 實作2: 會呼吸的RGB LED,  按鍵控制, 狀態輸出

## 實作2-1, analogWrite(): 並且觀查LED亮度變化是否有像"呼吸的效果"和示波器的波形有什麼關連性?

### 電路 & Demo

![image](https://user-images.githubusercontent.com/89304181/190887391-19c13d3d-0f5a-4bd4-87d8-5bf9fdeb2642.png)

https://user-images.githubusercontent.com/89304181/190887475-b1eb7895-a183-4454-80b2-881e6ccf3a36.mp4

### 程式

```C
int brightness = 0;

void setup()
{
  pinMode(9, OUTPUT);
}

void loop()
{
  for (brightness = 0; brightness <= 255; brightness += 5) {
    analogWrite(9, brightness);
    delay(30); // Wait for 30 millisecond(s)
  }
  for (brightness = 255; brightness >= 0; brightness -= 5) {
    analogWrite(9, brightness);
    delay(30); // Wait for 30 millisecond(s)
  }
}

```


## 實作2-2, RGB LED燈全彩模組, 分別讓LED輪流表現正紅、正綠、正藍，三個顏色，時間間隔1秒鐘。並且觀查LED顏色和波形或是電壓有什麼關連性?

### 電路 & Demo

https://user-images.githubusercontent.com/89304181/190882877-a72f17e2-d526-42c4-8d3f-10a6bf39d54f.mp4

### 程式

```C
//
/*
  This program blinks pin 13 of the Arduino (the
  built-in LED)
*/

const int Red = 9;
const int Green = 10;
const int Blue = 11;

void setup()
{
  pinMode(Red, OUTPUT);
  pinMode(Green, OUTPUT);
  pinMode(Blue, OUTPUT);
}

void loop()
{
  // turn the LED on (HIGH is the voltage level)
  analogWrite(Red, 255);
  analogWrite(Green, 0);
  analogWrite(Blue, 0);
  delay(1000); // Wait for 1000 millisecond(s)
  
  analogWrite(Red, 0);
  analogWrite(Green, 255);
  analogWrite(Blue, 0);
  delay(1000); // Wait for 1000 millisecond(s)
  
  analogWrite(Red, 0);
  analogWrite(Green, 0);
  analogWrite(Blue, 255);
  delay(1000); // Wait for 1000 millisecond(s)  
}

```

## 實作2-3, 讓你的RGB LED燈全彩模組也可會"呼吸", LED顏色變化是否有像"呼吸的效果"和示波器的波形有什麼關連性?

### 電路 & Demo

https://user-images.githubusercontent.com/89304181/190882880-04ebd9cf-1dcf-4526-9292-6d9178db4da2.mp4

### 程式

```C
int R = 9;
int G = 10;
int B = 11;

int DR = 2;
int DG = 4;
int DB = 7;

void setup()
{
  pinMode(13, OUTPUT); // pin 13
  
  pinMode(R, OUTPUT);
  pinMode(G, OUTPUT);
  pinMode(B, OUTPUT);  
  
  pinMode(DR, OUTPUT);
  pinMode(DG, OUTPUT);
  pinMode(DB, OUTPUT);   
}

void loop()
{
  // digitalWrite: 2 state (i.e., 0, 1) Only
  digitalWrite(13, 1); // LED @ pin 13, ON
  
  delay(1000); 
  
  digitalWrite(DR, 1);
  digitalWrite(DG, 0);
  digitalWrite(DB, 0);
  delay(1000);
  digitalWrite(DR, 0);
  digitalWrite(DG, 1);
  digitalWrite(DB, 0);  
  delay(1000);
  digitalWrite(DR, 0);
  digitalWrite(DG, 0);
  digitalWrite(DB, 1);  
  delay(1000);

  digitalWrite(13, 0); // OFF
  digitalWrite(DR, 0); // OFF
  digitalWrite(DG, 0); // OFF
  digitalWrite(DB, 0); // OFF  
  delay(1000);
  
  // analogWrite: The brightness can be adjusted with 256 levels
  for (int i = 0; i<= 255; i++)
  {
  	analogWrite(R, i);
		analogWrite(G, 0);
		analogWrite(B, 0);
    delay(10);
  } // from dark to bright 

  for (int i = 255; i>= 0; i--)
  {
  	analogWrite(R, i);
		analogWrite(G, 0);
		analogWrite(B, 0);
    delay(10); // 10ms = 0.01s
  }  // from bright to dark
  delay(1000);
}

```
## 實作2-4 analogRead(), 1024解析度 (i.e.,10-bit): 可變電阻 + 序列監視器與輸出; 當你改變可變電阻的阻值(e.g., 10K-ohm)時，序列監視器輸出的數值有什麼改變? 數值又有什麼意義呢? 可試將你的想法寫在你的GitHub Page中喔!

### 電路 & Demo

https://user-images.githubusercontent.com/89304181/192082695-ac52c281-1b63-46be-a956-c7f871b6ac03.mp4


### 程式

```C
int sensorValue = 0;

void setup()
{
  pinMode(A0, INPUT);
  Serial.begin(9600);
}

void loop()
{
  // read the input on analog pin 0:
  sensorValue = analogRead(A0);
  // print out the value you read:
  Serial.println(sensorValue);
  delay(10); // Delay a little bit to improve simulation performance
}

```

## 實作2-5: 按下按鍵, Green LED亮 & Red LED滅; 放開按鍵, Green LED滅 & Red LED亮. 想要再深入的同學可以試試喔. (思考方向: digitalRead(), digitalWrite(): 按鍵 +序列輸出 + LED)
### 電路 & Demo

https://user-images.githubusercontent.com/89304181/192082725-ca8efeee-9b69-4656-9eb5-91ce840082a3.mp4

### 程式

```C
int buttonState = 0;
int GLED = 13;
int RLED = 8;
void setup()
{
  pinMode(2, INPUT);
  
  pinMode(GLED, OUTPUT);
  pinMode(RLED, OUTPUT);
  
  Serial.begin(9600);
}

void loop()
{
  // read the state of the pushbutton value
  buttonState = digitalRead(2);
  // check if pushbutton is pressed.  if it is, the
  // buttonState is HIGH
  if (buttonState == HIGH) {
    // turn LED on
    digitalWrite(GLED, HIGH);
    digitalWrite(RLED, LOW);
    
  } else {
    // turn LED off
    digitalWrite(GLED, LOW);
    digitalWrite(RLED, HIGH);
  }
  Serial.println(buttonState);
  delay(10); // Delay a little bit to improve simulation performance
}

```
