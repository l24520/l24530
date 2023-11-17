---
title: Ubuntu扩展lv系统磁盘 /dev/mapper/ubuntu--vg-ubuntu--lv
date: 2021-10-27 11:35:17
tags: Ubuntu linux

---
Ubuntu虚拟机系统磁盘不够用？扩它！

使用 lvextend 工具

lvextend -L 10G /dev/mapper/ubuntu--vg-ubuntu--lv      //增大或减小至19G

lvextend -L +10G /dev/mapper/ubuntu--vg-ubuntu--lv     //增加10G

lvreduce -L -10G /dev/mapper/ubuntu--vg-ubuntu--lv     //减小10G

lvresize -l  +100%FREE /dev/mapper/ubuntu--vg-ubuntu--lv   //按百分比扩容

正常使用最后一个，将所有空闲的空间全部扩容

最后执行扩容命令

resize2fs /dev/mapper/ubuntu--vg-ubuntu--lv
