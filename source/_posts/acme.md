---
title: "使用acme自动生成https的ssl证书"
date: 2021-10-20 14:42:31
tags: acme https ssl
---

# 安装acme.sh

```
#使用root账户
su root
```

-- 对于有些网络不太好的同学来说可能需要等上一会尽管这些文件很小
-- 第一种安装方法

```
curl https://get.acme.sh | sh
```

-- 第二种安装方法

```
wget -O  -  https://get.acme.sh | SH
```

-- 第三种安装方法-直接从github克隆下来，按步骤执行三条命令

> ***这里给一个镜像站https://gitee.com/crackersw/acme.sh***

```
git clone https://github.com/Neilpang/acme.sh.git
cd ./acme.sh
./acme.sh --install
```

安装成功后会在用户的根目录下生成一个.acme.sh文件夹
要是想要查看的话使用 ``ls -a``命令查看

# 配置

我的域名在阿里云上所以我这里配置阿里云的密钥
其它配置请查看文档 [官方文档](https://github.com/acmesh-official/acme.sh/wiki/dnsapi "官方文档")

```
export Ali_Key="xxx"
export Ali_Secret="xxx"
```

这个配置只需要配置一次就可以了以后可以直接使用

# 开始生成ssl证书

```
acme.sh --issue --dns dns_ali -d 'guofurong.com.cn'
```

通过-d添加多个域名,生成后的证书在/root/.acme.sh/文件夹下有一个你域名的文件夹里面就有证书

#安装证书

```
acme.sh --installcert  -d "guofurong.com.cn"  \
--key-file /root/DockerFileForLNMP/nginx/ssl/certificateS.key \
--fullchain-file /root/DockerFileForLNMP/nginx/ssl/certificateS.pem \
--reloadcmd "dnmpr reload nginx"
```

--key-file 就是key文件的存放路
--fullchain-file 就是pem文件的存放路径

这时候去配置nginx就可以了

***Let's Encrypt 证书的有效期为三个月，acme.sh会每隔60天自动帮你续期，无需你进行任何干预***
