---
title: GCP-GoogleCloudPlatform-creat-vm-指令
date: 2018-06-19 15:42:47
tags:
---

# 建立GCP雲端機器 ( 指令版 )

#### 1. https://cloud.google.com/

#### 2. 登入Google

#### 3. 點擊畫面右上角控制台 ( 主頁有各種資訊可以查看 )

![ ](images/1.png)

#### 4. 在GCP控制台中，點擊右上角工具欄上的 Cloud Shell 圖標

![ ](images/2.png)

#### 啟動畫面

![ ](images/3.png)
![ ](images/4.png)

#### 5. 開啟專案

```
gcloud projects create 專案ID --name=專案名稱 
```

![ ](images/5.png)
![ ](images/6.png)



建立 VM 指令介紹：

查詢
gcloud compute (想要查詢的東西) list
ex：gcloud compute images list 查詢images


創建VM (不設定的值會給預設值)
gcloud compute instances create (name) --zone (區域) 
ex：gcloud compute instances create test --zone  asia-east1-c

沒有下區域指令回詢問是否在此區域，不再此區域回答y會顯示error
ex：Did you mean zone [asia-east1-b] for instance: [test] (Y/n)?


設定image (使用gcloud compute images list查詢project和image)
--image-project (project) --image (image) 
ex：gcloud compute instances create gcelab2 --zone us-central1-c --image-project ubuntu-os-cloud --image ubuntu-1604-xenial-v20180522


設定網路標記(目前防火牆要先設定好標記，防火牆指令設標記在研究)
--tags (你設定的標記)
ex： gcloud compute instances create --tags test

設定記憶體跟cpu
--custom-cpu (數字) --custom-memory (數字) 
ex：gcloud compute instances create --custom-cpu 4 --custom-memory 8

設定開機硬碟容量(不給單位預設GB)
--boot-disk-size (數字)
ex：gcloud compute instances create --boot-disk-size 30GB


設定開機硬碟類型(使用gcloud compute disk-types list查詢)
--boot-disk-type (硬碟類型)
ex：gcloud compute instances create --boot-disk-type pd-ssd


設定開機硬碟在刪除虛擬機器的instance下會保留住開機硬碟，預設情況是會刪除開機硬碟
--no-boot-disk-auto-delete


掛其他硬碟
--create-disk (name),(硬碟類型),(容量)
ex：gcloud compute instances create --create-disk name=test,type=pd-ssd,size=10GB


舉例
ex：gcloud compute instances create test --zone asia-east1-c --image-project ubuntu-os-cloud --image ubuntu-1604-xenial-v20180522 --tags test --custom-cpu 4 --custom-memory 8 --boot-disk-size 30 --create-disk size=10GB,type=pd-ssd,name=test-disk