---
title: about git
date: 2017-02-14 15:08:16
tags: git
categories: 技术
---
## 一个新手的折腾之路

### git搭建。

最近心血来潮，想搭建一个github page 博客，然后各种google 。。。嗯，其实我用的baidu。。。

1. 下载安装Git ...  
windows 下面用msysgit(自己百度)就好啦。
linux 嘛直接命令行安装，以ubuntu为例：
> sudo apt-get install git
<!--more-->
2. 配置git
打开git bush:
> git config --global user.name "Your Name"  
> git config --global user.email "email@example.com"

3. 开始使用  
> git init  
> git checkout -b dev   # 创建dev分支，并切换到dev  
> git remote add origin git@github.com/yourname/youname.github.io.git  
> git add .  
> git commit -m "你想说啥就说啥，本次提交的注释"  
> git push origin -u dev # 提交到远程仓库的dev分支  

4. 大坑

 - 各种问题的解决办法（菜鸟总是想方设法偷懒而不是翻教程，嗯，就酱！）,适用远端已有仓库的情况  
> git clone https://github.com/yourname.git Blog # 从github 克隆库到本地Blog 文件夹  

然后就可以愉快的：  
> git add .  
> git commit -m "你想说啥就说啥，本次提交的注释"  
> git push origin -u dev # 提交到远程仓库的dev分支  

 - 把需提交的东西拷贝到Blog文件夹，如果是hexo部署，有第三方主题的，将第三方主题里面的.git文件夹，.gitignore删除，然后再提交

### 部署到 coding 和github
参考：
> http://www.jianshu.com/p/7ad9d3cd4d6e

### travis CI 持续集成
  
   参考：  
> https://segmentfault.com/a/1190000005622331  
> http://blog.csdn.net/woblog/article/details/51319364

 - 加密时候请在**linux**下进行，windows有各种坑等你跳！

不想再敲字啦，我就是懒，你来打我啊！

