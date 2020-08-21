---
title: git指令
date: 2019-02-26 15:22:06
tags: git
categories: git
---

#### 本文章作筆記用，會持續更新 git 指令

<!-- more -->

#### 檢視目前 git 的設定

```
git config --list
```

#### 查看 git 使用者跟信箱

```
git config user.name

git config user.email
```

#### 變更 git 使用者跟信箱

#### --global 的參數，意思是要做全域（Global）的設定，也就是所以有倉庫都是吃這個設定

```
git config --global user.name "Your_username"

git config --global user.email "Your_email"
```

#### 也可以修改設定檔更換使用者跟信箱

```
cd ~/.gitconfig

[user]
  name = 
	email = 
```

#### 特定倉庫使用特定使用者

```
切換路徑到倉庫

git config --local user.name "Your_username"

git config --local user.email "Your_email"
```