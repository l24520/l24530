---
title: "使用nvm安装控制nodejs版本"
date: 2021-10-21 15:33:43
tags: node nodejs nvm
---
![1634894622774.png](image/使用nvm安装控制nodejs版本/1634894622774.png)

# 安装nvm

## 两种方式

> 官网地址:https://github.com/nvm-sh/nvm#installing-and-updating

* curl安装

```
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash
```

* wget安装

```
wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash
```

如果网络环境不太好的话容易报错

`curl: (7) Failed to connect to raw.githubusercontent.com port 443: Connection refused`

![1634801839783.png](image/使用nvm安装控制nodejs版本/1634801839783.png)

解决方法直接浏览器打开

`https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh`

然后把里面的代码复制到一个install.sh文件里面 在运行一下也是可以的

# 使用nvm安装/控制nodejs版本

* 安装

```
nvm install 14
# 后面的14 就是代表所要安装的版本
```

* 切换nodejs版本

***注意:切换版本之前要先安装所要用到的版本***

```
$ nvm use 16
Now using node v16.9.1 (npm v7.21.1)
$ node -v
v16.9.1
$ nvm use 14
Now using node v14.18.0 (npm v6.14.15)
$ node -v
v14.18.0
$ nvm install 12
Now using node v12.22.6 (npm v6.14.5)
$ node -v
v12.22.6
```
