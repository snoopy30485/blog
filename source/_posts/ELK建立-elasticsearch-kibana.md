---
title: ELK建立-elasticsearch-kibana
date: 2018-07-26 16:13:20
tags:
---

### 本章將使用 ubuntu 16.04、elasticsearch:5.6.7、kibana：5.6.7

### elasticsearch 版本發行說明：
### https://www.elastic.co/guide/en/elasticsearch/reference/5.6/es-release-notes.html

### kibana 版本發行說明：
### https://www.elastic.co/guide/en/kibana/5.6/release-notes.html

***

#### 一、指令建立 ELK

#### 前置作業

#### 更新

```
sudo apt-get update
```

#### 安裝 docker

```
sudo apt-get -y install docker.io
```

#### 增加虛擬記憶體大小至少要大於 262144 KB，否則建立好的 Elasticsearch 執行會失敗

```
sudo vi /etc/sysctl.conf

sysctl -w vm.max_map_count=262144 ( 在文件最下面加進去 )
```

#### 也可以直接下這行指令幫你增加到文件裡

```
sudo su

echo vm.max_map_count=262144 >> /etc/sysctl.conf
```

#### 下載 elasticsearch 並 run 起來

#### 參數介紹：

#### -d：背景執行

#### -v：持久化，設定容器儲存 LOG 路徑 /usr/share/elasticsearch/data 同步一份到我們指定路徑 /data/elasticsearch

#### --name：Container 命名

#### -p：設定 port號

#### --restart=always：機器重啟後 Container 自動重啟（預設是關閉）

#### --link：Container 互聯

#### -e ES_JAVA_OPTS="-Xms2g -Xmx2g"：設定記憶體可使用上限

```
sudo docker run -d --name es -p 9200:9200 --restart=always -v /data/elasticsearch:/usr/share/elasticsearch/data -e ES_JAVA_OPTS:-Xmx2g -e ES_JAVA_OPTS:-Xms2g elasticsearch:5.6.7
```

#### 下載 kibana 並 run 起來

```
sudo docker run -d --name kibana --restart=always -p 80:5601 --link es:elasticsearch kibana:5.6.7
```

#### 使用指令查看容器狀態

```
sudo docker ps -a
```

![ ](images/4.png)


#### 二、使用 docker-compose 建立 ELK

#### 一開始指令是練習用的，等熟悉後用 docker-compose 可以快速搞定，不需要再一行行指令下

#### 安裝 docker-compose

```
sudo apt-get -y install docker-compose
```

#### 建立 docker-compose

```
sudo vi docker-compose.yml
```

#### docker-compose 內容

```
version: "2"

services:

  elasticsearch:
    container_name: elasticsearch
    image: elasticsearch:5.6.7
    ports:
      - "9200:9200"
    restart: always
    volumes:
      - /data/elasticsearch:/usr/share/elasticsearch/data
    environment:
      - "ES_JAVA_OPTS=-Xms2g -Xmx2g"
    networks:
      - docker_elk

  kibana:
    container_name: kibana
    image: kibana:5.6.7
    ports:
      - "80:5601"
    restart: always
    networks:
      - docker_elk
    depends_on:
      - elasticsearch

networks:
  docker_elk:
    driver: bridge
```

#### 使用 docker-compose 把 elk 下載並 run 起來

```
sudo docker-compose up -d
```

#### 到這邊就建立完成了！