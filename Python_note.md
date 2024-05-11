# Python

>Anaconda 開發環境
>spyder
## 變數與運算式
### 變數命名規則
>coding style

```
NewDataAlter
new_data_alter
coding format
```

### 變數
```
a = 1
a = b = c = 100
a, b = 30, 30
```

### 刪除變數
`del a`

### 變數定義地雷
```
for = 3
jack_1 = 1
1_jack = 1
```

### 隱藏變數
```
_a = 1  # a=100
```

### 註解

#單行註解

"""
這是多行註解 # 多行註解也可以當作字串
這是多行註解
這是多行註解
"""

### type 命令
```
a = 1
type(a)
b = 1.0
type(b)
c = "1"
type(c)
d = True
type(True)
type(d)
e = False
type(e)
```

### 字串定義須知
```
str1 = "'123!'"
str2 = '"123!"'
str3 = "\"123!\""
```

### 透過input 去取得使用者輸入值
```
name = input('input your name:')
print('your name is ', name)

print("123\t\t123")
print("123\n123")
```

### 運算子「+」的功能

```
a = 1
b = 1.0
c = "1"
d = True

a + b
a + c  # 數值不能跟字串做計算
c + c  # 字串相加 在python 裡面代表合併
d + a  # True -> 1  # False -> 0
d + d
d + False
```

### 轉換型態
```
int(c) + a
float(c) + 1
str(a) + c
```

#### 牛刀小試: 請使用者輸入兩次數值並將兩個數值相加後顯示
```
a1 = int(input('請輸入數值1:'))
a2 = int(input('請輸入數值2:'))
print(a1+a2)
```


### print 用法
```
print(a, b)
print(a, b, sep='\t')

print(a, b)
print(a, b)

print(a, b, end=' ')
print(a, b)
```

### fstring 用法
```
a = f'my name is jack'
name = 'jack'
a = f'my name is {name}'
cc = '123'
a = f'{cc} is {name}'
print(a)
```
### 字串格式化
`'%s xxx' % ('123')`

#### 牛刀小試:
```
a1 = int(input('請輸入國文成績:'))
a2 = int(input('請輸入數學成績:'))
a3 = int(input('請輸入英文成績:'))
print(f"總成績為:{a1+a2+a3}")
```

### Python計算符號
```
1+1
1-1
11*11
10/3
100//3
100 % 3
2**10
```

### 先乘除後加減
```
1+2*5
(1+2)*5
```

#### 計算梯形面積
```
a1 = float(input('請輸入上底:'))
a2 = float(input('請輸入下底:'))
a3 = float(input('請輸入高:'))
shape = (a1+a2)*a3/2
print(f"面積為:{shape}")
```


### 比較運算子
```
a = 1
a == 1
1 != 3  # !->not
1 > 3
1 < 3
1 >= 3
1 <= 3
```

### 邏輯運算子
```
""" 
and 並且 
and 是兩者為真 才回傳真 其餘為否
"""
True and True
False and True
1 > 3 and 4 > 5

""" 
or 或者 
or 是兩者為否 才回傳否 其餘為真
"""
True or False
False or False
True or True

""" 
not 布林值反轉
"""
not True
not False
```

### 複合指定運算子
```
a = 1
a+1
a = a+1
a += 1
a **= 10
```

#### 牛刀小試: 輸入本金 回傳終值
```
capital = float(input('請輸入本金:'))
ratio = float(input('請輸入利率:'))
year = int(input('請輸入年分:'))
capital *= (1+ratio)**year
print(f'結果為:{capital}')
```

```
a+=1+6+5==3 and 1+2
    _____        ___
    ________
    ________________
____________________

```

## 判斷式&迴圈

### 程式流程
>判斷句 迴圈
判斷 a == 1
決定做什麼事情

```
a = 2
if a == 1:
    print('a等於1')
else:
    print('a不等於1')
```

### 雙向判斷式
>如果 .... 除此之外 ....
if XXX:
    區塊1
else:
    區塊2

