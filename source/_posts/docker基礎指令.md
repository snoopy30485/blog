---
title: docker基礎指令
date: 2018-07-02 16:13:05
tags:
---

#### 這邊列出 docker有關 Container 指令的分類，供作者自己查詢

#### create：建立 Container 並執行指令
#### run：同 create
#### kill：刪除執行中的 Container，但 Container 還是存在，只是死了。
#### rm：刪除 Container ( 停止或運行中都行 )，Container 就從這世上消失了
#### pause：暫停執行中的 Container，仍暫有記憶體停，服務不中斷
#### unpause：恢復暫停中的 Container
#### stop：停止執行中的 Container，但不暫有記憶體，服務中斷
#### start：啟動停止中的 Container
#### restart：重新啟動 Container
#### wait：讓 Container 暫停直到 Container 停止為止
#### rename：更名 Container

#### Container 的狀態
#### inspect：檢查 Container 的狀態
#### stats：查看 Container 的 CPU、記憶體及網路使用
#### port：查看 Container 的通訊埠使用
#### ps：查看 Container 使用狀態
#### top：查看 Container 在主系統中的記憶體使用
#### dip：查看 Container 的 IP
#### dpid：查看 Container 的 pid

#### Container執行時的操作
#### exec：在外部向Container內執行指令
#### exec -it contain /bin/bash
#### logs：將Container內的輸出顯示到螢幕上
#### docker logs --tail=50 container

#### Container和主系統之間的操作
#### cp：複製Container內的檔案到主系統

#### container log
#### var/lib/docker/contains/contain id

#### exec -it influxdb influxd
#### show datebase
#### show (table)

#### docker rm -f $(docker ps -aq) 刪除全部容器
#### docker rmi -f $(docker images -aq) 刪除全部 images