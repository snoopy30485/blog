---
title: ELK建立-elasticsearch-logstash-kibana
date: 2018-07-26 18:01:43
tags:
---

### 本章將使用 ubuntu 16.04、elasticsearch:5.6.7、logstash:5.6.7、kibana：5.6.7 並在

### elasticsearch 版本發行說明：
### https://www.elastic.co/guide/en/elasticsearch/reference/5.6/es-release-notes.html

### logstash  版本發行說明：
### https://www.elastic.co/guide/en/logstash/current/releasenotes.html

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
sudo echo vm.max_map_count=262144 >> /etc/sysctl.conf
```

#### 配置 logstash config ( 如果先下 logstash 指令 -v 會找不到路徑下的檔案或執行失敗，所以要先配置檔案 )

```
sudo vi logstash.conf
```

#### config 內容

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

#### 下載 elasticsearch 並 run 起來

#### 參數介紹：

##### -d：背景執行

##### -v：持久化，設定容器儲存 LOG 路徑 /usr/share/elasticsearch/data 同步一份到我們指定路徑 /data/elasticsearch

##### --name：Container 命名

##### -p：設定 port號

##### --restart=always：機器重啟後 Container 自動重啟（預設是關閉）

##### --link：Container 互聯

##### ES_JAVA_OPTS="-Xms2g -Xmx2g"：設定記憶體可使用上限

```
sudo docker run -d --name es -p 9200:9200 --restart=always -v /data/elasticsearch:/usr/share/elasticsearch/data -e ES_JAVA_OPTS:-Xmx2g -e ES_JAVA_OPTS:-Xms2g elasticsearch:5.6.7
```

#### 下載 logstash 並 run 起來

#### 注意：-v 把我們設置的 config 同步到容器裡面 ( 配置 logstash.conf 放的路徑要跟 -v 的一樣本文章 config 放置路徑是在 /home/h102539/ )

```
sudo docker run -d --name logstash -p 5044:5044 --link es:elasticsearch --restart=always -v /home/h102539/logstash.conf:/usr/share/logstash/pipeline/logstash.conf -e LS_JAVA_OPTS:-Xms2g -e LS_JAVA_OPTS:-Xmx2g docker.elastic.co/logstash/logstash:5.6.7
```


#### 下載 kibana 並 run 起來

```
sudo docker run -d --name kibana --restart=always -p 80:5601 --link es:elasticsearch kibana:5.6.7
```

#### 使用指令查看容器狀態

```
docker ps -a
```

![ ](images/4.png)

#### 三、docker-compose 建立 ELK

#### 一開始指令是練習用的，等熟悉後用 docker-compose 可以快速搞定，不需要再一行行指令下

#### 安裝 docker-compose

```
apt-get -y install docker-compose
```

#### 配置 logstash config 這次配置的 config 只要跟 docker-compose 放一起就可以了

```
vi logstash.conf
```

#### conf 內容

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

#### 建立 docker-compose

```
vi docker-compose.yml
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

  logstash:
    container_name: logstash
    image: docker.elastic.co/logstash/logstash:5.6.7
    ports:
      - "5044:5044"
    restart: always
    volumes:
      - ./home/h1025139/logstash.conf:/usr/share/logstash/pipeline/logstash.conf
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

#### 使用 docker-compose 把 elk 下載並 run 起來

```
docker-compose up -d
```

#### 到這邊就建立完成了！