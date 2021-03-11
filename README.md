# Python爬蟲之蝦皮爬爬樂_linux版本
## 動機

根據之前'Python爬蟲之蝦皮爬爬樂_windows版本'，友人A要我每天幫他跑，每天6點跑一次，收集當天資料。

因為懶，就讓旁邊不知道做什麼的linux主機，直接用 crontab 每天跑一下，所以寫了一下linux版本。



## 參數說明

```python
# linux utf8，因為 linux 會因為語系的關係出現錯誤，所以就加這一段進去，讓他認得中文字。
import sys
reload(sys)
sys.setdefaultencoding('utf-8')

# Url
url_main = '搜尋網址'
key_str = '關鍵字，拿來當 sheet title'

# GCP api，google 報表，權限部分去搜尋google 大神吧
gc = pygsheets.authorize(service_file='valid-xxxx-xxxx-xxxxxxx.json')
# 要把權限打開，認真!!
survey_url = '報表網址'

# 新創 sheet 的一行資料
wks.update_values(crange='A1',values=[
        [
            '品名',
            '項目',
            '價錢',
            '已出售',
            '商品數量',
            '產地',
            '重量',
            '出貨地',
            '網址',
        ]])
```



## 直接運作方式

執行就是了，結果 :

```
查看連線狀況: 200
連線網址: https://shopee.tw/search?keyword=%E5%86%B7%E5%87%8D%E7%99%BD%E8%9D%A6
分頁數量: 8
當頁網址: https://shopee.tw/search?keyword=%E5%86%B7%E5%87%8D%E7%99%BD%E8%9D%A6&page=0
c: 【貝蛤蛤】南美生白蝦40/50／生白蝦／白蝦／蝦子／冷凍白蝦／冷凍蝦子／冷凍食品／海鮮／
p: 270
page: 0
number_i: 1
*---------------------------------*
```

c : 網址標題

p: 多少錢

page: 頁面，通常都是從0，不知道哪天會從1開始數

number_i: 第0頁的第1筆資料



報表部分: https://docs.google.com/spreadsheets/d/1y4RNIrpryeLPylnUS3YDcnUxLMWLOK2GKa809vOWeWQ/edit#gid=2087910786



## crontab 處理方式

```
0 6 * * * /usr/bin/python /home/projects/auto_sheep/main_shopee_deep.py >> /home/test.log 2>&1
```

太久沒用 linux ，都忘記語法，這邊順便記一下

| 指令            | 功用               | 備註                                                         |
| --------------- | ------------------ | ------------------------------------------------------------ |
| sudo crontab -e | crontab 進去編輯   |                                                              |
| which           | which 尋找執行位置 | 光是找pyhon，挖到哭，結果被路過的同事說: 你為什麼不用 which，一下就知道了 (SO:學習了) |



## 結論

突然感覺，同事、朋友真好，隨便問問，一堆答案，一堆連結和一堆垃圾話。