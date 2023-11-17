---
title: Ubuntu安装视频处理软件FFmpeg以及php使用FFmpeg
date: 2022-05-23 14:56:23
tags: FFmpeg
---

# 第一步/首先安装必要扩展

* 使用 apt install 进行安装

```
gcc
make
yasm
libsdl1.2-dev
libstl2-dev
```

# 第二步/去[FFmpeg官网](http://ffmpeg.org/)下载ffmpeg

官网地址: [http://ffmpeg.org/]([http://ffmpeg.org/]())

# 第三步/编译安装FFmpeg

```
tar -xvf ffmpeg_4.4.2.orig.tar.xz
cd ffmpeg-4.4.2
./configure
make
make install
```

# 第四步/安装完成后进行测试

```
ffmpeg -version
返回结果
ffmpeg version 4.4.2 Copyright (c) 2000-2021 the FFmpeg developers
built with gcc 9 (Ubuntu 9.3.0-17ubuntu1~20.04)
configuration:
libavutil      56. 70.100 / 56. 70.100
libavcodec     58.134.100 / 58.134.100
libavformat    58. 76.100 / 58. 76.100
libavdevice    58. 13.100 / 58. 13.100
libavfilter     7.110.100 /  7.110.100
libswscale      5.  9.100 /  5.  9.100
libswresample   3.  9.100 /  3.  9.100
```

# 使用

## 命令行使用

* FFmpeg常用命令参数

```
-c：指定编码器
-c copy：直接复制，不经过重新编码（这样比较快）
-c:v：指定视频编码器
-c:a：指定音频编码器
-i：指定输入文件
-an：去除音频流
-vn： 去除视频流
-preset：指定输出的视频质量，会影响文件的生成速度，有以下几个可用的值 ultrafast, superfast, veryfast, faster, fast, medium, slow, slower, veryslow。
-y：不经过确认，输出时直接覆盖同名文件。
```

* 查看视频元信息

```
ffmpeg -i input.mp4
```

* 分离视频音频流

```
ffmpeg -i input_file -vcodec copy -an output_file_video　　//分离视频流 
ffmpeg -i input_file -acodec copy -vn output_file_audio　　//分离音频流
```

* 视频转码

*转换编码格式（transcoding）指的是， 将视频文件从一种编码转成另一种编码。比如转成 H.264 编码，一般使用编码器libx264，所以只需指定输出文件的视频编码器即可。*

```
ffmpeg -i [input.file] -c:v libx264 output.mp4
```

* 改变分辨率

*从1080p转到480p*

```
ffmpeg -i input.mp4 -vf scale=480:-1 output.mp4
```

* 添加音轨

*添加音轨（muxing）指的是，将外部音频加入视频，比如添加背景音乐或旁白。*

```
ffmpeg -i input.aac -i input.mp4 output.mp4
```

* 获取视频截图

*-ss 01:23:45表示截取的时间戳， -vframes 1指定只截取一帧，-q:v 2表示输出的图片质量，一般是1到5之间（1 为质量最高）*

```
ffmpeg  -ss 01:23:45  -i input  -vframes 1 -q:v 2  output.jpg
```

* 为音频添加封面

```
ffmpeg -loop 1 -i cover.jpg -i input.mp3 -c:v libx264 -c:a aac -b:a 192k -shortest output.mp4
```

## 在PHP中使用

* exec形式
* 视频压缩

```
public static function reSize($path, $outPath, $toSize)
{
    $shell = "ffmpeg -i " . $path . " -strict -2  -y -fs " . $toSize . "  ". $outPath . " 2>&1";
    exec($shell, $output, $ret);
    return $ret;
}
```

* 视频截图

```
public static function screenshot($path, $outPath)
{
    $shell = "ffmpeg -i " . $path . " -ss 1 -y -frames:v 1 -q:v 1 " . $outPath . " 2>&1";
    exec($shell, $output, $ret);
    return $res;
}
```

* php-ffmpeg扩展
  
  使用composer安装php-ffmpeg扩展
  
  ```
  composer require php-ffmpeg/php-ffmpeg
  ```
* 基本使用 具体去看github的[README.md](https://github.com/PHP-FFMpeg/PHP-FFMpeg/blob/master/README.md)

```
require 'vendor/autoload.php';
$ffmpeg = FFMpeg\FFMpeg::create();
$video = $ffmpeg->open('video.mpg');
$video
    ->filters()
    ->resize(new FFMpeg\Coordinate\Dimension(320, 240))
    ->synchronize();
$video
    ->frame(FFMpeg\Coordinate\TimeCode::fromSeconds(10))
    ->save('frame.jpg');
$video
    ->save(new FFMpeg\Format\Video\X264(), 'export-x264.mp4')
    ->save(new FFMpeg\Format\Video\WMV(), 'export-wmv.wmv')
    ->save(new FFMpeg\Format\Video\WebM(), 'export-webm.webm');
```

