# ES2022 - 實作4: 七段顯示器, LCD 顯示器 + 超音波感測器

<a name="000"/>

## 目錄(Table of Contents)

[Lab 4-1 用七段顯示器來顯示數字"8."](#111)

[Lab 4-2 如下圖的Demo, 用七段顯示器, 顯示 . →1→ ... → 9 → 0 → 全滅, 狀態改變的間隔時間為0.5秒](#222)

[Lab 4-3 LCD顯示"Hello" + 你的英文名字 (e.g., "Hello Horace")](#333)

[## Lab 4-4 整合超音波感測器 + LCD + LED](#444)


## Lab 4-1 用七段顯示器來顯示數字"8."

<a name="111"/>

### Circuit

<div align="left">
     <img 
      src="https://user-images.githubusercontent.com/89304181/137589897-c40100d5-3e87-4eca-a1b5-39c65ad7c3a8.png" 
      width="70%" height="70%">
    </div>

### Code

````C
void setup()
{
for(int x = 1; x < 9; x++) {
pinMode(x,OUTPUT);
}
}

void seg71(int a, int b, int c, int d, int e, int f, int g, int h)
{
digitalWrite(1, a);
digitalWrite(2, b);
digitalWrite(3, c);
digitalWrite(4, d);
digitalWrite(5, e);
digitalWrite(6, f);
digitalWrite(7, g);
digitalWrite(8, h);
delay(500);
}

void loop()
{
//    a, b, c, d, e, f, g, h
seg71(0, 0, 0, 0, 0, 0, 0, 0); // OFF
seg71(1, 1, 1, 1, 1, 1, 1, 1); // 8
}
````

[return to content](#000) 

## Lab 4-2 如下圖的Demo, 用七段顯示器, 顯示 . →1→ ... → 9 → 0 → 全滅, 狀態改變的間隔時間為0.5秒

<a name="222"/>

### Circuit

![image](https://github.com/Grace-TA/ES-Fall2021/blob/main/Lab4-7seg-lcd/Lab4-2.gif)

### Code

> 參考程式: 可參考Lab4-1的程式或是自行設計完成以上的任務.

---

## Lab 4-3 LCD顯示"Hello" + 你的英文名字 (e.g., "Hello Horace")

<a name="333"/>

### Circuit

![image](https://github.com/Grace-TA/ES-Fall2021/blob/main/Lab4-7seg-lcd/Lab4-3.gif)

### Code

````C
// include the library code:
#include <LiquidCrystal.h>

// initialize the library with the numbers of the interface pins
LiquidCrystal lcd(12, 11, 5, 4, 3, 2);

void setup() {
  // set up the LCD's number of columns and rows:
  lcd.begin(16, 2);
  // Print a message to the LCD.
  lcd.print("hello, Horace!");
}

void loop() {
  // set the cursor to column 0, line 1
  // (note: line 1 is the second row, since counting begins with 0):
  lcd.setCursor(0, 1);
  // print the number of seconds since reset:
  lcd.print(millis() / 100);
````

![image](https://user-images.githubusercontent.com/89304181/137607314-aeab5548-2264-46eb-b05d-ca0d6114a166.png)

[return to content](#000) 

## Lab 4-4 整合超音波感測器 + LCD + LED: 參考之前的實作, 將超音波感測器傳回的距離, 在LCD上面顯示, 同時也和之前的實作一樣, 在序列輸出. 另外, 當物體的距離小於150cm時, 則亮紅色LED, 否則亮綠色LED

<a name="444"/>

### Circuit

![image](https://github.com/Grace-TA/ES-Fall2021/blob/main/Lab4-7seg-lcd/Lab4-4.gif)

### Code
````C
/*
Developed for Embedded System Course, VNU by Horace. Fall 2021
*/

#include <LiquidCrystal.h> //LCD library
  
  #define echo 7
  #define trig 7
  
  float  duration; // time taken by the pulse to return back
  float  dd; // oneway distance travelled by the pulse
  int RLED = 9;
  int GLED = 8;
  LiquidCrystal lcd(12, 11, 5, 4, 3, 2); 

  void setup() {
  
	digitalWrite(RLED, OUTPUT);
  digitalWrite(GLED, OUTPUT);
    
    Serial.begin(9600);
    lcd.begin(16, 2);
  
  }
  
  void loop() {
  
    time_Measurement();
    dd = duration * 0.01723;   

/*
		待完成
*/

    
  }
  
  void time_Measurement()
  { //function to measure the time taken by the pulse to return back
    pinMode(trig, OUTPUT);
    digitalWrite(trig, LOW);
    delayMicroseconds(2);  
    digitalWrite(trig, HIGH);
    delayMicroseconds(10);
    digitalWrite(trig, LOW);
    pinMode(echo, INPUT);  
    duration = pulseIn(echo, HIGH);
  }

````

[return to content](#000) 
