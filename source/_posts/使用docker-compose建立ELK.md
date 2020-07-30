---
title: 使用docker-compose建立ELK
date: 2018-07-26 16:13:08
tags: ELK
categories: ELK
---

### 本文章將介紹使用 docker-compose 建立 ELK

<!-- more -->

#### 指令安裝 docker-compose

```
apt-get install -y docker-compose
```

#### 建立 logstash 資料夾並進入

```
mkdir logstash

cd logstash
```

#### 建立資料夾 conf.d 裡面放入 logstash config 跟 logstash filter config

```
mkdir conf.d

cd conf.d

vi logstash.conf

vi serverlog.conf
```

#### logstash.conf

```
input {
    redis {
        host => "redis"
        port => 6379
        data_type => "list"
        key => "vplaylog"
        password => "QFkXXBZkLD6MgcEL1y8l"
    }
}
output {
    elasticsearch {
        hosts => ["elasticsearch"]
        index => "%{[@metadata][env]}_%{[type]}-%{+YYYY.MM.dd}"
    }
}
```

#### serverlog.conf

```
filter {
    if [type] == "serverlog" {
        grok {
            match => ["message", "%{TIMESTAMP_ISO8601:[@metadata][timestamp]} %{NUMBER:threadid} %{LOGLEVEL:loglevel} %{NOTSPACE:logger} %{GREEDYDATA:message}"]
            overwrite => [ "message" ]
        }

        date {
            match => [ "[@metadata][timestamp]", "YYYY-MM-dd HH:mm:ss.SSS" ]
            timezone => "UTC"
        }

        mutate {
            convert => {
                "threadid" => "integer"
            }
            add_field => { 
                "hostname" => "%{[beat][hostname]}"
                "servertype" => "%{[fields][servertype]]}"
                "[@metadata][env]" => "%{[fields][env]]}"
            }
            remove_field => ["beat", "fields"]
        }
    }
}
```

#### 回到上一層建立 Dockerfile 

```
cd ..

vi Dockerfile
```

#### Dockerfile

```
FROM  logstash:5.6.7
COPY conf.d /home/ben.yu/logstash/conf.d
CMD ["-f", "/home/ben.yu/logstash/conf.d"]

```

#### 建立 docker-compose.yml

```
mkdir docker-compose.yml
```

#### 寫入 docker-compose 內容

```
vi docker-compose.yml
```

#### 寫入內容

```
version: '2'

services:

  redis:
    container_name: redis
    image: redis:3.2.4
    ports:
      - "6379:6379"
    volumes:
      - /data/redis:/data
    entrypoint: redis-server --maxmemory "4gb" --appendonly yes --requirepass QFkXXBZkLD6MgcEL1y8l
    restart: always
    networks:
      - docker_elk

  elasticsearch:
    container_name: elasticsearch
    image: elasticsearch:5.6.7
    ports:
      - "9200:9200"
    restart: always
    volumes:
      - /data/elasticsearch:/usr/share/elasticsearch/data
    environment:
      ES_JAVA_OPTS: "-Xms2g -Xmx2g"
    networks:
      - docker_elk

  logstash:
    build: logstash/
    container_name: logstash
    ports:
      - "5044:5044"
    environment:
      LS_JAVA_OPTS: "-Xmx2g -Xms2g"
    restart: always
    networks:
      - docker_elk
    depends_on:
      - elasticsearch
      - redis

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

#### 儲存後下指令 run docker-compose

```
docker-compose up -d
```

#### 到這邊就完成了