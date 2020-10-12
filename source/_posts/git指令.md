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
查看系統 ssh-key 代理
ssh-add -l

# Could not open a connection to your authentication agent
系統代理沒有任何 key 執行下面指令
ssh-add ~/.ssh/id_rsa_gitee_one

如果系统已经有 ssh-key 代理，執行下面的命令可以删除
exec ssh-agent bash

添加金鑰到 ssh-agent
ssh-add ~/.ssh/金鑰

```

```
切換路徑到倉庫

git config --local user.name "Your_username"

git config --local user.email "Your_email"
```

#### git 推送

```
開分支
git branch [name]

查看分支
git branch

切換分支
git checkout [name]
```

```
檔案加入索引
git add [name]

全部檔案加入索引
git add .
```

```
變更提交到儲存庫
git commit -m "[name]"
```

```
切換分支回主線
git checkout master

合併分支
git merge 123

推送
git push -u origin master

刪除分支
git branch -D [name]
```

#### 待整理

```
git tag -a v1.4 -m 'my version 1.4'

git tag

git push origin v1.5

git checkout -b new_branch

git push -u origin new_branch
```