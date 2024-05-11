# Docker

## Docker Image

- Docker 的影像（image）

    - 是唯讀的
    - 是一個可以獨立執行的輕量級套件
    - 其包含所有執行程式所需要的
        - 函式庫、環境變數與設定檔等
    - 例如一個 MySQL server 的 docker image

#### 透過 search 這個命令來搜尋 Docker Hub 中的 Image
```
$ docker search <image name>
```
#### 透過 pull 從 Docker Hub 中下載 Docker Image
```
$ docker pull <image name>
```
#### 透過 images 列出所有下載的 Docker Image
```
$ docker images
```
#### 透過 run 執行下載的 Docker Image
```
$ docker run -ti <image ID>
```
### Workshop

```
vi dockerfile
```
```
FROM python:latest

LABEL version = "1.0" Copyright = "2024" owner = "negi"

EXPOSE 5001

WORKDIR /app

ADD . /app

RUN pip3 install -r requirements.txt

CMD python3 server.py

```
```
vi server.py
```
```

from flask import Flask
app = Flask(__name__)

@app.route("/", methods = ["GET"])
def home():
        return "OK"

if __name__ == "__main__":
    app.debug = False
    app.run(host = "0.0.0.0", port = 5001)

```
```
vi requirements.txt
```
```
flask

```

#### Build Docker image:
```
$ docker build . -t image_name
```
#### List Docker image
```
$ docker images
```
#### Remove Docker image:
```
$ docker rmi (-f) <image id>
```
- 轉port
```
docker run -ti -p 5001:5001 <Docker Image ID>
```

