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
加圖片  
實驗適當斜度後可以熱熔膠黏貼在瓦楞板上，並切割寶特瓶當錢幣容器  
加圖片  
用另外一片瓦楞板，將4顆PIR sensor、RasbperryPi、breadboard都用熱溶膠貼在上面，並以杜邦線完成接線  
加圖片  
這次選用的GPIO說明如下  
加圖片  
* 軟體
在Rasbperry Pi 3安裝RasbperryPi os，安裝步驟可以參考以下網站  
https://www.raspberrypi.org/documentation/computers/using_linux.html#creating-a-new-user  
接下來就在終端機先安裝python的flask套件  
```$ pip install Flask```  
前置作業都完成了之後，我們就要來寫程式囉!  
第一支程式是要將接收感應器傳回來的值，並且加總所有金額，我將這隻程式存檔為coinbankwihPIR.py  
```python
gpio.board(15)
```  
第二支程式是使用flask將我們加總的結果以網頁呈現，我將這隻程式存檔為app.py  
```python
gpio.board(15)
```    
# 實作影片
來自受零用錢鼓舞的孩童
# 參考資料
https://www.youtube.com/watch?v=ItbHdrFvzlg  
https://www.tinkercad.com/  
https://hackmd.io/@shaoeChen/SyP4YEnef?type=view  
https://www.raspberrypi.org/  
