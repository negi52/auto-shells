# Linux資料轉移規劃與執行

> 創作者：Negi
創作日期：2024/04/09
最後更新：2024/4/13
安裝環境：Linux Ubuntu_22.04.4

## 作業說明
將 A Linux 上的資料轉移至 B Linux 上
包含資料與服務
Linux帳戶資料、設定檔等
**A Linux中需包含至少2個自建不同權限的帳號
服務包含 MariaDB 、Apache 資料與設定檔
**A Linux中的MariaDB內需包含至少2個自建的DB、2個Table
除IP不同其他服務都需要正常運作
執行方式：使用 shellscript 自動化完成並驗證

## 在 A Linux 建立使用者與安裝服務

### 更新
```
sudo apt update
sudo apt upgrade
```

### 新增使用者
```
sudo adduser ann
sudo adduser andy
```

### 安裝 Apache2 & MariaDB
```
sudo apt install apache2 -y
sudo apt install mariadb-server -y
```

### 在MariaDB建立資料庫與資料表
#### 進入MariaDB
```
sudo mysql
```
#### 建立資料庫與資料表
```
CREATE DATABASE test1;
CREATE DATABASE test2;

USE test1;

CREATE TABLE t1(id INT AUTO_INCREMENT PRIMARY KEY, name VARCHAR(255));
CREATE TABLE t2(id INT AUTO_INCREMENT PRIMARY KEY, data VARCHAR(255));

INSERT INTO t1 (name) VALUES ('Alice'), ('Bob'), ('Charlie');
INSERT INTO t2 (data) VALUES ('1'), ('2'), ('3');


USE test2;

CREATE TABLE t1(id INT AUTO_INCREMENT PRIMARY KEY, name VARCHAR(255));
CREATE TABLE t2(id INT AUTO_INCREMENT PRIMARY KEY, data VARCHAR(255));

INSERT INTO t1 (name) VALUES ('David'), ('Eve'), ('Frank');
INSERT INTO t2 (data) VALUES ('Data A'), ('Data B'), ('Data C');
```
### 建立資料庫與表的結果
![image](https://hackmd.io/_uploads/S13_ZpDl0.png)

## 執行轉移
>建立 shellscript trans-l.sh

```
#!/bin/bash

# 配置
BACKUP_DIR="/home/negi"
DEST_USER="negi"
DEST_IP="10.167.223.17"
DEST_PATH="/home/negi"
SOURCE_DIR="/home/negi"
MYSQL_USER="negi"
MYSQL_PASS="123456"

# 備份
backup_all() {
    echo "開始備份"

    # 備份資料庫
    echo "備份所有資料庫.."
    mysqldump -u"$MYSQL_USER" -p"$MYSQL_PASS" --all-databases > "${BACKUP_DIR}/all_databases_backup.sql" 2>&1 && echo "資料庫備份成功" || echo "資料庫備份失敗""

    # 備份系統文件
    echo "備份系統檔案..."
    tar -czvf "${BACKUP_DIR}/system_files.tar.gz" /etc/passwd /etc/shadow /etc/group && echo "系統檔案已備份"

    # 備份使用者文件
    echo "正在備份使用者檔案..."
    cd /home
    tar --exclude="${BACKUP_DIR}" -czvf "${BACKUP_DIR}/home.tar.gz" /home && echo "已備份的主目錄檔案"

    # 同步到遠端
    echo "正在同步..."
    rsync -avz -e "ssh -i /home/negi/.ssh/id_rsa" "${SOURCE_DIR}/" "${DEST_USER}@${DEST_IP}:${DEST_PATH}" 2>&1 && echo "同步完成" || echo "同步失敗"

    echo "備份作業完成"
}

# 備份作業完成
restore_all() {
    echo "正在開始所有恢復操作..."

    # 檢查並安裝必要的軟體
    ssh -i /home/negi/.ssh/id_rsa "${DEST_USER}@${DEST_IP}" <<EOF
        echo '檢查並安裝必要的軟體...'

        #  是否有安裝Apache2
        if ! dpkg -l | grep -qw apache2; then
            sudo apt-get update -y > /dev/null &&
            sudo apt-get install apache2 -y > /dev/null && echo 'Apache2 安裝完成'
        else
            echo 'Apache2 已安裝'
        fi

        # 啟動 Apache2
        sudo systemctl start apache2 && echo 'Apache2 啟動成功' || echo 'Apache2 啟動失敗'

        # 是否有安裝 MariaDB
        if ! dpkg -l | grep -qw mariadb-server; then
            sudo apt-get install mariadb-server -y > /dev/null && echo 'MariaDB安裝完成'
        else
            echo 'MariaDB 已安裝'
        fi

        # MariaDB使用者權限
        sudo mysql -e "GRANT ALL PRIVILEGES ON *.* TO '$MYSQL_USER'@'%' IDENTIFIED BY '$MYSQL_PASS'; FLUSH PRIVILEGES;" && echo '使用者權限已設定'
EOF

    # 復原資料庫
    echo "正在恢復資料庫..."
    ssh -i /home/negi/.ssh/id_rsa "${DEST_USER}@${DEST_IP}" "mysql -u'$MYSQL_USER' -p'$MYSQL_PASS' < '${DEST_PATH}/all_databases_backup.sql'" && echo "資料庫已恢復"

    # 恢復系統文件
    echo "正在恢復系統檔案..."
    ssh -i /home/negi/.ssh/id_rsa "${DEST_USER}@${DEST_IP}" "sudo tar -xzf ${DEST_PATH}/system_files.tar.gz -C /" && echo "系統檔案已恢復"

    # 恢復使用者檔案
    echo "正在恢復使用者檔案..."
    cd /home
    ssh -i /home/negi/.ssh/id_rsa "${DEST_USER}@${DEST_IP}" "sudo tar -xzf ${DEST_PATH}/home.tar.gz -C /home" && echo "檔案已恢復"

    echo "還原操作完成"
}

# 主程式
echo "程式開始..."
backup_all
restore_all
echo "程式完成"
```

## 執行畫面
![螢幕擷取畫面 2024-04-17 161826](https://hackmd.io/_uploads/S1TCYZTxR.png)

![螢幕擷取畫面 2024-04-17 161840](https://hackmd.io/_uploads/Bk00FbTlR.png)

資料庫
![螢幕擷取畫面 2024-04-17 161758](https://hackmd.io/_uploads/H1tAK-px0.png)
使用者連線驗證
![螢幕擷取畫面 2024-04-17 161808](https://hackmd.io/_uploads/HJs0Y-6lA.png)
