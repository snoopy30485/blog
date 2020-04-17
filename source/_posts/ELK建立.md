---
title: ELK建立
date: 2018-07-26 16:13:06
tags:
---

### 本文章將介紹如何用 docker 建立 ELK

#### 新環境更新

```
sudo apt-get update
```

#### 下載 docker

```
sudo apt-get install -y docker.io
```

#### 下載 redis images 並且 docker run 起來 

```
docker run -d --name redis -p 6379:6379 -v /data/redis:/data --restart=always redis:3.2.4 redis-server --appendonly yes --maxmemory 4gb --requirepass QFkXXBZkLD6MgcEL1y8l
```

指令                 | 意義
:------------------- | :----
-d	                 | 在背景執行
--name	             | Container的名稱
-p	                 | 本機與Container對應的port
-v	                 | 本機與Container對應的資料路徑
--restart=always     |	機器重啟後Container自動重啟（預設是關閉）
redis:3.2.4	         | Redis Container的映像檔名稱與版本
redis-server         | 建立redis的server（另有redis-cli的客端版本）
--appendonly yes     | 是否做資料持久化
--maxmemory 4gb	     | 設定Redis Container 占用記憶體的最大容量
--requirepass        | 客端VM 將Log 資料傳送到Redis 時驗證用的key

