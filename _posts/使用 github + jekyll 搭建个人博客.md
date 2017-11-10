---
layout: post
title:  "使用 github + jekyll 搭建个人博客"
date:   2017-10-13 21:41:45 +0800
categories: share
---
### 1、在windows底下配置jekyll环境
1. 安装Ruby
<br>直接官网下载安装包：https://rubyinstaller.org/downloads/
2. 安装DevKit<br>
DevKit 是一个在 Windows 上帮助简化安装及使用 Ruby C/C++ 扩展如 RDiscount 和 RedCloth 的工具箱。
- 同样前往官网安装：https://rubyinstaller.org/downloads/
- 安装完成后，创建config.yml文件,命令行输入
    ```
    $ cd "D:\DevKit"
    $ ruby dk.rb init
    ```
3. 安装jekyll
- 确保已经安装gem
    
    ```
    $ gem -v
    ```

- 安装jekyll gem<br>
Jekyll是一个静态网站生成工具。它允许用户使用HTML、Markdown或Textile来建立静态页面，然后通过模板引擎Liquid（Liquid Templating Engine）来运行.
    ```
    $ gem install jekyll
    ```
### 2、初始化博客

    ```
    $ jekyll new myblog
    $ cd myblog
    $ jekyll serve  //在本地启动服务
    ```
### 3、将代码同步到GitHub上,并在GitHub Pages上免费运行
1. 创建一个名为userName.github.io的项目（userName为你的用户名）
2. 使用Git Bash将myblog提交到userName.github.io中
- 运行jekyll serve通过浏览器本地查看没问题之后，可以提交到github了。提交之前，要创建一个.gitignore文件，编写如下内容（表示./_site文件夹及其内容无需提交到远程，因为它本地临时文件，github不需要它）
    ```
    _site/*
    ```
- 提交本地代码
    ```
    $ git init
    $ git add .
    $ git commit -m "init blog"
    $ git remote add origin https://github.com/GossipJie/GossipJie.github.io.git
    $ git push origin master
    ```
### 4、博客地址：https://gossipjie.github.io/
- 写文章规则
   1. 文章必须新建在./_post文件夹中
   1. 文章名称格式：
 
    ```
    YEAR-MONTH-DAY-title.MARKUP
    ```
   1. 设置头信息
  
    ```
    ---
    layout: post
    title: Blogging Like a Hacker
    date:   2016-07-24 21:41:45 +0800
    categories: share
    ---
    ```
