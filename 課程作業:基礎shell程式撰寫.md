# 課程作業:基礎shell程式撰寫
>安裝與卸載 Apache、PHP模組 

## 安裝程式

```
# ubuntu_22.04.3_20240103
#!/bin/bash
# Program
# History: 2024/01/04
# :set ff=unix

# 安裝apache2
sudo apt install apache2 -y &> /dev/null && echo "Install Apache2 Complete"
# 安裝php與php套件
sudo apt install php php-common php-mysql php-gd php-cli php-fpm php-mbstring php-xml php-json -y &> /dev/null && echo "Install PHP Complete"
# 下載phpsysinfo
sudo wget https://github.com/phpsysinfo/phpsysinfo/archive/refs/tags/v3.4.3.zip -P /var/www/html/ &> /dev/null && echo "Download phpsysinfo Complete"
# 解壓縮
sudo unzip /var/www/html/v3.4.3.zip -d /var/www/html &> /dev/null && echo "Unzip Complete"
# 更名
sudo mv /var/www/html/phpsysinfo-3.4.3 /var/www/html/phpsysinfo && echo "Change phpsysinfo name"
# 複製
sudo cp /var/www/html/phpsysinfo/phpsysinfo.ini.new /var/www/html/phpsysinfo/phpsysinfo.ini &> /dev/null && echo "Copy Phpsysinfo"

echo "Complete"
```
## 卸載程式
```
# ubuntu_22.04.3_20240103
#!/bin/bash
# Program
# History: 2024/01/04


# remove phpsysinfo
sudo rm -rf /var/www/html/phpsysinfo && echo "phpsysinfo remove"

# remove zip
sudo rm -f /var/www/html/v3.4.3.zip && echo "zip remove"

# uninstall PHP
sudo apt remove php* -y &> /dev/null && echo "PHP Uninstall"

# unstall Apache2
sudo apt remove apache2 -y &> /dev/null && echo "Apache2 Uninstall"

echo "Complete"
```
