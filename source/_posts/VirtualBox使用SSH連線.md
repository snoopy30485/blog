---
title: VirtualBox使用SSH連線
date: 2018-06-30 06:41:15
tags: VirtualBox
categories: VirtualBox
---

### 本篇文章將介紹如何使用 SSH 連線工具連到virtualbox linux

<!-- more -->

#### 1. 點選左上方檔案，選擇主機網路管理員

![ ](images/1.png)

#### 2. 可以看到裡面已經有一組 IP，選擇左上角建立可以新增 IP

![ ](images/2.png)
![ ](images/3.png)
![ ](images/4.png)

#### PS. 到本機 cmd 下指令 ipconfig 可以看到預設就有 virtualbox 的網卡

![ ](images/5.png)

#### 3. 選擇機器點選設定

![ ](images/6.png)

#### 4. 先在要 SSH 連線的機器下指令 ifconfig 查看 IP，可以看到 ip 是 10.0.2.15

![ ](images/9.png)

#### 5. 選擇網路打開進階選項，點選連接埠轉送

![ ](images/7.png)
![ ](images/8.png)

#### 6. 點選邊變 + 新增

![ ](images/10.png)
![ ](images/11.png)

#### 7. 輸入自己想要的主機 IP，SSH 連線 port 是 22，客體 IP 就是剛剛機器的 IP

![ ](images/12.png)

#### 8. 在來回到虛擬機器，想要使用 SSH 協定連線至 VirtualBox 中的 Ubuntu 作業系統，在這邊還需要進一步使用指令 sudo service ssh status 來查詢 SSH 服務是否有在執行的狀態，如下圖所示可以看到回傳為檔案 not-found 的訊息，也就表示說此系統還未安裝好 OpenSSH Server 的套件，那接下來需要在系統上安裝會使用到的套件

![ ](images/13.png)

#### 9. 輸入指令來安裝 OpenSSH 套件

```
sudo apt-get update
sudo apt-get install openssh-server -y
```

![ ](images/14.png)

#### 10. 下指令 sudo service ssh status 就可以查看到 SSH 服務啟動了

![ ](images/15.png)

#### 11. 最後用 SSH 連線工具測試，可以看到成功了

![ ](images/16.png)

#### SSH 協定連線至 VirtualBox 中的 Ubuntu 作業系統，到這邊就完成了