```
a = 2
if a == 1:
    print('a等於1')
    print('另外的')
else:
    print('a不等於1')
    print('另外的')

print(123)
```

#### 牛刀小試:密碼輸入判斷
```
password = input('請輸入密碼:')
if password == '1234':
    print('密碼正確')
else:
    print('密碼錯誤')
```

#### 牛刀小試:進階密碼判斷
```
password = input('請輸入密碼:')
if password == '1234':
    print('一般密碼正確')
elif password == 'admin1234':
    print('管理者密碼正確 登入')
> elif ...:
     ...
else:
    print('密碼錯誤')
```

#### 牛刀小試:判斷成績等第
```
score = int(input('請輸入成績(0~100):'))
if score >= 90:
    print('優等')
elif score >= 80:
    print('甲等')
elif score >= 70:
    print('乙等')
elif score >= 60:
    print('丙等')
else:
    print('丁等')
```

### 巢狀判斷
>if 條件1:
    區塊1
    if 條件2:
        區塊2
        if 條件3:
            區塊3
            print('都滿足條件')
        print(123)

#### 牛刀小試:百貨公司折扣戰

```
消費金額 = int(input('請輸入消費金額:'))
disconut_ratio = 1

if 消費金額 >= 10000:
    disconut_ratio = 0.95
    if 消費金額 >= 30000:
        disconut_ratio = 0.9
        if 消費金額 >= 50000:
            disconut_ratio = 0.85
            if 消費金額 >= 100000:
                disconut_ratio = 0.8

消費金額 *= disconut_ratio
print(f'折扣後消費金額:{消費金額}')
```

### for 迴圈

>迴圈 的意義是執行重複的動作
for 迴圈
for 迴圈變數 in 集合:運算式

```
for i in (1, 2, 3, 4, 5, 6, 7, 8):
    print(f'i目前的值為{i}')
```

#### 牛刀: 透過迴圈把元素的值都進行相加
```
a = 0
b = 0
for i in (1, 2, 3, 4, 5, 6, 7, 8):
    a += i
    if i % 2 == 0:
        b += i
print(f'所有數值加總:{a}')
print(f'只加偶數加總:{b}')

for i in range(10):
    print(i)

for i in range(50, 60):
    print(i)

for i in range(50, 60, 2):
    print(i)
```

#### 從1加到10000 該怎麼寫？
```
a = 0
for i in range(1, 10000+1):
    a += i
print(a)


n = int(input('請輸入正整數:'))
for i in range(1, n+1):
    print(i, end=' ')


n = int(input('請輸入正整數:'))
x = 0
for i in range(1, n+1):
    x += i
print(x)

for i in range(1, 4):
    for j in range(1, 4):
        print(f"i:{i},j:{j}")
```

### 寫出一個99乘法表
```
for i in range(1,10):
    for j in range(1,10):
        r=i*j
        print(f"{i}*{j}={r}",end='\t')
    print()


```

#### 輸入三筆同學的資料
```
成績 = {}
for _i in range(3):
    name = input('請輸入同學名稱:')
    score = int(input('請輸入同學成績:'))
    成績[name] = score

print(成績)
```

#### 透過輸入同學名稱 來查詢成績
```
name = input('請輸入查詢的名稱:')
print(f'該同學的成績為:{成績[name]}')


成績.keys()
成績.values()
100 in 成績.values()

for key, value in 成績.items():
    print(f'key:{key}, value:{value}')
```



####
```
import random
天氣 = '晴天'
if 天氣 == '晴天':
    print('不用帶傘')
else:
    print('帶傘')

for i in range(10):
    print(i)
print(123)
```

#### 寫出一個99乘法表
```
for i in range(1, 9+1):
    for j in range(1, 9+1):
        print(f"{i}*{j}={i*j}", end='\t')
    print('')
```

### break 命令
>迴圈的指令
break 結束迴圈 (只能用在 迴圈中)

```
for i in range(10):
    print(i)
    if i == 5:
        break
```

