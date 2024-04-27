# SQL資料庫筆記整理
日期：2024/02/21~2024/02/23
使用平台：ubuntu 22.04.3 server
資料庫：MariaDB

# MariaDB安裝

## 查看是否有資料庫程序
```
ps -ef |grep mysql
```
## 查看伺服器埠號啟動狀況
```
netstat -aptn
```
## 更新套件庫
```
sudo apt update
```
## 安裝mariadb server
```
sudo apt install maria-server
```
## 直接登入mariadb的方法
## 透過root 直接登入 no passwd
```
sudo mariadb
```
## 給予admin帳號權限
```
GRANT ALL 
ON *.* 
TO 'admin'@'localhost'
IDENTIFIED BY '123456' 
WITH GRANT OPTION;
```
## 刷新權限
```
FLUSH PRIVILEGES;
```
## 透過admin登入資料庫
```
mysql -uadmin -p123456
```
## 顯示資料庫
```
show databases;
```
## 使用者權限
```
show grants;
```

## 1. 如何進入mysql (介紹各參數 uphP)
>h3u  > user
p  > passwd
h  > host 
P  > Port
使用者 密碼
```
mysql -uadmin -p123456 
mysql -uadmin -p123456 -h主機 -P3306
```
### D > DataBase 
```
mysql -uadmin -p123456 -D 特定資料庫
mysql -uadmin -p123456 -D mysql
```
## 2. 如何查詢內部ip 
```
mysql -uadmin -p123456 -h10.167.223.50 -P3306
mysql -uadmin -p123456 -h127.0.0.1 -P3306
```
## 3. 顯示、新增、刪除資料庫資料庫
### show 顯示 
```
show databases;
```
### create 新增
```
create database class;
```
#### drop 刪除
```
drop database class;
```
## 4. 使用資料庫 
```
mysql -uadmin -p123456 -D class
use class
```
## 新增 刪除 顯示 使用 是屬於定義語言

## 5. 建立資料表(水果 價錢類)
>create table 資料表名稱(
欄位 屬性,
欄位 屬性,
欄位 屬性,
欄位 屬性
);
### 建立新資料表
```
create table product(
	id int
);
```
### 刪除資料表
```
drop table product;
```
### 顯示所有資料表
```
show tables;
```
### 牛刀: 新增第二個價格欄位
```
drop table product;
create table product(
	id int,
	price int 
);
```
## 6. 查看資料表屬性
### describe 資料表名稱
```
describe product;
```
## 7. 輸入資料 (資料操控語言)
>INSERT INTO 資料表(欄位..) 
VALUES(值..);
```
INSERT INTO product(id) 
VALUES(1);
```
## 8. 簡單查詢資料
> select 欄位 from 資料表
```
SELECT * from product;
```
### 填寫3筆測試資料 兩個欄位都要有資料
### 練習：建立班級成績資料表
> 欄位: 座號 英文成績 國文成績 數學成績
 寫入兩筆範例資料
```
create table scroe(id int,English int,Chinese int,Math int)
```
### 寫入資料
```
insert into scroe(id int,English int,Chinese int,Math int)
values(1,80,90,88),(2,70,88,90);
```
### 寫入部分資料
```
insert into score(id,eng,chi )
values (1,70,60),(2,50,70);
```
### 寫入完整資料
```
insert into score
values (1,70,60,90),(2,50,70,100);
```
#### Column count doesn't match value count at row 1

### 空白字數不影響
```
select *         from 

score ;
```
### 字串處理

```
select jack;
select 'jack';
```
### 字串內需要單引號處理
select 'jack''s';

select * from score; # 單行註解
### 單行註解 select * from score; 

>/* 
多行註解 
多行註解 
多行註解 
*/

>select * /* 
註解: 搜尋所有欄位
*/ from score; 


