---
title: grafana使用網域開啟監控頁面
date: 2018-08-02 17:59:38
tags:
---

## 本文章將介紹使用 GCP 加入 DNS 網域開啟 grafana 監控頁面

### 在 GCP 加入 DNS 網域請看本文章 [傳送們](https://snoopy30485.github.io/2018/06/20/GCP-%E8%A8%AD%E5%AE%9ADNS%E7%B6%B2%E5%9F%9F/)

### GCP 網域加好後，只需要在指令多加 -e GF_AUTH_GOOGLE_ALLOWED_DOMAINS=你的網域 這樣就可以使用網域開啟監控頁面

### grafana 指令 ( 本章使用的網域為 grafana.costworlds.com )

```
docker run -d --name grafana --restart=always -p 80:3000 -v /data/grafana:/var/lib/grafana --user root --link influxdb:influxdb -e GF_AUTH_GOOGLE_ALLOWED_DOMAINS=grafana.costworlds.com grafana/grafana:5.2.4
```

### docker-compose

```
version: "2"

services:

  influxdb:
    container_name: influxdb
    image: influxdb:1.7.2
    ports:
      - "8086:8086"
      - "8083:8083"
    restart: always
    volumes:
      - /data/influxdb:/var/lib/influxdb
    environment:
      - "ES_JAVA_OPTS=-Xms2g -Xmx2g"
    networks:
      - grafana

  grafana:
    container_name: grafana
    image: grafana/grafana:5.2.4
    user: root
    ports:
      - "80:3000"
    volumes:
      - /data/grafana:/var/lib/grafana
    restart: always
    environment:
      - GF_AUTH_GOOGLE_ALLOWED_DOMAINS=grafana.costworlds.com
    networks:
      - grafana
    depends_on:
      - influxdb

networks:
  grafana:
    driver: bridge
```
### 測試，直接使用網域開啟監控頁面，看到畫面就成功了

![ ](images/1.png)