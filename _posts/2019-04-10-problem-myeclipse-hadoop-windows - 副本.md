---
layout: post
title:  hadoop使用心得随笔记
date:   2019-04-10
categories: document
tag: hadoop
---

* content
{:toc}


Windows下MyEclipse开发hadoop的一些注意点			
====================================


步骤
-------------------------------------


1）装插件，百度一大堆


2）选择hadoop文件夹的路径（直接把压缩包解压即可，作为装好插件选择的路径，注意路径不要有中文）


3）需要把hadoop.dll和winutils.exe这两个兼容性插件放在hadoop安装目录的/bin文件夹下（注意插件和系统，位数，hadoop版本要对上）

4）在Windows下进入C:\Windows\System32\drivers\etc，添加或修改hosts中的内容，把对应节点的IP，名称信息写入，为了Windows找到映射关系，很重要。
（如192.168.177.172 master
 192.168.177.167 slave1
 192.168.177.135 slave2）


5）跳到Edit Hadoop location上，Location name随意，Map/Reduce(V2)Master下的Host添主节点的名称，不是计算机名，Port填mapred-site.xml下jobtrack（jobhistory)下的端口号（如10020），DFS Master下取消勾，Host填主节点的名称，Port填core-site.xml下hadoop配置的端口号（如9000）


可能错误
------------------------


连接不上DFS时，检查Host和Port无误后，查看各自结点的IP，若是发生了变化，除了在Linux下的/hosts（具体路径忘记）修改，还得重复步骤3，把变化后的IP替换原IP