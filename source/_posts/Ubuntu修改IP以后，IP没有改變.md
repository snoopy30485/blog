---
title: Ubuntu修改IP以后，IP没有改變
date: 2018-06-30 06:41:16
tags:
---

### Ubuntu修改IP以后，IP没有改變

#### 本邊文章將介紹修改 ubuntu ip 和修改後沒有更改如何解決

#### 指令查看 IP

```
ifconfig -a
```

![ ](images/1.png)

#### 到 /etc/network/interfaces 文件修改 IP

```
vi /etc/network/interfaces
```

![ ](images/2.png)

#### 預設是 dhcp 自動取得

![ ](images/3.png)

#### 改成固定 IP 保存退出

![ ](images/4.png)

#### 指令重啟網卡

```
/etc/init.d/networking restart

sudo systemctl restart networking ( 2種指令都可重啟 )
```

![ ](images/5.png)

#### ifconfig -a 再次查看 IP，會發現沒有更改

![ ](images/6.png)

#### 指令刷新網卡，然後在重啟網卡一次就會發現 IP 更改過去了

```
sudo ip addr flush enp0s3 ( enp0s3 是網卡名稱 )
```

![ ](images/7.png)

#### 到這邊更改 IP 就完成了