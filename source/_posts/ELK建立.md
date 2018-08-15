---
title: ELK建立
date: 2018-07-26 16:13:20
tags:
---

## 本章將使用 ubuntu 16.04、elasticsearch:5.6.7、logstash:5.6.7、kibana：5.6.7 並在 GCP 建立

## elasticsearch 版本發行說明：
## https://www.elastic.co/guide/en/elasticsearch/reference/5.6/es-release-notes.html

## logstash  版本發行說明：
## https://www.elastic.co/guide/en/logstash/current/releasenotes.html

## kibana 版本發行說明：
## https://www.elastic.co/guide/en/kibana/5.6/release-notes.html

***

### 一、在 GCP 建立一台機器

### VM 設定：名稱、區域、記憶體、CPU、開機磁碟

![ ](images/1.png)

### 網路：記得設定網路標記，外部 IP 設定成固定 IP

![ ](images/2.png)

### 防火牆設：目標代碼 ( 跟 VM 網路標記一樣 )、IP、通訊埠

### 埠號：Elasticsearch tcp:9200、logstash tcp:5044、Kibana tcp:80;tcp:5601、SSH tcp:22

![ ](images/3.png)

***

### 二、進入 VM 指令建立 ELK

### 前置作業

### 最高權限進入

```
sudo su
```

### 取得遠端更新伺服器的套件檔案清單

```
apt-get update
```

### 更新套件

```
apt-get -y dist-upgrade
```

### 安裝 docker

```
apt-get -y install docker.io
```

### 增加虛擬記憶體大小至少要大於 262144 KB，否則建立好的 Elasticsearch 執行會失敗

```
vi /etc/sysctl.conf
sysctl -w vm.max_map_count=262144 ( 在文件最下面加進去 )
```

### 也可以直接下這行指令幫你增加到文件裡

```
echo vm.max_map_count=262144 >> /etc/sysctl.conf
```

### 配置 logstash config ( 如果先下 logstash 指令 -v 會找不到路徑下的檔案或執行失敗，所以要先配置檔案 )

```
vi logstash.conf
```

### config 內容

```
input {
  beats {
    port => 5044
  }
}

output {
  elasticsearch {
    hosts => [ "elasticsearch:9200" ]
    manage_template => false
    index => "%{[@metadata][beat]}-%{[@metadata][version]}-%{+YYYY.MM.dd}"
    document_type => "%{[@metadata][type]}"
  }

}
```

### 下載 elasticsearch 並 run 起來

### 參數介紹：

#### -d：背景執行

#### -v：持久化，設定容器儲存 LOG 路徑 /usr/share/elasticsearch/data 同步一份到我們指定路徑 /data/elasticsearch

#### --name：Container 命名

#### -p：設定 port號

#### --restart=always：機器重啟後 Container 自動重啟（預設是關閉）

#### --link：Container 互聯

#### ES_JAVA_OPTS="-Xms6g -Xmx6g"：設定記憶體可使用上限

```
docker run -d --name es -p 9200:9200 --restart=always -v /data/elasticsearch:/usr/share/elasticsearch/data -e ES_JAVA_OPTS:-Xmx6g -e ES_JAVA_OPTS:-Xms6g elasticsearch:5.6.7
```

### 下載 logstash 並 run 起來

### 參數介紹：

### -v：把我們設置的 config 同步到容器裡面 ( 配置 logstash.conf 放的路徑要跟 -v 的一樣 )

```
docker run -d --name logstash -p 5044:5044 --link es:elasticsearch --restart=always -v /logstash.conf:/usr/share/logstash/pipeline/logstash.conf -e LS_JAVA_OPTS:-Xms6g -e LS_JAVA_OPTS:-Xmx6g docker.elastic.co/logstash/logstash:5.6.7
```


### 下載 kibana 並 run 起來

```
docker run -d --name kibana --restart=always -p 80:5601 --link es:elasticsearch kibana:5.6.7
```

### 使用指令查看容器狀態

```
docker ps -a
```

![ ](images/4.png)

### 恭喜 ELK 建立完成

***

### 三、進入 VM docker-compose 建立 ELK

### 一開始指令是練習用的，等熟悉後用 docker-compose 可以快速搞定，不需要再一行行指令下

### 安裝 docker-compose

```
apt-get -y install docker-compose
```

### 建立 docker-compose

```
vi docker-compose.yml
```

### docker-compose 內容

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

  logstash:
    container_name: logstash
    image: docker.elastic.co/logstash/logstash:5.6.7
    ports:
      - "5044:5044"
    restart: always
    volumes:
      - ./logstash.conf:/usr/share/logstash/pipeline/logstash.conf
    networks:
      - docker_elk
    depends_on:
      - elasticsearch

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

### 使用 docker-compose 把 elk 下載並 run 起來

```
docker-compose up -d
```

### 配置 logstash config 這次配置的 config 只要跟 docker-compose 放一起就可以了

```
vi logstash.conf
```

### conf 內容

```
input {
  beats {
    port => 5044
  }
}

output {
  elasticsearch {
    hosts => [ "elasticsearch:9200" ]
    manage_template => false
    index => "%{[@metadata][beat]}-%{[@metadata][version]}-%{+YYYY.MM.dd}"
    document_type => "%{[@metadata][type]}"
  }

}
```
### 到這邊 ELK 就建立完成了！