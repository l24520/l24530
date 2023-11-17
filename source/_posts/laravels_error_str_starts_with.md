---
title: "laravels报错str_starts_with.md"
date: 2021-10-20 15:30:03
tags: laravels php
---
laravel 使用了laravel-s胶水项目启动报错Uncaught Error: Call to undefined function Symfony\Component\Console\Input\str_starts_with()


# 问题

运行php bin/laravels start报错

```
Uncaught Error: Call to undefined function Symfony\Component\Console\Input\str_starts_with()
```

# 分析

* 问题原因 "symfony/console":4.4.27 改用php8的 str_starts_with()代替0 === strpos()写法，并在"symfony/polyfill-php80"兼容php8以下版本，通过composer autoload 会自动引入，然而定义的启动laravels 命令没有引用composer的autoload文件，导致 "symfony/polyfill-php80"的兼容文件没有加载而引起的错误

# 解决

### 方法1(不推荐)

* 降低symfony/console插件版本到"symfony/console": "4.4.26",
  很显然不现实

### 方法2（推荐）

* 在在bin/laravels中引入composer的autoload

```
include dirname(__DIR__) . '/vendor/autoload.php';
```
