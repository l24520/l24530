---
title: "docker-machine /docker toolbox 换源"
date: 2021-10-20 15:23:48
tags: docker docker-machine
---

## 使用 ``docker-machine ssh xxx ``进入虚拟机

```
docker-machine ssh [machine-name]
```

## 编辑boot2docker配置

```
sudo vi /var/lib/boot2docker/profile
```

在--label provider=virtualbox下面加一行

```
--registry-mirror=https://xxxxxxxx.mirror.aliyuncs.com
```

## 重启docker服务

```
sudo /etc/init.d/docker restart
```

* 或者

```
docker-machine restart [machine-name]
```
