# IOT_intelligent coin bank-智慧撲滿

# 關於智慧撲滿
這是一項IOT的實作，可以為你解決一堆零錢不知道怎麼整理、不知道數量是多少的困擾，  
讓你可以利用網頁，就知道今天存進撲滿的零錢是多少，當你月光光心慌慌的時候，就可以打開撲滿繼續揮霍囉~

# 運作方式介紹
* 使用模型依錢幣大小切割後，當錢幣投入模型中時能依尺寸歸類到該錢幣該去的類別
* 設置4個PIR sensor來感應每個類別掉落的錢幣數
* 使用樹梅派將PIR sensor感應到的資訊回傳到python程式中，並使用flask套件顯示在網路上

# 設備
## 硬體
### 錢幣分類模型
* 瓦楞板
* 寶特瓶
* 熱熔膠
### 感應計數
* Rasbperry Pi 3
* breadboard
* PIR sensor *4
* Dupont Lines
## 軟體
* RasbperryPi os
* python
* pip3 install flask
 
# 開始實作
* 硬體  
依實際錢幣大小割下虛線  
![投影片1](https://user-images.githubusercontent.com/97165881/148979248-359c8494-e630-4631-9c73-0ee84ed335b2.JPG)  
實驗適當斜度後可以熱熔膠黏貼在瓦楞板上，並切割寶特瓶當錢幣容器  
![投影片2](https://user-images.githubusercontent.com/97165881/148979288-d69f7f63-d673-4121-be20-1c6fd955ee68.JPG)
用另外一片瓦楞板，將4顆PIR sensor、RasbperryPi、breadboard都用熱溶膠貼在上面，並以杜邦線完成接線  
![投影片3](https://user-images.githubusercontent.com/97165881/148979321-838b8d64-c13b-4988-a437-929303ff7637.JPG) 
這次選用的GPIO說明如下  
![投影片4](https://user-images.githubusercontent.com/97165881/148979383-3fd8a75c-64b9-4fac-9f56-41951cc8e28e.JPG)

* 軟體
在Rasbperry Pi 3安裝RasbperryPi os，安裝步驟可以參考以下網站  
https://www.raspberrypi.org/documentation/computers/using_linux.html#creating-a-new-user  
接下來就在終端機先安裝python的flask套件  
```$ pip install Flask```  
前置作業都完成了之後，我們就要來寫程式囉!  
第一支程式是要將接收感應器傳回來的值，並且加總所有金額，我將這隻程式存檔為coinbankwihPIR.py  
```python
import RPi.GPIO as GPIO
from time import procese_time
GPIO.setwarnings(False)
GPIO.setmode(GPIO.BOARD)
GPIO.setup(13, GPIO.IN)         #Read output from PIR motion sensor for$1
GPIO.setup(15, GPIO.IN)         #Read output from PIR motion sensor for$5
GPIO.setup(16, GPIO.IN)         #Read output from PIR motion sensor for$10
GPIO.setup(18, GPIO.IN)         #Read output from PIR motion sensor for$50
def coinbank():
    count1 = 0
    count5 = 0
    count10 = 0
    count50 = 0
    while True:
     a=GPIO.input(13)
     b=GPIO.input(15)
     c=GPIO.input(16)
     d=GPIO.input(18)
     if a==1:                 
      count1 += a
      print("$1")
     if b==1:               
      count5 += 1
      print("$5")
     if c==1:               
      count10 += 1
      print("$10")
     if d==1:               
      count50 += 1
      print("$50")
     if process_time() > 0.1:
         break
    total = count1*1+count5*5+count10*10+count50*50
    return "tatol : &",str(total)
```  
第二支程式是使用flask將我們加總的結果以網頁呈現，我將這隻程式存檔為app.py  
```python
from flask import Flask
from coinbankwithPIR import coinbank


app = Flask(__name__)

@app.route("/coinbank")
def home():
    return coinbank()

app.run()
```    
# 實作影片
希望奇蹟出現
# 參考資料
https://www.youtube.com/watch?v=ItbHdrFvzlg  
https://www.tinkercad.com/  
https://hackmd.io/@shaoeChen/SyP4YEnef?type=view  
https://www.raspberrypi.org/  
