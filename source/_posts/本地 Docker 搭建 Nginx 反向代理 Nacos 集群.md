---
title: 本地 Docker 搭建 Nginx 反向代理 Nacos 集群
date: 2021-03-19 08:41:29
tags: Docker
---
# 本地 Docker 搭建 Nginx 反向代理 Nacos 集群

> Nginx 从入门到实践，万字详解！：https://mp.weixin.qq.com/s/hafErlto-1N6ypYfOVIGBQ

### 搭建 Nacos 集群

> 官网地址：https://nacos.io/zh-cn/docs/quick-start-docker.html

- Clone 项目

  ```bash
  git clone https://github.com/nacos-group/nacos-docker.git
  cd nacos-docker
  ```

- 查看目录结构

  > tree .

  ```powershell
  .
  ├── README.md
  ├── README_ZH.md
  ├── build								 # nacos 镜像制做的源码
  │   ├── Dockerfile
  │   ├── bin
  │   │   └── docker-startup.sh
  │   ├── conf
  │   │   └── application.properties
  │   └── init.d
  │       └── custom.properties
  ├── changlog
  ├── env									 # docker compose 环境变量
  │   ├── mysql.env
  │   ├── nacos-embedded.env
  │   ├── nacos-hostname.env
  │   ├── nacos-ip.env
  │   └── nacos-standlone-mysql.env
  └── example								 # docker compose 编排文件
      ├── cluster-embedded.yaml
      ├── cluster-hostname.yaml
      ├── cluster-ip.yaml
      ├── init.d
      │   └── custom.properties
      ├── prometheus
      │   ├── prometheus-cluster.yaml
      │   └── prometheus-standalone.yaml		
      ├── standalone-derby.yaml
      ├── standalone-mysql-5.7.yaml
      └── standalone-mysql-8.yaml
  ```- 单机模式 Derby```
  docker-compose -f example/standalone-derby.yaml up
  ```

- 单机模式 MySQL

  如果希望使用 MySQL5.7

  ```docker-compose -f example/standalone-mysql-5.7.yaml up```

  如果希望使用 MySQL8

  ```docker-compose -f example/standalone-mysql-8.yaml up```

- 集群模式

  ```powershell
  docker-compose -f example/cluster-hostname.yaml up
  ```

> 若启动后连接不上 mysql ，需要将配置自动生成的 volumes 卷轴文件夹删除（volumes: - ./mysql:/var/lib/mysql）

启动：

``` powershell
$: docker run --name my-nginx -p 8888:80 -v "$PWD/html":/user/share/nginx/html  -v "$PWD/conf":/etc/nginx -d nginx
```

> PWD：当前目录

自定义配置 nginx.cong 中的 server_name www.linlin.com 配置到 hosts 中 120.0.0.1 www.linlin.com

访问浏览器：www.linlin.com:8888/nacos

> 配置好 Nginx 反向代理后，若出现无法访问，列出以下几种情况：
>
> 1. 404 检查负载均衡到对应的端口没，我的情况是从 git 拉下来的 Nacos 配置代码里端口映射的有了 "9555:9555" ，但 ngnix.conf 里的 upstream 中没有配置该端口，所以负载均衡到 9555 端口出现 404
> 2. 在配置 hosts 之前提前访问了 www.linlin.com ，此时未走 127.0.0.1 页面出现 462，再次访问时会走浏览器缓存。反复都会页面 462，所以需要重新配置 server_name 或者强制清除缓存