#  數值型態介紹
```
create table int_test(
	i1 int,
	i2 tinyint
);
```
## 針對不同範圍去做測試
```
insert into int_test values(100,100); # o
insert into int_test values(200,200); # x
```
### 練習:去建立 tinyint smallint int bigint 的資料表 並填入該欄位的最大與最小值
```
create table int_test2(i1 tinyint,i2 smallint,i3 int,i4 bigint);
```
```
insert into int_test2
value(-128,-32768,-2147483648,-9223372036854775808);

insert into int_test2 
value(127,32767,2147483647,9223372036854775807);
```
```
select * from int_test2;
```


#  浮點位數型態介紹
```
create table float_test(f1 float,f2 double);
```
```
insert into float_test
value(1.11111111111111111111111,1.1111111111111111111111111)
```
### float(總長度,小數點位數)999999.9999
```
create table float_test2 (f1 float(10,4),f2 double);
```
```
insert into float_test2 (f1)
values(111111.1111111111111); # 小數點位數會自動篩掉 但超出範圍時會報錯
```
```
select * from float_test2 ;
```

#  字串型態介紹
>CHAR 固定儲存長度 -> CHAR(10) -> 10個字元長度的字串
'jack' -> 'jack______'

>VARCHAR 浮動儲存長度 -> VARCHAR(10) -> 最大為10個字元長度的字串
'jack' -> 'jack'
```
create table str_test(s1 char(5),s2 varchar(5));
insert into str_test value('123','45622');
```
# text 操作



# 時間型態介紹

```
create table dt_test(t1 date,t2 time);
```
```
insert into dt_test values(20240101,110330);
insert into dt_test values('20240101','110330');
insert into dt_test values('2024-01-01','11:03:30');
insert into dt_test values('2024/01/01','11:03:30');
insert into dt_test values('2024!01!01','11:03:30');
```
### datetime 欄位型態 建立一次 寫入資料
```
create table dt_test2(t1 datetime,t2 timestamp);
```
### 寫入資料
```
insert into dt_test2 (t1) values('2024-01-01','12:21');
```
### 搜尋當前時間 
```
select current_timestamp();
```
```
select * from dt_test2;
```


#  控制語言介紹
>控制語言 -> 掌管權限的語法
定義語言 
create drop alter 
操作語言
select insert delete update

>GRANT ALL PRIVILEGES 		# 給予所有權限
ON 資料庫.資料表 		# 在特定的資料庫 
TO 'myuser'@'localhost’ 	# 給特定的使用者	
IDENTIFIED BY '123456';	# 設定密碼(僅限於沒有該使用者的情況)
```
GRANT ALL PRIVILEGES
ON class.*
TO 'myuser'@'localhost'
IDENTIFIED BY '123456';
```
### 牛刀小試:
>建立一個使用者(含密碼) 
建立完整權限 
在class的product資料表
以及mysql的user資料表
```
GRANT ALL PRIVILEGES
ON class.product
TO 'andy'@'localhost'
IDENTIFIED BY '123456';
```
```
GRANT ALL PRIVILEGES
ON mysql.user;
TO 'jack'@'localhost'
```
## 並透過該使用者登入 並查看權限
```
show grants;
```
## 針對單一權限給予
```
GRANT SELECT.CREATE
ON class.product
TO 'jack2'@'localhost'
IDENTIFIED BY '123456';
```
### 練習:給予一個使用者可以建立 class 資料表的權限
```
GRANT CREATE
ON class.*
TO 'andy'@'localhost'
IDENTIFIED BY '123456';
```
## 登入
```
mysql -uandy -p123456 -D class;
```
## 新增資料表
```
create table sss(id int);
```

#  修改mariadb 的服務  #

## 搜尋特定字串 找出開放IP的設定
```
grep -r bind /etc/mysql/*
```
## 修改該設定檔 將 bind-address 改成 0.0.0.0
```
sudo vim /etc/mysql/mariadb.conf.d/50-server.cnf
```
## 修改 port
```
sudo vim /etc/mysql/mariadb.cnf
```
## 重啟 mariadb
```
sudo systemctl restart mariadb
```
## 查看 mariadb 服務是否重啟
```
netstat -aptn | grep 3306
```


