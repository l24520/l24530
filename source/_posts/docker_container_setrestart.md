---
title: "docker为已有容器设置自动重启"
date: 2021-10-20 15:25:16
tags:
---
* 有时候启动容器的时候忘记给容器加自动重启的命令 可以使用docker update 命令来更新


```
docker update --restart=always 容器ID(或者容器名)
```
