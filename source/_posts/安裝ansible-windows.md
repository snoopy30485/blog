---
title: 安裝ansible-windows
date: 2019-01-03 14:29:23
tags:
---

### 本章將介紹使用 ubuntu-ansible 連線控制 windows，但是 windows 是沒有 ssh 連線的所以會需要用到 pywinrm

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

#### 新增群組資料夾

```
mkdir /etc/ansible/group_vars

vi /etc/ansible/group_vars/windows.yml

ansible_user: 遠端帳號
ansible_password: 遠端密碼
ansible_port: 5986
ansible_connection: winrm
ansible_winrm_server_cert_validation: ignore
```

![ ](images/5.png)
![ ](images/6.png)
![ ](images/7.png)

#### 4. windows 開啟 powershell 設定，本文章是使用 windows server 2016 R2 不用下列步驟可以跳第 5 步驟

```
安裝 .NET Framework 4.5

更改powershell 策略為 remotesigned

查看版本（ 須為3.0以上 ）
$PSVersionTable.PSVersion

開啟 Winrm service
winrm enumerate winrm/config/listener
如果沒有回應，表示該服務沒有啟動，預設是不啟動的
```

#### 5. 對 winrm service 進行基礎配置

```
winrm quickconfig

查看 winrm service listener
winrm e winrm/config/listener

將winrm service 配置auth
winrm set winrm/config/service/auth ‘@{Basic="true"}‘

將winrm service配置加密方式為允許非加密
winrm set winrm/config/service ‘@{AllowUnencrypted="true"}‘

在cmd 執行 powershell.exe -File ConfigureRemotingForAnsible.ps1
配置winrm 與https證書訊息
檔案內容：https://snoopy30485.github.io/2019/01/03/%E9%85%8D%E7%BD%AEwinrm%E8%88%87https%E8%AD%89%E6%9B%B8%E8%A8%8A%E6%81%AF/
```

![ ](images/14.png)
![ ](images/8.png)
![ ](images/9.png)
![ ](images/10.png)

#### 10. 測試，如下圖就成功了接下來可以下其他指令對機器做控制

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