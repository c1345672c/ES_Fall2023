# 實作3: 使用超音波感測器 + LED控制, C語言程式速成

## Lab 3-1: Ultrasonic Sensor (3-pin) + 測距 (以公分顯示即可) + RS232 Output

### Circuit, Demo, and Code

https://user-images.githubusercontent.com/89304181/192084084-b356cb4d-b1d5-4506-a40c-760f6179b68b.mp4


## Lab 3-2: 超音波感測器 + LED (紅色LED:亮<70cm, 藍色LED: 亮>270cm, 緑色LED:亮, 介於70cm ~ 270cm之間) + RS232 Output

### Circuit, Demo, and Code

https://user-images.githubusercontent.com/89304181/192084087-25c4fbc3-4482-4d6d-a6be-1d87d15b7ffe.mp4


## Lab 3-3: Arduino常用的C語言程式介紹與實作

### Circuit, Demo

https://user-images.githubusercontent.com/89304181/192084091-24ba5d91-2455-4449-a514-b458967849e5.mp4

### Code

```C
/*
 Lab 3-3, Embedded System, VNU
 Date: 2021/09/26
*/
int RLED = 13;
int GLED = 11;


int result, result2, result3;
String d0 = "****** 9X9 Table ******";
String d1, d2, d3;
void setup()
{
  pinMode(RLED, OUTPUT);   // Configure PIN13
  pinMode(GLED, OUTPUT);   // Configure PIN11
  
  Serial.begin(9600);

}

void loop()
{
  int aa = 0;

  Serial.println(d0); 
  
  digitalWrite(RLED, HIGH);
  analogWrite(GLED, aa); 
  
  for (int i=1;i<=9; i=i+3){
    for (int j=1;j<=9; j++){
      
      result = i*j;
      result2 = (i+1)*j;
      result3 = (i+2)*j;
      
      d1 = String(String(i) + "X" + String(j) + "=" + String(result));

     /*
       待完成
     */
      
      Serial.println(d1 + ", " + d2 + ", " + d3);
    
      aa+=1;
      
      delay(100);
    } // loop j
    analogWrite(GLED, aa*3); 
    Serial.println("");
  } // loop i

  digitalWrite(RLED, LOW);
  analogWrite(GLED, 255); 
  delay(2000);	
  analogWrite(GLED, 0);
}


```
