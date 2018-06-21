---
title: GCP-GoogleCloudPlatform-creat-vm-指令
date: 2018-06-19 15:42:47
tags:
---

# 建立GCP雲端機器 ( 指令版 )

### 1. https://cloud.google.com/

### 2. 登入Google

### 3. 點擊畫面右上角控制台 ( 主頁有各種資訊可以查看 )

![ ](images/1.png)

### 4. 在GCP控制台中，點擊右上角工具欄上的 Cloud Shell 圖標

![ ](images/2.png)

### 啟動畫面，虛擬機裝載了所有您需要的開發工具。它提供了一個持久的5GB主目錄，並在 Google Cloud 上運行。只需使用瀏覽器或 Google Chromebook 即可完成中大部分（如果不是全部的話）工作。

![ ](images/3.png)
![ ](images/4.png)

### 5. 開啟專案

```
gcloud projects create (專案ID) --name=(專案名稱) 
```

![ ](images/5.1.png)
![ ](images/6.png)

### 6. 查看帳戶跟專案

```
gcloud auth list
```

![ ](images/7.png)
```
gcloud config list project
```

![ ](images/8.png)

### 如果不是此專案可以用下面指令更換

```
gcloud config set project (專案ID)
```

![ ](images/9.png)

### 7. 建立 VM

```
gcloud compute instances create (VM名稱) --zone (區域) --image-project (project) --image (name) --tags (名稱) --custom-cpu (數字) --custom-memory (數字) --boot-disk-size (數字) --create-disk size=(數字單位),type=(硬碟類型),name=(名稱)
```

ex：gcloud compute instances create test --zone asia-east1-c --image-project ubuntu-os-cloud --image ubuntu-1604-xenial-v20180522 --tags test --custom-cpu 4 --custom-memory 8 --boot-disk-size 30 --create-disk size=10GB,type=pd-ssd,name=test-disk

![ ](images/16.png)

### 建立 VM 指令介紹：

### 創建 VM：(除了名稱跟區域不設定的值會給預設值) 沒有下區域指令會詢問是否在此區域，Did you mean zone [asia-east1-b] for instance: [test] (Y/n)? 回答 y 會直接在這個預設區域，n 會讓你選區域

```
gcloud compute instances create (name) --zone (區域)
```

### ex：gcloud compute instances create test --zone asia-east1-a

![ ](images/14.png)

### 回答 y 會直接在預設區域

![ ](images/11.png)

### 回答 n 會讓你選區域，輸入想要的區域的數字就會變成該區域了

![ ](images/12.png)
![ ](images/13.png)

### 設定 image：使用 gcloud compute images list 查詢 project 和 image 

```
gcloud compute images list
```

### 選擇需要的 project 和 name

![ ](images/10.png)

```
--image-project (project) --image (name)
```

### ex：gcloud compute instances create gcelab2 --zone us-central1-c --image-project ubuntu-os-cloud --image ubuntu-1604-xenial-v20180522

### 設定網路標記：目前防火牆要先設定好標記，防火牆指令設標記在研究

```
--tags (你設定的標記)
```

### ex： gcloud compute instances create --tags test

### 設定記憶體跟 cpu

```
--custom-cpu (數字) --custom-memory (數字)
``` 

### ex：gcloud compute instances create --custom-cpu 4 --custom-memory 8

### 設定開機硬碟容量：容量沒給單位預設是 GB

```
--boot-disk-size (數字)
```

### ex：gcloud compute instances create --boot-disk-size 30GB

### 設定開機硬碟類型：使用 gcloud compute disk-types list 查詢

```
gcloud compute disk-types list
```

![ ](images/15.png)

```
--boot-disk-type (硬碟類型)
```

### ex：gcloud compute instances create --boot-disk-type pd-ssd

### 設定開機硬碟在刪除虛擬機器的 instance 下會保留住開機硬碟，預設情況是會刪除開機硬碟

```
--no-boot-disk-auto-delete
```

### 掛其他硬碟：容量沒給單位預設是 GB

```
--create-disk name=(name),type=(硬碟類型),size=(容量)
```

### ex：gcloud compute instances create --create-disk name=test,type=pd-ssd,size=10GB