#### 牛刀小試:找最小公倍數
```
# 取得使用者輸入的 a b
a = int(input('請輸入數值:'))
b = int(input('請輸入數值:'))
# 透過for迴圈去跑i = 1到a*b
for i in range(1, (a*b)+1):
    # 判斷 i 是否可以被 a、b 整除
    if i % a == 0 and i % b == 0:
        # 如果可以的話 跳出迴圈
        break
# 顯示i (最小公倍數)
print(f"{i}為最小公倍數")
```

### continue命令
>跳過該循環 (只能用在 迴圈中)
```
for i in range(10):
    if i == 5:
        continue
    print(i)
```

#### 牛刀小試:顯示正整數數列，排除5的倍數
```
x = int(input('請輸入數值:'))
for i in range(1, x+1):
    if i % 5 == 0:
        continue
    print(i, end=' ')
```

### while 迴圈
>依照判斷是決定是否繼續執行的模式
無限迴圈
```
while True:
    print(1)

while False:
    print(1)
```

### 有限迴圈
```
a = 1
while a <= 10:
    print(a)
    a += 1
```

#### 牛刀小試:透過 while 迴圈 1加到5
```
a = 1
b = 0
while a <= 5:
    print(f"開始 a:{a} b:{b}")
    b += a
    a += 1
    print(f"結束 a:{a} b:{b}")

print(b)
```

#### 牛刀小試:透過 while 迴圈 1乘到N
```
n = int(input('請輸入數值:'))
a = 1
b = 1
while a <= n:
    b *= a
    a += 1

print(b)
```
#### 互動式小遊戲 — 終極密碼

```
終極密碼 = random.randint(1, 99)
# 透過迴圈請使用者去猜 密碼
尚未猜中 = True
while 尚未猜中:
    使用者猜測 = int(input('請輸入密碼:'))
    # 判斷 使用者的猜測值 是否 更大
    if 使用者猜測 > 終極密碼:
        # 提示密碼更小
        print('密碼更小')
    # 判斷 使用者的猜測值 是否 更小
    elif 使用者猜測 < 終極密碼:
        # 提示密碼更大
        print('密碼更大')
    # 判斷 使用者的猜測值 是否 相等
    else:
        print('BOOM ! 你猜中了')
        尚未猜中 = False
```

## 串列 & 元組 & 字典

### 串列宣告  (list)

```
x = []
type(x)

x = [1, 2, 3, 4, '5', '6', '7']  # 中括號定義
x[0]  # 中括號filter
x[5]
x[:5]
x[3:]
x[1:3]
x[-1]
```

### 抓到這個list的最後4個值 該怎麼做
```
x[-4:]
```
### 該怎麼透過for 迴圈 去取得前5個值呢?
```
for i in range(5):
    print(x[i])

x[-3] = 100
```


### 直接將X內的元素取得
```
for i in x:
    print(i)
```

### 透過X的index 取得X的元素
```
for i in range(len(x)):
    print(x[i])
```
#### 牛刀小試:利用迴圈配合索引讀取串列元素
```
subjects = ["國文", "數學", "英文"]
scores = [85, 79, 93]

for i in range(len(subjects)):
    # print(subjects[i],scores[i])
    print(f"科目:{subjects[i]} 分數:{scores[i]}")
```
### 串列搜尋與計次
```
print(123)
```
### index() 搜尋
```
x.index(100)
```
```
x.index(1440)
```
### count() 計算次數
```
x.count(3)
```
### 增加串列元素
```
x.append(888)
```

### 用程式碼抓到 4 的值的下一筆資料
```
x[x.index(4)+1]
```
### insert() 方法
```
x.insert(2, 1000)
```
### del 刪除串列元素
```
del x[0]
```

