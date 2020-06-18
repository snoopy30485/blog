---
title: 使用docker-compose建立grafana
date: 2018-08-03 14:12:13
tags:
---

### 本文章將介紹使用 docker-compose 建立 grafana

#### 指令安裝 docker-compose

```
apt-get install -y docker-compose
```

#### 建立 docker-compose.yml

```
touch docker-compose.yml
```

#### 寫入 docker-compose 內容

```
vi docker-compose.yml
```

#### 寫入內容

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
      -e GF_AUTH_DISABLE_LOGIN_FORM=false -e GF_AUTH_GOOGLE_ENABLED=true 
      -e GF_AUTH_GOOGLE_CLIENT_ID=33574658051-0f9glecg4ujag71t3r2r6i96lc1bdgqe.apps.googleusercontent.com 
      -e GF_AUTH_GOOGLE_CLIENT_SECRET=NNDaKWcBni51U7Ya4uYL6-Ay 
      -e GF_AUTH_GOOGLE_ALLOWED_DOMAINS=gmail.com 
      -e GF_AUTH_GOOGLE_ALLOW_SIGN_UP=true
      -e GF_EXTERNAL_IMAGE_STORAGE_PROVIDER=gcs
      -e GF_EXTERNAL_IMAGE_STORAGE_GCS_KEY_FILE=/var/lib/grafana/proven-cosine-207802-ec7a854d7ba9.json
      -e GF_EXTERNAL_IMAGE_STORAGE_GCS_BUCKET=test-grafana
    networks:
      - grafana
    depends_on:
      - influxdb

networks:
  grafana:
    driver: bridge
```

#### 儲存後下指令 run docker-compose

```
docker-compose up -d
```

#### 到這邊就完成了