---
title: linux指令筆記
date: 2020-08-14 13:37:24
tags: linux
categories: linux
---

### linux 指令筆記，持續更新

<!-- more -->

#### ubuntu sudo 不用輸入密碼設定

```
sudo vi /etc/sudoers

編輯設定檔
%sudo ALL=(ALL:ALL) ALL

改成
%sudo ALL=(ALL:ALL) NOPASSWD:ALL

存檔
:wq!
```