```
x = [90, 80, 70]
sum(x)/len(x)
```
#### 牛刀小試:以串列計算班級成績
```
x = []
尚未結束 = True
while 尚未結束:
    y = int(input('請輸入成績:'))
    if y == -1:
        尚未結束 = False
    else:
        x.append(y)

print(f"共有{len(x)}位")
print(f"總成績{sum(x)}")
print(f"平均成績{sum(x)/len(x)}")
```
### pop() 方法
```
x1 = x.pop(0)  # 抓出第一筆資料
```
### remove() 方法
```
x.remove(90)
```
### 串列排序
```
x.sort()
```
### reverse() 反轉串列順序
```
x.reverse()
```
```
80 in x
55 in x
```

#### 牛刀小試:刪除指定串列元素
```
水果 = ['蘋果', '火龍果', '葡萄', '奇異果']
while True:
    print(水果)
    y = input('請輸入要刪除的水果:')
    if y in 水果:
        水果.remove(y)
    else:
        print(f'沒有這種水果 {y}')
```
### 元組 (Tuple)
### tuple 不能被修改
```
x = ()
type(x)

x = (1, 2, 3, 4, 5)
x[:3]
x[3:]

x[0] = 10000
```

### tuple list 互轉
```
list(x)
tuple([1, 2, 3, 4])
```

### in 功能
```
x = [1, 2, 3, 4, 5]
# [ 表達式 for 迴圈變數 in 某個list ]
[i for i in x]
[i+10 for i in x]

y = [[i, i**2] for i in x]
y[3][1]

z = [i[1] for i in y]

z1 = [i for i in z if i > 10]
```

### dictionary 定義 取值 (字典取值)
```
x = {}
type(x)

x = {1: 'apple', 2: 'banana'}
x[2]

x = {'apple': 20, 'banana': 50}
x['apple']
x.get('apple')

x['appleeeeee']
x.get('appleeeeee')

None
x.get('appleeeeee') is None  # 判斷空值
```

#### 牛刀:血型個性查詢
```
血型 = {'A': '活潑開朗',
      'B': '健康快樂',
      'C': '鬱鬱寡歡',
      'D': '熱血青年'}

使用者查詢 = input('請輸入血型:')
if 血型.get(使用者查詢) is None:
    print('沒有該血型')
else:
    print(f"血型:{使用者查詢} 個性:{血型[使用者查詢]}")

血型['A'] = '開心快樂'
血型['G'] = '健康平安'

del 血型['G']
血型.clear()
```

### 傳值
```
a = 1
b = a
b += 1
a
```
### 傳址
```
a = [1, 2, 3]
b = a  # 傳址
b.append(4)
a
b = a.copy()  # 傳值
b.append(111)

a + a
a * 3
```


```
血型 = {
    # 'key' : 'value',
    'A': '活潑開朗',
    'B': '健康快樂',
    'C': '鬱鬱寡歡',
    'D': '熱血青年'}


"A" in 血型
'G' in 血型
```

## 函式與模組 & 檔案與例外處理

```
import matplotlib
import yfinance as yf
import pandas as pd
import os
from datetime import datetime, timedelta
from random import randint
from time import sleep
import time
from random import randint as ri
import random


def myfunction():  # 定義函數
    print('print hello world!')


def myfunction2():  # 定義函數2
    return 'return hello world!'


myfunction()
myfunction2()
```

>開啟 anaconda prompt
python Python檔案完整路徑
所在路徑\檔名


```
def myfunction3(a, b):
    return a+b


myfunction3(123, 456)


def myfunction4(a, b=100):
    return a+b


myfunction4(123)
```

>有預設值的參數必須放在沒有預設值的後面
因為沒有預設值的參數 是必要參數


```
def myfunction5(b=100, a):
    return a+b
```

#### 牛刀::攝氏溫度轉華氏溫度

```
def 華氏轉攝氏(a):
    return a*1.8+32


攝氏溫度 = float(input('請輸入攝氏溫度:'))
華氏溫度 = 華氏轉攝氏(攝氏溫度)
print(f'華氏溫度:{華氏溫度}')
```
```
def 華氏轉攝氏():
    攝氏溫度 = float(input('請輸入攝氏溫度:'))
    華氏溫度 = 攝氏溫度*1.8+32
    print(f'華氏溫度:{華氏溫度}')
```
```
def 華氏轉攝氏(a):
    b = a*1.8+32
    return b

b = 100
華氏轉攝氏(30)
```
```
def 華氏轉攝氏(a):
    global b
    b = a*1.8+32
    return b


b = 100
華氏轉攝氏(30)
```

