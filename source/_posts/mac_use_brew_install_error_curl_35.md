---
title: "mac 使用brew 安装软件报  curl: (35)"
date: 2021-10-20 15:18:24
tags: mac brew
---

mac 使用 Home brew 安装软件出现下面错误

* curl: (35) LibreSSL SSL_connect: SSL_ERROR_SYSCALL in connection to download.libsodium.org:443
  执行

```
openssl s_client -connect download.libsodium.org:443 -msg
```

然后再执行安装命令即可解决
