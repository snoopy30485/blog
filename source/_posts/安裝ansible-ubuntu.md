---
title: 安裝ansible-ubuntu
date: 2019-01-03 14:29:15
tags: ansible
categories: ansible
---

### 想要用 ansible 控制另外一台 ubuntu 機器很簡單，只要安裝好 ansible 設定好 host，並且 SSH 可以連線要被控制的 ubuntu 機器就可以了

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

#### 2. 配置 ansible

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
[unubtu]
test ansible_ssh_host=127.0.0.1

或是 ( 這樣要單獨操控指令就要使用 IP )
[windows]
127.0.0.1
```

![ ](images/4.png)
![ ](images/8.png)

#### 3. 測試，如下圖就成功了接下來可以下其他指令對機器做控制

```
ansible -m ping all

ansible -m ping test ( 指定單個主機 )

ansible -m ping 127.0.0.1 ( 指定單個主機 )

ansible -m ping ubuntu ( 指定群組 )
```

![ ](images/5.png)
![ ](images/7.png)

#### 4. 下指令方式操作機器

```
ansible name -m command -a "command"

ex：ansible test -m command -a "sudo reboot"
```

#### 如下圖下完重啟指令後會發現連不到，因為重新啟動會暫時連不到表示指令操作成功

![ ](images/6.png)