```
round(2.6)
round(2.4)
round(2.5)
round(3.5)


divmod(100, 3)
```


```
x = int(input('請輸入蘋果總數:'))
y = int(input('請輸入學生總數:'))
rs = divmod(x, y)
print(f'每個人可以分到{rs[0]}顆 剩餘{rs[1]}顆')
```


```
x = [1, 2, 3, 900, 4]
sorted(x)
sorted(x, reverse=True)
```



### 字串的合併
```
x = ['a', 'p', 'p', 'l', 'e']
y = ','.join(x)
```

### 字串的分割
```
y.split('p')
y.split(',')
```

### 讀取csv檔案
```
for i in open('D:/scores3.csv', encoding='utf-8'):
    print(i.strip().split(','))

content = [i.strip().split(',') for i in open(
    'D:/scores3.csv',
    encoding='utf-8')]
```

### 取得數學成績 (取得第3列)
```
[i[3] for i in content]
```
### 取得數學成績 (取得第3行)
```
content[2]
```

### 檢查起始或結束字串
```
a = '1,2,3,4,5,,6,7,889'
a.startswith('123')
a.startswith('1,2')

a.endswith('123')
a.endswith('889')
```


#### 牛刀:檢查網址格式
```
url = input('請輸入網址')
if url.startswith('http://'):
    print('網址正確')
else:
    print('網址錯誤')
```




#### 牛刀:設計一個函數 是將民國年分 轉換為西元年分
>例如: '109-01-01' 轉換為 '2020-01-01'
民國年 + 1911 = 西元年

```
a = '109-01-01'
b = a.split('-')
年分 = b[0]
月份 = b[1]
日期 = b[2]
西元年 = int(年分) + 1911
西元年 = str(西元年)
a1 = '-'.join([西元年, 月份, 日期])
```



```

def 轉西元(a):
    b = a.split('-')
    年分 = b[0]
    月份 = b[1]
    日期 = b[2]
    西元年 = int(年分) + 1911
    西元年 = str(西元年)
    a1 = '-'.join([西元年, 月份, 日期])
    return a1
```
```

轉西元('108-08-25')

```
### 亂數模組
```
random.randint(1, 10)

```
```
randint(1, 10)

```
```
ri(1, 10)
```
### 時間模組:time
```
time.time()  # 1970-01-01 00:00:00 迄今的秒數

start_time = time.time()
while time.time() < start_time + 3:
    print(123)
```

```
start_time = time.time()
x = 0
while time.time() < start_time + 10:
    x += 1
print(x)
```
### sleep 函式
```
sleep(2)
```


### 時間模組:datetime
>字串與時間的轉換
```
tstr = '2019-01-01 08:45'
```
>字串轉時間
```
dt = datetime.strptime(tstr, '%Y-%m-%d %H:%M')
```
>時間轉字串
```
dt.strftime('%Y/%m/%d')
```
>時間的計算

```
dt + timedelta(hours=3)
dt += timedelta(hours=3)
dt -= timedelta(days=3)
```

>將以下的字串 減去730天 並回傳字串
```
tstr = '2023-08-16 16:45'
dt = datetime.strptime(tstr, '%Y-%m-%d %H:%M')
dt -= timedelta(days=730)
dt.strftime('%Y/%m/%d')
```



>r read
w write
a append

### 寫檔案
```
file_path = 'D:/python_class/20240124_tmp.txt'
f = open(file_path, mode='w')
f.write('123,456\n')
f.close()
```

### 讀檔案
```
[i for i in open(file_path, mode='r')]
```


