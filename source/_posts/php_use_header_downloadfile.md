---
title: "php使用header下载文件"
date: 2021-10-20 14:51:24
tags: php
---
#### 使用 header 头，实现浏览器下载文件。

```
<?php
	$file_path = 'uploads/test/1.png'
	if (!is_file($file)) {
		exit('没有文件');
	}
	header("Content-type:application/octet-stream");
	header("Content-Disposition:attachment;filename = " . basename($file_path));
	header("Accept-ranges:bytes");
	header("Accept-length:" . filesize($file_path));
	$handle = fopen($file, 'rb');
	while (!feof($handle)) {
		echo fread($handle, 102400);
	}
	fclose($handle);
	exit();
?>
```

#### 参考[php实现文件下载功能（支持中文）](https://segmentfault.com/a/1190000010912097 "php实现文件下载功能（支持中文）")
