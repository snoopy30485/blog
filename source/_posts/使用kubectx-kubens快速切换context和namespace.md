---
layout: kubernetes
title: 使用kubectx/kubens快速切换context和namespace
date: 2020-10-06 14:54:52
tags: Kubernetes
categories: Kubernetes
---

### 本文章將介紹使用 kubectx/kubens 快速切换 context 和 namespace

<!-- more -->

#### 安裝

```
git clone https://github.com/ahmetb/kubectx

sudo cp kubectx/kube* /usr/local/bin/
```

#### 列出全部 context

```
kubectx
```

#### 切换到指定 context

```

```

#### 在最近使用過的 2 个 context 快速切換

```
kubectx -
```

#### 列出全部 namespace

```
kubens
```

#### 切换到指定 namespace

```
kubens  [name]
```

#### 在最近使用過的 2 个 namespace 快速切换

```
kubens -
```