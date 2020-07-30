---
title: GCP-iap遠端連線
date: 2018-06-27 16:41:23
tags: GCP
categories: GCP
---

### 本文章將介紹如何用 iap 遠端

<!-- more -->

#### 1. 首先打開本機 google SDK 輸入下面指令

#### 沒有安裝 google SDK 可到[本篇文章](https://snoopy30485.github.io/2018/06/27/google-command-SDK%E5%AE%89%E8%A3%9D/)查看如何安裝

```
gcloud auth login
```

![ ](images/1.png)

#### 2. 指令輸入完會自動開啟分頁讓你選擇帳號，輸入完帳號後點選允許，出現通過驗證就是成功了

![ ](images/2.png)
![ ](images/3.png)
![ ](images/4.png)

#### 3. 輸入指令選擇專案

```
gcloud config set project [Project] ( Project 為專案 ID )

ex：gcloud config set project proven-cosine-207802
```

![ ](images/5.png)

#### 4. 輸入指令查看專案帳號是否正確

```
gcloud config list
```

![ ](images/6.png)

#### 5. 先輸入一次 iap 遠端指令，因為第一次下 alpha 指令會做 alpha 套件安裝

```
gcloud alpha compute start-iap-tunnel [instance_name] [設定的遠端 port 或 3389] --zone=asia-east1-b --local-host-port=localhost:[想要遠端的 port]

ex：gcloud alpha compute start-iap-tunnel test 3389 --zone=asia-east1-b --local-host-port=localhost:13389
```

![ ](images/7.png)

#### 會跑出安詢問，選 Y

![ ](images/8.png)

#### 跑讀條

![ ](images/9.png)

#### 跑完讀條按任意鍵結束視窗

![ ](images/10.png)

#### 6. 指令開啟防火牆，因為 iap 需要開通 35.235.240.0/20 TCP 的防火牆，開通這個防火牆代表著允許 Cloud iap 的 TCP forwarding 至連線的機器

```
gcloud compute firewall-rules create cloud-iap --direction=INGRESS --priority=1000 --network=default --action=ALLOW --rules=tcp:3389 --source-ranges=35.235.240.0/20
```

![ ](images/11.png)

#### 到 GCP 看會看到新增加一條防火牆規則，這樣就是成功了

![ ](images/12.png)

#### 7. 接下來到 GCP 導覽選單 → 安全性 → Identity-Aware Proxy，選擇 SSH 和 TCP 資源然後選擇要開啟 iap 的機器，然後右邊會出現增加權限點選新增成員

![ ](images/13.png)

#### 8. 把要新增的成員信箱打上去，角色選擇 Cloud IAP → IAP-secured Tunnel User

![ ](images/14.png)
![ ](images/15.png)
![ ](images/16.png)

#### 9. 成功後回到本機 google SDK 再輸入一次 iap 遠端指令，看到 Listening on port [你設定的遠端 port]就是成功了

```
gcloud alpha compute start-iap-tunnel [instance_name] [設定的遠端 port 或 3389] --zone=asia-east1-b --local-host-port=localhost:[想要遠端的 port]

ex：gcloud alpha compute start-iap-tunnel test 3389 --zone=asia-east1-b --local-host-port=localhost:13389
```

![ ](images/17.png)

#### 10. 接下來就可以在本機使用 { 127.0.0.1:遠端 port } 遠端了

![ ](images/18.png)

#### 11. 可以 iap 遠端後，可以把 GCP 防火牆 3389 port 停用一樣可以 iap 遠端

![ ](images/19.png)

#### 這邊附上我測試 iap 遠端的結果

#### 1. 防火牆 cloud-iap，關閉後遠端會失效

#### 2. 要遠端連線必須有安裝 google sdk 並且下指令，google sdk 關閉遠端就會失效

#### 3. google sdk 下完指令會一直在執行指令，用 ctrl+c 結束遠端會失效

#### 4. 下完指令出現 Listening on port 就代表 iap 成功，可以本機遠端在這期間不管是關閉指令、SDK、機器重開，做了以上動作造成 Listening on port 消失就都要在重複打上指令才能重新遠端

#### 5. 承4.指令還在執行只有關閉遠端，只要在遠端一次就好不用再次執行指令

#### 6. 遠端 port ( --local-host-port=localhost:port ) 可以隨意更改，只要不要用到正在用的就可以了

#### 7. 同一個專案同時有多台要遠端，只需要多開啟 google SDK 各自下指令就可以了，注意遠端 port 不能一樣 ( --local-host-port=localhost:port )

#### 8. 因為安全 3389 port 會更改掉，指令 port 就要變成更改過後的 port

#### 9. IAM 沒有加入，不能使用 iap 遠端