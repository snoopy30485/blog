---
title: ELK+Redis
date: 2018-08-02 13:58:11
tags:
---

### 一、 Redis 介紹

### Redis 是 REmote DIctionary Server（ 遠程字典服務器 ）的縮寫，它以字典結構（ key-value 鍵值對結構 ）存儲數據，並允許其他應用通過 TCP 協議讀寫字典中的內容。所以，redis 是一個key-value 存儲系統，或者說是一個 key-value 數據庫，因此常常被用在需要快取一些資料的場合，可以減輕許多後端資料庫的壓力

***

### 二、 ELK + Redis ( 在 gcp 防火牆要開啟 port 6379 ) 指令 ( 前面文章有 ELK 建立，所以只上建立容器指令 )

### 一樣要先配置 logstash 文件

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
filter {
    if [type] == "wineventlog" {
        mutate {
            add_field => { 
                "hostname" => "%{[beat][hostname]}"
                "[@metadata][env]" => "%{[fields][env]]}" 
            }
            remove_field => [ "beat", "fields" ]
        }
    }
}
output {
    elasticsearch {
        hosts => ["elasticsearch"]
        index => "%{[@metadata][env]}_%{[type]}-%{+YYYY.MM.dd}"
    }
}
```

### 容器 run 起來

### Redis 參數介紹：

#### redis-server：建立redis的server（另有redis-cli的客端版本）

#### --appendonly yes：是否做資料持久化

#### --maxmemory 4gb：設定Redis Container 占用記憶體的最大容量

#### --requirepass：客端 VM 將 Log 資料傳送到 Redis 時驗證用的 key ( 跟 logstash 配置的要一樣 )

```
docker run -d --name redis -p 6379:6379 -v /data/redis:/data --restart=always redis:3.2.4 redis-server --appendonly yes --maxmemory 4gb --requirepass QFkXXBZkLD6MgcEL1y8l
```

```
docker run -d --name es -p 9200:9200 --restart=always -v /data/elasticsearch:/usr/share/elasticsearch/data -e ES_JAVA_OPTS:-Xmx6g -e ES_JAVA_OPTS:-Xms6g elasticsearch:5.6.7
```

```
docker run -d --name logstash -p 5044:5044 --link es:elasticsearch --link redis:redis --restart=always -v /logstash.conf:/usr/share/logstash/pipeline/logstash.conf -e LS_JAVA_OPTS:-Xms6g -e LS_JAVA_OPTS:-Xmx6g docker.elastic.co/logstash/logstash:5.6.7
```

```
docker run -d --name kibana --restart=always -p 80:5601 --link es:elasticsearch kibana:5.6.7
```

***

### 三、 docker-compose 建立 ( logstash 配置跟 docker-compose 同一層 )

```
version: "2"

services:

  redis:
    container_name: redis
    image: redis:3.2.4
    ports:
      - "6379:6379"
    volumes:
      - /data/redis:/data
    entrypoint: redis-server --maxmemory "1gb" --appendonly yes --requirepass QFkXXBZkLD6MgcEL1y8l
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
      - redis
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