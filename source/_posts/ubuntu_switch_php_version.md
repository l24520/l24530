---
title: Linux切换php版本
date: 2022-11-15 10:32:33
tags: linux php
---
* ***以下只是举例说明，请自行修改相关版本***

---



### 禁用php7.4模块

```shell
sudo a2dismod php7.4
```

### 开启php8.1模块

```shell
sudo a2enmod php8.1
```

### 将8.1设置成默认版本

```shell
sudo update-alternatives --set php /usr/bin/php8.1
#或者使用以下命令实现选择默认版本
sudo update-alternatives --config php
```

### 如果有安装其它扩展可以将已经安装的扩展设置成默认

```shell
sudo update-alternatives --set phar /usr/bin/phar8.1
```

### 最后重启web服务

```shell
sudo systemctl restart apache2
```