#  開啟遠端伺服器用戶  #

```
GRANT ALL
ON *.* 			
TO 'peter'@'localhost' 	
IDENTIFIED BY '123456';	

GRANT ALL
ON *.* 			
TO 'peter_remote'@'%' 	
IDENTIFIED BY '123456';	
```
```
show grants for peter@localhost;
show grants for peter_remote@'%';
```
```
mysql -upeter -p123456 -h127.0.0.1
mysql -upeter_remote -p123456 -h127.0.0.1

mysql -upeter -p123456 -h10.167.223.50
mysql -upeter_remote -p123456 -h10.167.223.50
```

### 開一個帳號 給隔壁同學 讓隔壁同學試圖連線到你的伺服器
> 將port 改成 6609
```
grant all privileges
on *.* to 'cs'@'%'
identified by'123456';
```
```
mysql -ucs -p123456 -h10.167.223.46 -P6609
```

# 查看已啟用用戶
```
select * from mysql.user
select user,Host from mysql.user;
```

# 查看特定用戶的資料
```
show grants for peter@'%';'
```

# 修改root密碼 讓root可以透過一般密碼登入

```
sudo mariadb-admin -uroot password
```
# 一般使用者登入(預設是只有root系統可以直接登入)
```
mysql -uroot -p123456
mysql -uroot -p123456 -D mysql
```
# 新增、刪除、修改使用者密碼


## 新增使用者
```
caeate user jack2@'localhost'IDENTIFIED BY '123456';
```
## 更新使用者
```
alter user jack2@'localhost'IDENTIFIED BY '123456';
```
## 刪除使用者
```
drop  user jack2@'localhost'IDENTIFIED BY '123456';
```
## 取消權限
```
REVOKE all privilage
ON *.*
FROM 'jack'@'%';
```

# 取消權限


## 刪除特定權限
```
REVOKE SELECT
ON class.* 
FROM 'myuser'@'localhost' ;
```
```
show grants for 'myuser'@'localhost' ;
```
```
REVOKE INSERT, UPDATE, DELETE
ON class.* 
FROM 'myuser'@'localhost' ;
```

# 查看在線用戶

## 顯示在線用戶
show processlist;

## 刪除用戶程序
kill processID


# 非空值屬性
```
create table student(
id smallint not null,
name varchar(20) not null,
height smallint,
weight smallint
);
```
### 錯誤會出現 Field 'id' doesn't have a default value
```
insert into student(height) values(160); 
```

#  預設值屬性
```
drop table student;
create table student(
id smallint not null DEFAULT 100,
name varchar(20) not null DEFAULT 'noname',
height smallint,
weight smallint
);
```
```
insert into student(height) values(160);
```
#  唯一值屬性
```
drop table student;
create table student(
id smallint not null UNIQUE,
name varchar(20) not null DEFAULT 'noname',
height smallint,
weight smallint
);
```
```
insert into student(id,height) values(1,160);
insert into student(id,height) values(1,160);
insert into student(id,height) values(2,160);
insert into student(height) values(160);
```

#  無符號屬性  #
```
drop table student;
create table student(
id smallint not null UNIQUE,
name varchar(20) not null DEFAULT 'noname',
height tinyint unsigned,
weight tinyint
);
```
```
insert into student(id,height,weight) values(1,200,200);
insert into student(id,height,weight) values(1,200,85);
```
#  修改表格  #

```
describe student;
```
## 新增一個年齡的欄位
```
alter table student
add column age tinyint unsigned;
```
### 練1:修改年齡欄位使其預設值為25歲
```
alter table student
MODIFY column age tinyint default 25;
```
### 練2:刪除年齡欄位
```
alter table student
drop column age;
```
#### 新增一個年齡的欄位，放在第一個
```
alter table student
add column age tinyint unsigned first;
```
#  索引與主鍵  #
```
CREATE TABLE employee (
	id INT PRIMARY KEY,
	name VARCHAR(50) NOT NULL,
	age INT,
	gender ENUM('M', 'F'),
	department VARCHAR(50),
	salary DECIMAL(10, 2),
	hire_date DATE
);
```
```
describe employee;
```
```
create table employee_onboard_time(
	date date,
	time time,
	employee_id int,
	primary key(date,time)
);
```
```
describe employee_onboard_time;
```
### 寫入資料: 20240221 當天有三個員工打卡什麼情況下會有資料衝突 ?
```
insert into employee_onboard_time 
values('2024-02-22','11:35:00',1);
insert into employee_onboard_time 
values('2024-02-22','11:36:00',1);
insert into employee_onboard_time 
values('2024-02-22','11:35:00',2); # x
```

