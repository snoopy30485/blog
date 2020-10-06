---
title: Kubernetes常用指令
date: 2020-10-06 14:45:16
tags: Kubernetes
categories: Kubernetes
---

### Kubernetes 指令筆記，持續更新

<!-- more -->

#### 取得叢集狀態

```
kubectl cluster-info
```

#### 取得設定檔

```
kubectl config view
```

#### 查詢有哪些叢集可以切換

```
kubectl config current-context
```

#### 管理多個 k8s 叢集

```
kubectl config use-context [NAME]
```

#### 建立命名空間

```
kubectl create namespace [name]
```

#### 查詢命名空間

```
kubectl get namespace
```

#### 取得資源

```
kubectl get [resources][namespace]
```

#### 查詢在 develop 命名空間 ( namespace ) 中運行的 pod

```
kubectl get pods --namespace=[name]
```

#### 查詢在 production 命名空間 ( namespace ) 中運行的 service

```
kubectl get services --namespace=[name]
```

#### 取得資源詳細內容

```
kubectl describe [resources][namespace]
```

#### 刪除資源

```
kubectl delete [resources][namespace]
```

#### 部署

```
kubectl apply -f [resources file/folder][namespace]
```

#### run 部署

```
kubectl run nginx --image=nginx
```
