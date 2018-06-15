---
title: GCP-GoogleCloudPlatform VM 建立
date: 2018-06-15 18:04:28
tags:
---
# 建立GCP雲端機器
#### <p>1. [連結到 Google Cloud Platform](https://cloud.google.com/?utm_source=google&utm_medium=cpc&utm_campaign=japac-TW-all-en-dr-bkws-all-super-trial-e-dr-1002234&utm_content=text-ad-none-none-DEV_c-CRE_205812821243-ADGP_BKWS%20%7C%20EXA%20~%20T1%20-%20General_M:1_TW_EN_cloud-googlecloud-KWID_43700018487811535-kwd-35920686936&userloc_9040380&utm_term=KW_googlecloud&gclid=CNnCzIrBg9UCFVgFKgod99wNLQ&dclid=COnE9orBg9UCFcUulgodL5kHxg "Google Cloud Platform")</p>
#### <p>2. 登入Google</p>
#### <p>3. 點擊畫面右上角控制台</p>
![](images/1.png)
***
#### 4. 選取或建立新機構（ 專案 )
![](images/2.jpg)
#### 進入專案畫面

![...](images/5.png)

***
#### 5. 選取專案
![](images/3.png)
***
#### 6. 點選資訊主頁畫面左上方的工具列
![](images/22.png)

***
#### 7. 點選工具列清單 → Compute Engine → VM 執行個體 ( 可點選圖釘把自己常用的工具釘選到最上面 )
![](images/4.png)
#### 點選建立執行個體，建立 VM
![](images/6.png)
***
#### 8. 輸入名稱（ 名稱必須為小寫字母、數字或連字號，且結尾須為小寫字母或數字 ）、選擇區域與機器類型
![](images/7.png)
#### 預設是 google 給的便宜方案，也可以自己調整
![](images/8.png)
#### 點選變更選擇作業系統，及開機磁碟容量及類型
![](images/9.png)
![](images/10.jpg)
***
#### 9. 依需求變更身分及 API 存取權與防火牆
![](images/11.jpg)
***
#### 10. 設定管理、磁碟、網路、SSH 金鑰
![](images/12.jpg)
#### 設定管理頁籤內容 
![](images/13.jpg)
#### 點選 ＋新增項目後點選建立磁碟建立第二磁碟
![](images/14.jpg)
![](images/15.png)
![](images/16.png)
#### 在網路介面下點選編輯，預設 ip 是臨時可以改成靜態 ip 才不會下次無法進入 VM
![](images/17.jpg)
![](images/18.jpg)
#### 設定 SSH 金鑰 
![](images/19.jpg)
***
#### 11. 設定完後右上拉開會顯示每個月多少金額
![](images/21.png)
***
#### 12. 再次確認步驟 8 至步驟 11 的內容是否正確，確認無誤後點選建立
![](images/20.jpg)
# 完成 GCP 雲端機器建立