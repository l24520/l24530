---
title: "Ubuntu 安装php7.4"
date: 2021-10-20 15:22:04
tags: ubuntu php
---

## 先安装一下这个命令

add-apt-repository

```
apt-get install software-properties-common
```

## 添加第三方源：

```
add-apt-repository ppa:ondrej/php
apt-get update
```

## 安装php:

```
apt install php7.4
```

## 安装php编译

```
apt install php7.4-dev
```

## 安装php扩展

```
apt install php7.4-fpm php7.4-mysql php7.4-gd php7.4-mbstring
```
