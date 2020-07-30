---
title: 安裝ansible-windows
date: 2019-01-03 14:29:23
tags: ansible
categories: ansible
---

### 本章將介紹使用 ubuntu-ansible 連線控制 windows，但是 windows 是沒有 ssh 連線的，所以會需要用到 pywinrm

<!-- more -->

#### 1. 安裝 ansible

```
將 PPA 添加到系統中，中間需要案 Enter 接受 PPA 增加

sudo apt-add-repository ppa:ansible/ansible
```

![ ](images/1.png)
![ ](images/2.png)

```
更新並安裝

sudo apt-get update

sudo apt-get install -y ansible
```

![ ](images/3.png)

#### 2. 安裝 pywinrm

```
安裝 pywinrm 模組

sudo apt-get install -y python-pip

pip install pywinrm
```

![ ](images/4.png)

#### 3. 配置 ansible

#### Ansible 通過 hosts 文件知道所有服務器，我們需要先設置此文件，然後才能開始與我們的其他機器連線

```
host 文件路徑
/etc/ansible/hosts

更改指令
sudo vi /etc/ansible/hosts

更改內容
[隨意群組名稱]
隨意名稱 ansible_ssh_host=要連線機器 ip

ex：
[windows]
test ansible_ssh_host=127.0.0.1

或是 ( 這樣要單獨操控指令就要使用 IP )
[windows]
127.0.0.1
```

![ ](images/6.png)
![ ](images/12.png)

#### 4. 新增群組資料夾，windows 連線會需要輸入遠端帳密，因此我們在 ansible 下建立 group_vars 輸入遠端需要設定

#### PS.檔案名稱要跟群組一樣，才會讀取到 YMAL 檔的內容

```
sudo mkdir /etc/ansible/group_vars

sudo vi /etc/ansible/group_vars/windows.yml

ansible_user: 遠端帳號
ansible_password: 遠端密碼
ansible_port: 5986
ansible_connection: winrm
ansible_winrm_server_cert_validation: ignore
```

![ ](images/5.png)
![ ](images/7.png)

#### 5. 製作 powershell 腳本，本文章是使用 windows server 2016 Datacenter

#### 桌面右鍵 → 新增 → 文件資料夾

![ ](images/19.png)

#### 隨意資料夾右上箭頭 → 點選分頁檢視 → 副檔名打勾，這樣就看的到檔案副檔名

![ ](images/20.png)
![ ](images/21.png)
![ ](images/22.png)

#### 命名 ConfigureRemotingForAnsible.ps1 貼上網址內容，檔案內容：https://goo.gl/t5BWTN

#### 貼上內容後更改檔名 .ps1

![ ](images/23.png)

#### 6. windows 開啟 powershell 設定，本文章是使用 windows server 2016 Datacenter 不用下列步驟可以跳第 7 步驟

#### 開啟 powershell，左下搜尋 → 輸入 powershell → 右鍵以系統管理員身分執行

![ ](images/24.png)

```
安裝 .NET Framework 4.5
```

```
更改 powershell 策略為 remotesigned 輸入 y 確認

Set-ExecutionPolicy remotesigned

檢查策略

Get-ExecutionPolicy

```

![ ](images/15.png)

```
查看版本（ 須為3.0以上 ）

$PSVersionTable.PSVersion
```

![ ](images/16.png)

```
開啟 Winrm service

winrm enumerate winrm/config/listener

如果沒有回應，表示該服務沒有啟動，預設是不啟動的
```

![ ](images/17.png)

#### 7. 對 winrm service 進行基礎配置

```
winrm quickconfig

如果已經啟動設定會需要用指令修改
```

![ ](images/18.png)

```
winrm service 配置 auth

winrm set winrm/config/service/auth ‘@{Basic="true"}‘
```

![ ](images/8.png)

```
winrm service 配置加密方式為允許非加密

winrm set winrm/config/service ‘@{AllowUnencrypted="true"}‘
```

![ ](images/9.png)

```
在放置 ConfigureRemotingForAnsible.ps1 路徑下執行配置 winrm 與 https 證書訊息

powershell.exe -File ConfigureRemotingForAnsible.ps1
```

![ ](images/10.png)

```
檢查 config 內容

winrm get winrm/config
```

![ ](images/14.png)

#### 8. 測試，如下圖就成功了接下來可以下其他指令對機器做控制

```
ansible all -m win_ping

ansible test -m win_ping ( 指定單個主機 )

ansible 127.0.0.1 -m win_ping ( 指定單個主機 )

ansible windows -m win_ping ( 指定群組 )
```

![ ](images/11.png)
![ ](images/13.png)

#### 9. 下指令方式操作機器

```
ansible name -m win_command -a "command"

ex：ansible windows -m win_command -a "shutdown -r -t 10" ( 遠端操作重啟指令 )
```