### 逐行寫入 1~100 到特定檔案內
```
file_path = 'D:/python_class/20240124_tmp2.txt'
f = open(file_path, mode='w')
for i in range(1, 101):
    f.write(f'{i}\n')
f.close()



file_path = 'D:/python_class/20240124_tmp3.txt'
with open(file_path, mode='w') as f:
    for i in range(1, 101):
        f.write(f'{i}\n')

print('跳出with 的區塊')
```



### 一次讀取該資料夾底下的所有 txt的文字檔內容

```
file_content = {}
fpath = 'D:/python_class/'
for file_name in os.listdir(fpath):
    if file_name[-4:] == '.txt':
        file_content[file_name] = [i for i in open(f"{fpath}/{file_name}")]
```

### 例外處理
>try⋯except 常用錯誤表
```
try:  # 該區塊的程式碼 若有錯誤 則會跳到 except 區塊
    a += 1
    # 網路連線的程式碼 放在這裡
except:
    print('例外狀況')
```
>try⋯except⋯finally 語法
```
try:  # 該區塊的程式碼 若有錯誤 則會跳到 except 區塊
    print('正常狀態')
except:
    print('例外狀況')
finally:
    print('不管如何 都會執行到的區塊')
```

```
try:  # 該區塊的程式碼 若有錯誤 則會跳到 except 區塊
    a += 1
except Exception as e:
    print(f'例外狀況:{e}')
```

```
try:
    1+'1'
except SyntaxError:
    print('語法錯誤')
except TypeError:
    print('命名錯誤')
except:
    print('未知錯誤')
```


#### 牛刀:串列初值設定
```
a1 = input('輸入數值:')
a2 = input('輸入數值:')

try:
    a3 = int(a1) + int(a2)
    print(f'加總為{a3}')
except ValueError:
    print('發生輸入非數值的錯誤')
except:
    print('發生其他錯誤')
```

## Python Pandas 應用
```
a = [[1, 2, 3], [3, 4, 5], [5, 6, 7]]
df = pd.DataFrame(a)

b = {'open': [1, 2, 3],
     'high': [4, 5, 6]}
df2 = pd.DataFrame(b)
```

### dataframe 屬性
```
df2.index
df2.columns
df2.shape
df2.dtypes
df2.ndim
```
### df2['欄位']
```
df2['open']
df2['high']
```
### loc[row 名稱, column 名稱] -> locate
```
df2.loc[1, 'high']
df2.loc[2, 'open']
```
### iloc[row index, column index ] -> int locate
```
df2.iloc[2, 1]
df2.iloc[2, 0]
```


```
pip install yfinance
import yfinance as yf
data = yf.download('0050.TW')
data.columns
data.index
data.shape
```

### 時間序列的特定資料取得方法
```
data.loc['2024']
data.loc['2023-11']
data.loc['2023-11-23']
data.loc['2023-01':'2023-04']
data.loc['2023-01':'2023-04', 'Open']
```

### 資料分析三大圖表
- 折線圖
```
data['Close'].plot()
```
- 直方圖
```
data['Close'].plot.hist()
```
- 散點圖
```
data.plot.scatter(x='Close', y='Volume')
```

### 重計 時間框架
```
data.resample('M')['Close'].ohlc()
data.resample('Y')['Close'].ohlc()

data['昨收'] = data['Close'].shift(1)
data['明收'] = data['Close'].shift(-1)
data['漲跌'] = data['Close'] - data['昨收']
```

### 依照 昨天的成交量 與 今天的漲跌 去繪製散點圖
```
data['昨量'] = data['Volume'].shift(1)
data['漲跌幅度'] = data['漲跌'].abs()
data.plot.scatter(x='昨量', y='漲跌幅度')

matplotlib.rc('font', family='Microsoft JhengHei')
```

### 計算移動平均值
```
data['20ma'] = data.rolling(20)['Close'].mean()
data['120ma'] = data.rolling(120)['Close'].mean()
data['Close'].plot()
data['20ma'].plot()
data['120ma'].plot()
```
