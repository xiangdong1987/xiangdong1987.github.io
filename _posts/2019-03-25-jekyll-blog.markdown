---
layout: post
title:  "Github免费博客空间"
date:   2019-03-26 16:39:26 +0800
categories: blog
---
本来想自己买服务器，搭建自己的博客，突然google到一种不用服务器也可以做自己博客的方式，利用github pages搭建自己的博客个人实践，完全可行。步骤如下：

### 创建代码库

* 创建一个自己的代码库blog

> * 注意下面两个设置

![设置1](/images/1.png)

![设置1](/images/2.png)

### 安装环境

* 安装ruby(已安装跳过)
* 安装jekyll
```
#安装jekyll 
gem install bundler jekyll
#新建jekyll羡慕
jekyll new my_blog
cd my_blog
#开启本地服务
bundle exec jekyll serve
```
* 我是使用vm虚拟机为了方便本地调试，利用反向代理本地服务
```
server {
    listen 80;
    server_name ytiamo.com;
    location /{
        proxy_pass http://127.0.0.1:4000;
    }
}
```
* 补充知识点可以利用参数-H 来指定主机
```
bundle exec jekyll serve -H 192.168.112.20
```

>* 注意：代码库目录和jekyll代码目录是不同目录，最后将代码库目录更新到github

### 博客撰写

* 从远端拉取自己的代码库
```
git clone https://github.com/xxxxxx/blog.git
```

### 构建部署

* 构建代码到你的到blog目录
```
jekyll build --destination ../blog/
```
* 推送代码到远端