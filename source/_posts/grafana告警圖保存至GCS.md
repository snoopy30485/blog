---
title: grafana告警圖保存至GCS
date: 2018-08-03 14:12:12
tags:
---

## 本文章將介紹將 grafana 告警圖片上傳到 gcs

### 一、進入 gcp 然後到導覽選單 storage → 瀏覽器

![ ](images/1.png)

### 二、點選建立 bucket

![ ](images/2.png)

### 三、為值區命名，點擊繼續

![ ](images/3.png)

### 四、選擇儲存空間級別，本文章使用 regional 每個級別 gcp 都有解釋，請依個人需求做選擇

![ ](images/4.png)

### 五、選擇控制物件的存取權，選擇設定物件層級和值區層級權限

![ ](images/5.png)

### 六、進階設定預設，全部選好後點選建立

![ ](images/6.png)

### 七、回到瀏覽器畫面可以看到設定好的 bucket，接下來點選生命週期下的無設定生命週期

### 因為 grafana 告警圖片並不是需要長久保存的資料，因此我們設定生命週期定期刪除資料，不要讓圖片越存越多

![ ](images/7.png)

### 八、點擊新增規則

![ ](images/8.png)

### 九、設定物件選取條件和選取動作，本文章選擇30天刪除，請依個人需求選擇

![ ](images/9.png)

### 兩個條件都點選繼續後就可以儲存了

![ ](images/10.png)

### 回到 bucket 可以看到生命週期已啟用

![ ](images/11.png)

### 十、接下來到 iam 與管理員 → 服務帳戶

![ ](images/12.png)

### 十一、點選建立服務帳號

![ ](images/13.png)

### 十二、輸入服務帳戶名稱

![ ](images/14.png)

### 十三、選擇角色

![ ](images/15.png)

### 角色選擇 儲存空間 → storage 物件建立者

![ ](images/16.png)

### 十四、點選 create key 下載金鑰

![ ](images/17.png)

### 選擇 josn 檔，點選建立後就會自動幫你下載了

![ ](images/18.png)

### 回到服務帳戶可以看到已建立好的服務帳戶

![ ](images/19.png)

### 十五、接下來回到 grafana vm 把下載的 josn 檔案放到 vm 的路徑 /data/grafana 底下，因有將實體機器資料夾指向 container 路徑，所以放此路徑底下

![ ](images/20.png)

### 十六、增加 grafana GCP 存放告警圖片環境參數

### GF_EXTERNAL_IMAGE_STORAGE_PROVIDER=gcs

### GF_EXTERNAL_IMAGE_STORAGE_GCS_KEY_FILE=/var/lib/grafana/服務帳戶金鑰 JOSN檔名稱+.josn

### GF_EXTERNAL_IMAGE_STORAGE_GCS_BUCKET=服務帳戶名稱

### 本文章使用指令

```
docker run -d --name grafana --user root -p 80:3000 -v /data/grafana:/var/lib/grafana --link influxdb:influxdb --restart=always -e GF_SERVER_ROOT_URL=http://grafana.costworlds.com -e GF_AUTH_DISABLE_LOGIN_FORM=false -e GF_AUTH_GOOGLE_ENABLED=true -e GF_AUTH_GOOGLE_CLIENT_ID=33574658051-0f9glecg4ujag71t3r2r6i96lc1bdgqe.apps.googleusercontent.com -e GF_AUTH_GOOGLE_CLIENT_SECRET=NNDaKWcBni51U7Ya4uYL6-Ay -e GF_AUTH_GOOGLE_ALLOWED_DOMAINS=gmail.com -e GF_AUTH_GOOGLE_ALLOW_SIGN_UP=true -e GF_EXTERNAL_IMAGE_STORAGE_PROVIDER=gcs -e GF_EXTERNAL_IMAGE_STORAGE_GCS_KEY_FILE=/var/lib/grafana/proven-cosine-207802-ec7a854d7ba9.json -e GF_EXTERNAL_IMAGE_STORAGE_GCS_BUCKET=test-grafana  grafana/grafana:5.2.4
```

### 十七、查看

### container log 指令

```
docker logs (Container ID)
```

![ ](images/21.png)

### 十八、接下來回到 grafana 監控頁面測試告警

![ ](images/22.png)

### 看到告警圖片就是成功了