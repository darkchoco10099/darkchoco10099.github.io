---
layout: post
title: docker运行ubuntu相关指令
tags: [docker, Linux, ubuntu]
---

docker运行ubuntu相关指令与进入

- Build 为镜像（安装包）和运行

```
编译 docker build -t test:v1 .

-t 设置镜像名字和版本号
```
命令参考：https://docs.docker.com/engine/reference/commandline/build/



- 运行 docker run -p 8080:8080 --name test-hello test:v1

```
-p 映射容器内端口到宿主机
--name 容器名字
-d 后台运行

ubuntu：
docker run --name unbuntu_fir ubuntu:20.04
```

命令参考文档：https://docs.docker.com/engine/reference/run/

- 进入ubuntu系统

```
docker exec -it ubuntu_fir /bin/bash
```

