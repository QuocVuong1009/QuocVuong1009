#include <LiquidCrystal.h>
LiquidCrystal lcd (12, 11, 5, 4, 3, 2);
/*
 Nối chân LCD:
 VDD nối 5V
 VSS nối GND 
 RW nối GND
 RS chân 12
 E chân 11
 D4 chân 5/ D5 chân 4/ D6 chân 3/ D7 chân 2
 */
/*
 Nối chân cảm biến vật thể:
 VCC nối 5V
 GND nối GND
 Out nối chân 1
 */
/*
 Nối chân cảm biến màu TCS3200
 VCC nối 5V
 GND nối GND
 s0 nối chân 8
 s1 nối chân 9
 s2 nối chân 10
 s3 nối chân 13
 Out nối chân 7
 OE nối GND
 */
 int ObjectSensor = 1; 
 int Pre = HIGH;
 int CountRed = 0; //Đếm số lượng sản phẩm màu đỏ
 int CountBlue = 0; //Đếm số lượng sản phẩm màu xanh dương
 int CountGreen = 0; //Đếm số lượng sản phẩm màu xanh lá
 int CountError = 0; //Số lượng sản phẩm bị lỗi
 int s0 = 8;
 int s1 = 9;
 int s2 = 10;
 int s3 = 13;
 int ColorSensor = 7;
 //các biến để so sánh
 int ToRed; //Dùng để phân loại màu đỏ
 int ToBlue; //Dùng để phân loại màu xanh dương
 int ToGreen; //Dùng để phân loại màu xanh lá


void setup() 
{
  lcd.begin(16, 2);
  pinMode(ObjectSensor, INPUT);
  pinMode(s0, OUTPUT);
  pinMode(s1, OUTPUT);
  pinMode(s2, OUTPUT);
  pinMode(s3, OUTPUT);
  pinMode(ColorSensor, INPUT);
  //Tần số lọc là 20%
  digitalWrite(s0, HIGH);
  digitalWrite(s1, LOW);
  //
  ToRed = 0;
  ToGreen = 0;
  ToBlue = 0;
}

void loop() 
{
  int isObject = digitalRead(ObjectSensor);
  if (isObject == LOW && Pre == HIGH)
  {
    GetColor(); 
    delay(1000);
    //So sánh các khoảng giá trị để xác định màu
    if (ToRed >= 25 && ToRed <= 40 && ToRed <= ToGreen && ToRed <= ToBlue)
    {
      CountRed++;
    }
    else if (ToBlue >= 18 && ToBlue <= 30 && ToRed >= ToBlue && ToGreen >= ToBlue)// && ToGreen <= ToRed)
    {
      CountBlue++;
    }
    else if (ToRed >= ToGreen && ToBlue >= ToGreen && ToBlue >= ToRed)
    {
      CountGreen++;
    }
    else
    {
      CountError++;
    }
  }
  Pre = isObject;
  lcd.setCursor(0, 0); //cột 0 hàng 0
  lcd.print("RED:");
  lcd.setCursor(4, 0); //cột 4 hàng 0
  lcd.print(CountRed);
  lcd.setCursor(8, 0); //cột 8 hàng 0
  lcd.print("BLUE:");
  lcd.setCursor(13, 0); //cột 13 hàng 0
  lcd.print(CountBlue);
  lcd.setCursor(0, 1); //cột 0 hàng 1
  lcd.print("GREEN:");
  lcd.setCursor(6, 1); //cột 6 hàng 1
  lcd.print(CountGreen);
  lcd.setCursor(10, 1); //cột 10 hàng 1
  lcd.print("ER:");
  lcd.setCursor(13, 1); //cột 13 hàng 1
  lcd.print(CountError);
}

void GetColor()
{
  //Lọc màu đỏ
  digitalWrite(s2, LOW);
  digitalWrite(s3, LOW);
  ToRed = pulseIn(ColorSensor, LOW);
  delay(100);

  //Lọc màu xanh dương
  digitalWrite(s2, LOW);
  digitalWrite(s3, HIGH);
  ToBlue = pulseIn(ColorSensor, LOW);
  delay(100);

  //Lọc màu xanh lá
  digitalWrite(s2, HIGH);
  digitalWrite(s3, HIGH);
  ToGreen = pulseIn(ColorSensor, LOW);
  delay(100);
}
