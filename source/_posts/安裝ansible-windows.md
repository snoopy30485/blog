---
title: 安裝ansible-windows
date: 2019-01-03 14:29:23
tags:
---

### 本章將介紹使用 ubuntu-ansible 連線控制 windows，但是 windows 是沒有 ssh 連線的，所以會需要用到 pywinrm

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
```

![ ](images/5.png)
![ ](images/6.png)

#### 4. 新增群組資料夾，windows 連線會需要輸入遠短帳密，因此我們在 ansible 下建立 group_vars 輸入遠端需要設定

```
mkdir /etc/ansible/group_vars

vi /etc/ansible/group_vars/windows.yml

ansible_user: 遠端帳號
ansible_password: 遠端密碼
ansible_port: 5986
ansible_connection: winrm
ansible_winrm_server_cert_validation: ignore
```

![ ](images/7.png)

#### 5. windows 開啟 powershell 設定，本文章是使用 windows server 2016 Datacenter 不用下列步驟可以跳第 5 步驟

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

#### 6. 製作 powershell 腳本

#### ConfigureRemotingForAnsible.ps1 檔案內容：https://goo.gl/t5BWTN

#### 7. 對 winrm service 進行基礎配置

```
winrm quickconfig

如果已經啟動設定會需要用指令修改
```

![ ](images/18.png)

```
將winrm service 配置auth

winrm set winrm/config/service/auth ‘@{Basic="true"}‘
```

![ ](images/8.png)

```
將winrm service配置加密方式為允許非加密

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
ansible -m ping all

ansible -m ping test ( 指定單個主機 )
```

```
執行命令
ansible name -m command -a "command"

ex：ansible windows -m win_command -a "shutdown -s -t 10" ( 遠端操作關機指令 )
```

![ ](images/11.png)
![ ](images/12.png)
![ ](images/13.png)