#  次要索引 INDEX  #


>建立索引的語法
CREATE INDEX 索引的名稱 
ON 資料表 (資料欄位);

## 建立索引
```
create index employee_age_idx
on employee (age);
```
## 建立索引以後 得到的顯示
```
describe employee;
```
## 在多列上建立索引
```
create index idx employee_name_salary
on employee(name,salary);
```
## 刪除索引
```
ALTER TABLE employee
DROP INDEX idx_employee_id
```

#  唯一值索引  #

>CREATE UNIQUE INDEX 索引名稱
ON 資料表 (欄位#名稱);

>練習建立唯一值索引
(建立一個職員身分證編號) id_number 
並設置為唯一值索引
```
alter table employee
drop table employee
```
## 顯示職員表格欄位
describe employee;

## 創建唯一值索引
CREATE UNIQUE INDEX idx_id_number
ON employee (id_number);

## 顯示employee的所有索引
show indexes from employee ;

#  自動索引  #

DROP TABLE employee;
CREATE TABLE employee (
id INT PRIMARY KEY AUTO_INCREMENT,
name VARCHAR(50) NOT NULL,
age INT,
gender ENUM('M','F'),
department VARCHAR(50),
salary DECIMAL(10, 2),
hire_date DATE
);

## 新增資料時不必帶上資料，就可以自動索引
INSERT INTO employee 
VALUES(null,'jack',20,'M','RD',10000,'20240222');

## 給定特定值也不會有問題 
INSERT INTO employee 
VALUES(1000,'jack',20,'M','RD',10000,'20240222');


# =========================== #
#  透過指令 將檔案匯入資料庫  #
# =========================== #

## 建立新資料sample.csv
1,2,3,4
5,6,7,8
2,4,6,8

 建立相對的資料表 
create table sample (
	i1 tinyint ,
	i2 tinyint ,
	i3 tinyint ,
	i4 tinyint 
);
## 指令匯入
mysqlimport -u root -p
--local # 本地端
--fields-terminated-by="," #欄位分割符號
--lines-terminated-by="\r\n" # 換行
資料庫名稱
匯入檔案

mysqlimport -uroot -p123456 \
--local \
--fields-terminated-by="," \
--lines-terminated-by="\n" \
class \
/home/negi/sample.csv

sudo mysql -D class

#  透過SQL 將檔案匯入資料庫  #

## 建立新資料 sample2.csv
"1","2","3","4"
"5","6","7","8"
"2","4","6","8"

## 透過SQL匯入
LOAD DATA LOCAL INFILE '/home/negi/sample2.csv'
INTO TABLE sample
FIELDS TERMINATED BY ' ,'
ENCLOSED BY '"'
LINES TERMINATED BY '\n';

LOAD DATA LOCAL INFILE '/tmp/class.bak'
INTO TABLE class
FIELDS TERMINATED BY ' ,'
ENCLOSED BY '"'
LINES TERMINATED BY '\n';

###  台灣期貨1分K資料
>日期 時間 開盤價 最高價 最低價 收盤價 成交量(0)
在不要設定索引及主鍵的情況下，匯入資料表

## scp 來源 目的 
scp \
D:\資料庫教學\future_k.csv \
jack@140.137.223.69:/tmp/

scp filename.Fileextension ssh username @ IP:目的地

scp future_k.csv ssh negi@10.167.223.46:~

## 建立資料表
create table future_k(
	date date,
	time time,
	open smallint unsigned,
	high smallint unsigned,
	low smallint unsigned,
	close smallint unsigned,
	volume tinyint
);

## 匯入資料
mysqlimport -uroot -p123456 \
--local \
--fields-terminated-by="," \
--lines-terminated-by="\r\n" \
class \
/home/negi/future_k.csv

sudo mysql -D class
## 查詢前10筆
select * from future_k limit 10;

>1. 資料正確性
>2. 占用空間
>```
>sudo ls -lh /var/lib/mysql/class/future_k.ibd
>```
>64M(省去87M  27%)
>3. 使用效率
>```
>select * 
>from future_k
>where date = '2018-01-10';
>```
>平均耗費時間 0.691 sec

### 牛刀: 將date 設定為索引 並且查看搜尋效率
#### 建立索引
CREATE INDEX date_index ON future_k (date);
#### 顯示所有索引
SHOW INDEXES FROM future_k

>索引的效率(搜尋變快了)
索引成本(硬碟容量)
64M-> 84M (多了 31%)

## 查看整個資料庫容量
sudo du -sh /var/lib/mysql/*

## 解釋查詢是否有受到特定 index 影響
explain
select * 
from future_k
where date = '2018-01-10';

## 刪除index 再次查看搜尋解釋
alter table future_k drop index date_index;


# ================================================= #
#  台灣期貨1分K資料                                 #
#  日期 時間 開盤價 最高價 最低價 收盤價 成交量(0)  #
#  在設定索主鍵的情況下，匯入資料表                 #
# ================================================= #

>設定PRIMARY KEY  資料表名稱為 future_k2
create table future_k2(
	date date,
	time time,
	open smallint unsigned,
	high smallint unsigned,
	low smallint unsigned,
	close smallint unsigned,
	volume tinyint,
	primary key (date,time)
);

### 資料改名
mv /tmp/future_k.csv /tmp/future_k2.csv

### 匯入資料
mysqlimport -uroot -p123456 \
--local \
--fields-terminated-by="," \
--lines-terminated-by="\r\n" \
class \
/home/negi/future_k2.csv

### 查看容量
64M -> 56M

### 搜尋速度
explain
select * from future_k
where date = '2018-01-10';

#  短句之間的互相配合

>INSERT INTO 資料表
VALUES (值)
可以改成以下:
INSERT INTO 資料表( 特定欄位)
SELECT 特定欄位
FROM 其他資料表
```
CREATE TABLE employee_backup (
	id INT PRIMARY KEY AUTO_INCREMENT,
	name VARCHAR(50) NOT NULL,
	age INT,
	gender ENUM('M', 'F'),
	department VARCHAR(50),
	salary DECIMAL(10, 2),
	hire_date DATE
);
```
## 將 employee 資料倒進 employee_backup
```
INSERT INTO employee_backup(
	name,age,gender,department,salary, hire_date
)
SELECT name,age,gender,department,salary, hire_date
FROM employee;
```
#  刪除資料  #

>DELETE FROM 資料表
WHERE 條件;

## 刪除所有資料
```
DELETE FROM employee_backup;
```
## 回復原廠設定
```
TRUNCATE employee_backup
```
## 刪除特定資料
```
DELETE FROM employee_backup WHERE id > 5;
```
### 練習: 刪除部門為開發部門的employee
#### 測試資料
```
INSERT INTO employee (name, age, gender, department, salary, hire_date)
VALUES ('John', 28, 'M', 'Sales', 50000.00, '2022-03-15'),
('Mary', 35, 'F', 'Marketing', 65000.00, '2022-04-01'),
('David', 42, 'M', 'Engineering', 80000.00, '2022-02-15');
```
```
DELETE FROM employee
WHERE department='Engineering';
```
#  更新資料  #

>UPDATE 資料表
SET 欄位=值[,欄位+=值]
WHERE 判斷條件）
```
UPDATE employee
SET department = 'Research'
WHERE name = 'jack';
```
```
select * from employee;
```
### 牛刀: 將年紀超過20歲的員工 薪水*1.5倍
```
UPDATE employee
SET salary = salary * 1.5
WHERE age >20 ; 
```

#  搜尋唯一的值
```
select department from employee;

select distinct department 
from employee;
```
#  欄位別名
```
select name,salary,salary*2 salary_double
from employee;

select name,salary,salary*2 as salary_double
from employee;
```
### 牛刀小試: student 表格 
>BMI 體重去除以身高(公尺)平方
80 / (1.6)*(1.6)
```
CREATE TABLE `student` (
  `age` tinyint(3) unsigned DEFAULT NULL,
  `id` smallint(6) NOT NULL,
  `name` varchar(20) NOT NULL DEFAULT 'noname',
  `height` tinyint(3) unsigned DEFAULT NULL,
  `weight` tinyint(4) DEFAULT NULL,
  UNIQUE KEY `id` (`id`)
) ;
```

# 進階邏輯指令
```
select * from student
where age in (15,20,25,27);
```
```
select * from student
where age between 25 and 35;
```
# 練習：




#  模糊搜尋  #


>where 欄位 like '表達式';
表達式 裡面 包含兩種萬用字元
% -> 0~無限個不特定字元 
_ -> 1個不特定字元


#  正則表達式
```
select * from member
where username REGEXP 'i';
```
```
select * from member
where username REGEXP '^k';
```
```
select * from member
where username REGEXP 'l$';
```
```
select * from member
where username REGEXP '^[^a-g]';
```
```
select * from member
where username REGEXP '^[^a-g]';
```

# 聚合函數
```
select AVG(salary) from employee;
```
```
select MIN(salary) from employee;
```
```
select MAX(salary) from employee;
```
```
select SUM(salary) from employee;
```

# 一般函數
```
select year(hire_date) from employee;
```
```
select concat('123','456');
```
```
select concat('name','name')
from employee;
```
```
select  year(hire_date),
	month(hire_date),
	day(hire_date)
from employee;
```
```
select NOW();
```
### DATE
```
SELECT DATEDIFF('2022-05-01', '2022-03-15')
```
# 群組化

## 群組化 -> 1.分群基準
```
select * from employee
group by department;
```

## 群組化 -> 2. 聚合函數
```
select department,avg(salary)
from employee
group by department;
```
### 練習:男與女的平均年齡
```
select gender,count(age),avg(age)
from employee
group by gender;
```

### 練習:男與女的平均薪資
```
select department,gender,count(age),avg(age)
from employee
group by department gender;
```

### 依照不同年齡層去看平均薪資(每10年為一個年齡層)
```
select floor(age/10) 年齡層,count(age) ,avg(salary) 
from employee 
group by floor(age/10);
```

### 依照不同薪資級距 去查看平均年齡
```
select floor(salary/10000) 級距,count(age) ,avg(age) 
from employee 
group by floor(salary/10000);
```

# Having

# where ->groupby -> having

# 群組年齡

# 年紀 > 30 才加入群組計算

# 期貨盤中資料
```
select dietinct time from future_k2 order by time;
```
# 08:45 ~ 13:45 日盤
# 15:00 ~ 05:00 夜盤
# 練習：統計日盤每個時間點的平均漲跌幅
```
select time,avg(abs(open-close))
from  future_k2
where time between '08:45:00' and '13:45:00'
group by time;
```

```
alter table future_k2
modify open smallint;
alter table future_k2
modify high smallint;
alter table future_k2
modify low smallint;
alter table future_k2
modify close smallint;
```

```
select department,avg(salary),group_concat(name) 
from employee 
group by department ;
```

# 外部約束


```
CREATE TABLE member (
id INT PRIMARY KEY AUTO_INCREMENT,
username VARCHAR(50) NOT NULL,
password VARCHAR(50) NOT NULL,
join_date DATE,
id_number VARCHAR(10) NOT NULL,
email VARCHAR(50) NOT NULL,
url VARCHAR(100) NOT NULL
);
```

```
INSERT INTO member (username, password, join_date, id_number, email, url)
VALUES
('john123', 'password123', '2022-01-01', 'A123456789', 'john123@gmail.com', 'https://www.example.com/john123'),
('mary456', 'password456', '2022-01-15', 'B234567890', 'mary456@gmail.com', 'https://www.example.com/mary456'),
('david789', 'password789', '2022-02-01', 'C345678901', 'david789@gmail.com', 'https://www.example.com/david789'),
('lisa111', 'password111', '2022-02-15', 'D456789012', 'lisa111@gmail.com', 'https://www.example.com/lisa111'),
('kevin222', 'password222', '2022-03-01', 'E567890123', 'kevin222@gmail.com', 'https://www.example.com/kevin222');
```
```
CREATE TABLE purchase (
id INT PRIMARY KEY AUTO_INCREMENT,
member_id INT NOT NULL, # 關連到 member id
product_name VARCHAR(50) NOT NULL,
price DECIMAL(8, 2) NOT NULL,
purchase_date DATE
);
```
```
INSERT INTO purchase (member_id, product_name, price, purchase_date)
VALUES
(1, 'T-shirt', 20.99, '2022-01-02'),
(2, 'Jeans', 39.99, '2022-01-17'),
(3, 'Sneakers', 79.99, '2022-02-03'),
(4, 'Dress', 59.99, '2022-02-18'),
(5, 'Jacket', 99.99, '2022-03-03'),
(1, 'Jeans', 29.99, '2022-03-05'),
(3, 'Dress', 89.99, '2022-03-20'),
(2, 'Handbag', 49.99, '2022-04-01');
```



# 新增不對襯的明細
 	
```
insert into purchase(member_id,product_name,price,purchase_date)
values(6,'T-shirt',21.99,'2022-01-02');
```
```
truncate purchase ;
```

# 新增外部鍵約束
```
ALTER TABLE purchase
ADD CONSTRAINT fk_member_id
FOREIGN KEY (member_id)
REFERENCES member(id);
```

`show create table purchase;`

# 子查詢

`select *from member;`
```
select member_id from purchase
where product_name = 'jacket';
```
```
select * from member
where id = (
	select member_id
	from purchase
	where product_name = 'jacket'
);
```

### 練習：找出購買牛仔褲的會員基本資料
`select * from purchase;`

select * from member
where id in = (
	select member_id
	from purchase
	where product_name = 'jeans'
);


# 交叉結合

`select * from member ,purchase ;`

```
select * 
from member ,purchase 
where member.id = purchase.member_id ;
```
```
select member.email,purchase.product_name
from member ,purchase 
where member.id = purchase.member_id ;
```


# 內部結合

## 以下兩個查詢句 功能相同
```
select m.email,p.product_name
from member m,purchase p
where m.id = p.member_id ;
```

```
SELECT m.username, p.product_name, p.price, p.purchase_date
FROM member m
INNER JOIN purchase p
ON m.id = p.member_id
```


## 外部結合
```

SELECT member.username, purchase.product_name, purchase.price
FROM member
LEFT JOIN purchase
ON member.id = purchase.member_id;
```
```

SELECT member.username, purchase.product_name, purchase.price
FROM member
INNER JOIN purchase
ON member.id = purchase.member_id;
```

### 填入一筆 會員基本資料
```
INSERT INTO member (username, password, join_date, id_number, email, url)
values
('jack123', 'password123', '2022-01-01', 
'A123456789', 'jack123@gmail.com', 
'https://www.example.com/jack123');
```




#  資料匯出 透過指令  #


>mysql
-uroot
-p123456
-D 資料庫
-e "查詢SQL"

## 透過e去外部執行SQL
```
mysql -uroot -p123456 -D class \
-e "select * from future_k2" -s
```

## sed 's /被取代的字串/取代字串/g'
```
mysql -uroot -p123456 -D class \
-e "select * from future_k2" -s | sed's/\t/,g'
```

## 導向至某個檔案
```
mysql -uroot -p123456 -D class \
 -e "select * from future_k2" -s | sed 's/\t/,/g' > /tmp/future_k.bak
```


# 資料匯出 透過SQL

```
SELECT * FROM future_k2
INTO OUTFILE '/tmp/future_k2___.bak'
FIELDS TERMINATED BY ' ,'
ENCLOSED BY ' "'
LINES TERMINATED BY '\r\n';
```

# 資料庫備份與還原


## 備份單一資料表
>mysqldump -uroot -p密碼 資料庫 資料表 [資料表] >目標檔案
`mysqldump -uroot -p123456 class employee > /tmp/class_employee.bak`

>mysql -uroot -p密碼 資料庫 < 備份檔
`mysqldump -uroot -p123456 class employee < /tmp/class_employee.bak`

`mysqldump -uroot -p123456 class > /tmp/class.bak`

```

drop database class;
create database class;
```
 
```
mysql -uroot -p123456 -D class < /tmp/class.bak;
```



#  View建立  #


### 練習將 future_k2 分成兩個View
```
create view future_day as
select * from future_k2
where time between '08:45:00 'and '13:45:00'
```

```
create view future_day as
select * from future_k2
where time between '08:45:00 'and '13:45:00'
```


#  View修改與刪除  #


`alter view future_k2`


#  View權限  #


```
CREATE USER jack_1 IBENTIFIED BY '123456';
GRANT SELECT ON future_night TO jack;
```


```
$ mysql -ujack_1 -p123456 -D class
show tables;
```


#  View 與資料表結合  #


`select member .username`



#  常規變數  #

## 設定常規變數
```
SET @myvar = 100;
select @myvar;
```

## 設定常規變數計算
```
SET @myvar = @myvar + 100;
select @myvar;
```

## 重新連線則消失
```
>將變數設定
SET @myvar = NULL
```

### 練習
>透過常規變數 去查出 'lisa111'
查詢 1
```
select id
into @a
from member
where username =@user;
```

### 查詢 2 : 透過變數a 去查詢購買紀錄
```
selecyt *
from purchase
where member_id = @a;
```


#  預存程序的建立  #


>DELIMITER //
CREATE PROCEDURE 預存程序([IN 帶入參數 型態,OUT 回傳參數 # 型態])
BEGIN
{自訂SQL語句}
END;
// DELIMITER

```
DELIMITER //
CREATE PROCEDURE getEmployeeFormDep([IN Dep varchar(50))])
BEGIN
	select *
	from employee
	where department =Dep
END;
// DELIMITER
```

## CALL 預存程序(參數);
`call getEmployeeFormDep('Marketing');`

## 建立 預存程序 有包含回傳值
```
DELIMITER //
CREATE PROCEDURE getEmployeeFormDep([IN Dep varchar(50)),OUT AvgSalary FLOAT])
BEGIN
	select avg(salary)
	INTO AvgSalary
	from employee
	where department = Dep;
END;
// DELIMITER
```

```
call getEmployeeFormDep('Marketing',@aaa)
```


# 觸發器範例  #

```
CREATE TABLE employee_operation_log (
log_id INT AUTO_INCREMENT PRIMARY KEY,
operation_type VARCHAR(10),
operation_time DATETIME,
operation_description VARCHAR(255)
);
```

```
DELIMITER //
CREATE TRIGGER employee_insert_tri
AFTER INSERT
ON employee
FOR EACH ROW
BEGIN
	insert into employee_operation_log
	values(null,'INSERT',NOW(),concat('new id',New.id))
END;
// DELIMITER
```

```
INSERT INTO employee
values(null, 'peter',23,'M','Marketing',30000,''20240223)'
```

```
DELIMITER //
CREATE TRIGGER employee_delete_tri
AFTER DELETE
ON employee
FOR EACH ROW
BEGIN
	insert into employee_operation_log
	values(null,'INSERT',NOW(),concat('old id',OLD.id))
END;
// DELIMITER
```

```
DELETE FROM employee
where name='peter';
```
