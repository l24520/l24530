---
title: "npm和yarn换淘宝源"
date: 2021-10-21 16:14:22
tags: npm yarn
---
# npm

* 临时使用

```
npm --registry https://registry.npm.taobao.org install express
```

* 持久使用

```
npm config set registry https://registry.npm.taobao.org
```

* 查看是否配置成功

```
npm config get registry
```

# yarn

* 换源

```
yarn config set registry https://registry.npm.taobao.org/
```

* 查看是否配置成功

```
yarn config get registry
```

都是淘宝源,挺好
