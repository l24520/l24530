---
title:  "使用wc工具统计代码行数"
date: 2021-10-20 15:32:29
tags: wc 统计代码行数
---
![1634894622774.png](image/使用nvm安装控制nodejs版本/1634894622774.png)

#### 1. 统计当前目录下，php 文件数量：

```
find . -name "*.php" |wc -l
```

#### 2. 统计当前目录下，所有 php 文件行数：

```
find . -name "*.php" |xargs cat|wc -l
```

#### 3. 统计当前目录下，所有 php 文件行数，并过滤空行：

```
find . -name "*.php" |xargs cat|grep -v ^$|wc -l
```

> [*来自：https://learnku.com/articles/21338*](https://learnku.com/articles/21338 "https://learnku.com/articles/21338")
