---
title: hexo博客换电脑之后配置  
date: 2017-02-08 19:37:04
tags: hexo
categories: 技术
toc: true
comments: true
---



搜了一圈，然后各种问题，最后回到原点，记录下，怕自己忘了
### NPM太慢，换淘宝cnpm

    npm install -g cnpm –registry=https://registry.npm.taobao.org

安装完成后用cnpm 代替 npm

<!--more-->
### 安装环境
1. 安装node.js
2. 安装git
3. 配置git，环境变量、账号、email、以及SSH      
     
    `git config --global user.name "yourname"`
    `git config --global user.email "your@email.com"`
    `ssh-keygen -t rsa -C "your@email.com"`
        
4. 将SSH公钥复制到GITHUB里面去

### 安装hexo

    cnpm install hexo -g

1.将原来电脑的文件夹复制到新电脑,只需复制_config.yml，theme/，source/，scaffolds/，package.json，.gitignore  
2.git bush 运行
    
    cnpm install
    
3.插件
    
    cnpm install hexo-deployer-git --save //hexo d部署到git插件
    cnpm install hexo-generator-feed --save  //RSS订阅插件
    cnpm install hexo-generator-sitemap --save //站点地图插件

### 调试
1. hexo g hexo d试一下是否成功  
    
    `hexo g`    
    `hexo d`