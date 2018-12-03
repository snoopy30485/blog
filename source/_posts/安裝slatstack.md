---
title: 安裝slatstack
date: 2018-11-30 13:43:24
tags:
---

### 什麼是 saltstack？

#### SaltStack 是一種新的基礎設施管理方法開發軟件，簡單易部署，可伸縮的足以管理成千上萬的服務器，和足夠快的速度控制。SaltStack 提供了一個動態基礎設施通信總線用於編排,遠程執行、配置管理等等。

#### saltstack 有三種架構，本文章先介紹第一種架構 master → minion 這種架構中 master 和所有 minion 都直接連接，minion 接收來自 master 的指令，完成命令執行或配置管理，如下圖所示

![ ](images/1.png)

#### 安裝 saltstack master 本文章使用 ubuntu 16.04 來安裝

#### 安裝指令

```
apt-get -y install salt-master
```
![ ](images/2.png)

#### 接下來安裝