---
layout: post
title:  "如何搭建本地docker registry"
date:   2019-04-03
categories: docker
---
学习k8s制作镜像就是毕竟之路，而如果想要一个快速的仓库，本地仓库就是首选，所以学习单间本地dock registry很重要。

## 获取镜像

拉取远程镜像用于制作本地镜像
```angular2html
docker pull nginx:alpine
```
## 本地docker registry
拉取docker registry 

```angular2html
docker pull registry:latest
```

运行docker registry

```angular2html
docker run \
  --detach \
  --name registry \
  --hostname registry \
  --volume $(pwd)/registry:/var/lib/registry/docker/registry \
  --publish 5000:5000 \
  --restart unless-stopped \
  registry:latest
```

## 制作镜像

* 利用DockerFile制作镜像
* 先将环境拉取到本地

```angular2html
//拉取官方php
docker pull php:7.1-cli-jessie
```
* 进入docker进行环境配置记录配置命令制作DockerFile

```angular2html
docker run -it php:7.1-cli-jessie /bin/bash
```

* [根据官方PHP镜像修改后的Dockerfile](https://github.com/xiangdong1987/local-env/tree/master)

* 容器相关命令

```angular2html
//容器属性
sudo docker inspect 6d4a2498c108 (容器id)
//容器ip
docker inspect [container_name] | grep IPAddress
//端口转发
iiptables -t nat -A DOCKER -p tcp -dport 8001 -j DNAT --to-destination 192.169.1.1:8080
//容器查看
sudo docker ps  /-a 
//删除容器
sudo docker rm 容器id
//容器镜像查看
sudo docker images 
//删除镜像
sudo docker image rm 镜像id
//运行docker -p 映射端口  -v 挂在目录  -it 进入容器
sudo docker run -p 8810:8810 -it chelun-test:v1 -v /data:/data /bin/bash

```
## 总结

镜像的制作就是一个环境搭建的流程，需要细心的记录没一部操作，也要合理话层级。尽量用少的层级来实现环境的待见。后面的路还很长需要继续学习。
