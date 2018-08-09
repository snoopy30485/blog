---
title: elasticsearch-log刪除
date: 2018-08-01 14:22:59
tags:
---

### elasticsearch log 刪除

### 手動刪除指令

### 要按照你 logstash.conf 設定格式才能刪除，\* 是全部刪除如下例子 2018.\* 就是 2018 的 log 全刪除

```
curl -XDELETE 'http://127.0.0.1:9200/( log格式 )'

ex：curl -XDELETE 'http://127.0.0.1:9200/winlogbeat-6.2.2-2018.01.15'

ex：curl -XDELETE 'http://127.0.0.1:9200/winlogbeat-6.2.2-2018.*'
```

***

### 自動刪除

### 我們將使用 linux 的 shell script 製作腳本，並用排程來達到自動化刪除 log

### 1. 建立腳本

```
vi (名字隨意).sh

ex：vi test.sh
```

### 腳本內容

```
#!/bin/bash

function delete_indices() {
    comp_date=`date -d "30 day ago" +"%Y-%m-%d"`
    date1="$1 00:00:00"
    date2="$comp_date 00:00:00"

    t1=`date -d "$date1" +%s`
    t2=`date -d "$date2" +%s`

    if [ $t1 -le $t2 ]; then
        echo "$1時間早於$comp_date，進行索引刪除"
        format_date=`echo $1| sed 's/-/\./g'`
        curl -XDELETE http://localhost:9200/*$format_date
    fi
}

curl -XGET http://localhost:9200/_cat/indices | awk -F" " '{print $3}' | awk -F"-" '{print $NF}' | egrep "[0-9]*\.[0-9]*\.[0-9]*" | sort | uniq  | sed 's/\./-/g' | while read LINE
do
    delete_indices $LINE
done
```

### 2. 給腳本權限

```
chmod +x test.sh
```

### 3. 啟動測試

```
./test.sh
```

### 輸出畫面

![ ](images/1.png)

### 4. 設定排程

```
vi /etc/crontabe
```

### 進入裡面設置排程

![ ](images/2.png)

```
0  12  *  *  *  root   /home/h1025139/test.sh

分  時  日  月  時  使用者  指令
```

### 代表意義：分鐘 0-59，小時 0-23，日期 1-31，月份 1-12，周 0-7

### 補充：\* 代表任何時刻都接受的意思， 上圖 \*/1 是每分鐘一次