---
title: google-SDK基礎指令
date: 2020-07-31 09:31:29
tags: GCP
categories: GCP
---

### google command SDK 基礎指令筆記，持續更新

<!-- more -->


#### 新增一個新的 SDK 設定檔

```
gcloud init
```

#### 登入帳戶

```
gcloud auth login
```

#### 列出目前所有在 sdk 中的設定檔

``` 
gcloud config configurations list
```

#### 查看目前設定檔資訊

```
gcloud config list
```

#### 更換設定檔

```
gcloud config configurations activate [config name]
```

#### 刪除設定檔

```
glcoud config configurations delete [config name]
```

#### 設定地區

```
gcloud config set compute/zone asia-east1-b
```

#### 設定區域

```
gcloud config set compute/zone asia-east1
```