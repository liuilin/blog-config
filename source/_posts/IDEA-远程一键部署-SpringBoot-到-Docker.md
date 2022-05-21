---
title: IDEA 远程一键部署 SpringBoot 到 Docker
date: 2022-05-20 19:16:59
tags:
---
# IDEA 远程一键部署 SpringBoot 到 Docker

### 一、开发准备

1. 安装 Docker

   [如何在 Ubuntu 20.04 上安装 Docker | Linux化](https://linuxize.com/post/how-to-install-and-use-docker-on-ubuntu-20-04/)

2. 配置开启 docker 远程连接端口

   ```bash
   # Centos
   vim /usr/lib/systemd/system/docker.service
   # Ubuntu
   vim /usr/lib/systemd/system/docker.service
   ```

   在 ExecStart 最后加上 `-H tcp://0.0.0.0:2375`

   > 如果是阿里云服务器，就在 `云服务器 ECS / 安全组` 中添加 TCP 端口 2375

3. 加载 docker 守护进程

   ```bash
   systemctl daemon-reload
   ```

4. 重启 docker

   ```bash
   systemctl restart docker
   ```

5. 测试是否开启成功

   ```bash
   curl http://localhost:2375/version
   ```

   > 或者查看端口是否打开
   >
   > ps aux | grep docker

7. 远程连接服务器 docker

   填写远程 docker 地址

   ![image-20211004205038877](https://cdn.jsdelivr.net/gh/liuilin/image-bed@latest/blog/img/image-20211004205038877.png)

   Settings - Build, Execution, Deployment - Docker：新加 Docker，并配置 TCP socket 的 Engine API URL 为 `tcp://服务器 ip:2375`

   连接成功后在 IDEA 主界面 services 的 dock 栏有新配置的 Docker 列表，双击连接后会列出远程的 docker 容器和镜像

### 二、建项目

1. 改 pom

   ```java
   <?xml version="1.0" encoding="UTF-8"?>
   <project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
            xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
     <modelVersion>4.0.0</modelVersion>
     <parent>
       <groupId>com.xkcoding</groupId>
       <artifactId>spring-boot-demo</artifactId>
       <version>1.0.0-SNAPSHOT</version>
     </parent>
     <groupId>com.liumulin</groupId>
     <artifactId>demo-docker1</artifactId>
     <version>0.0.1-SNAPSHOT</version>
     <name>demo-docker1</name>
     <description>demo-docker1</description>
   
     <properties>
       <java.version>1.8</java.version>
     </properties>
     <dependencies>
       <dependency>
         <groupId>org.springframework.boot</groupId>
         <artifactId>spring-boot-starter-web</artifactId>
       </dependency>
       <dependency>
         <groupId>org.springframework.boot</groupId>
         <artifactId>spring-boot-starter-test</artifactId>
         <scope>test</scope>
       </dependency>
     </dependencies>
   
     <build>
       <plugins>
         <plugin>
           <groupId>org.springframework.boot</groupId>
           <artifactId>spring-boot-maven-plugin</artifactId>
         </plugin>
         <plugin>
           <groupId>com.spotify</groupId>
           <artifactId>docker-maven-plugin</artifactId>
           <version>1.0.0</version>
           <configuration>
             <dockerDirectory>src/main/docker</dockerDirectory>
             <resources>
               <resource>
                 <targetPath>/</targetPath>
                 <!-- 打包到 target 目录，等于父 pom 文件的 <directory>${project.basedir}/target</directory>-->
                 <directory>${project.build.directory}</directory>
                 <!-- 等于父 pom 文件的 <finalName>${project.artifactId}-${project.version}</finalName>-->
                 <include>${project.build.finalName}.jar</include>
               </resource>
             </resources>
           </configuration>
         </plugin>
         <plugin>
           <artifactId>maven-antrun-plugin</artifactId>
           <executions>
             <execution>
               <phase>package</phase>
               <configuration>
                 <tasks>
                   <copy todir="src/main/docker"
                         file="target/${project.artifactId}-${project.version}.${project.packaging}"/>
                 </tasks>
               </configuration>
               <goals>
                 <goal>run</goal>
               </goals>
             </execution>
           </executions>
         </plugin>
       </plugins>
     </build>
   </project>
   ```

2. 在 src/main 目录下创建 docker 目录，并创建 Dockerfile 文件

   ```dockerfile
   FROM openjdk:8-jdk-alpine
   ADD *.jar app.jar
   ENTRYPOINT ["java","-Djava.security.egd=file:/dev/./urandom","-jar","/app.jar"]
   ```

3. 建 YAML

   ```yaml
   server:
     port: 9090
   logging:
     path: /docker/logs
   ```

4. 主启动类

   ```java
   package com.liumulin.demodocker1.controller;
   
   import org.springframework.web.bind.annotation.GetMapping;
   import org.springframework.web.bind.annotation.RequestMapping;
   import org.springframework.web.bind.annotation.RestController;
   
   @RestController
   @RequestMapping
   public class HelloController {
       @GetMapping("/hello")
       public String hello() {
           return "Hello,From Docker!";
       }
   }
   ```

5. 新增 Dockerfile 配置

   IDEA - Edit Configurations... 

   ![deploy Dockerfile](https://cdn.jsdelivr.net/gh/liuilin/image-bed@latest/blog/img/deploy%20Dockerfile.jpg)

   命令解释：

   Image tag：指定镜像名称和 tag，镜像名称为 docker-demo，tag 为 1.1

   Bind ports：绑定宿主机端口到容器内部端口。格式为 [宿主机端口]:[容器内部端口]

   Bind mounts：将宿主机目录挂到到容器内部目录中。格式为 [宿主机目录]:[容器内部目录]。这个 springboot 项目会将日志打印在容器 /home/developer/app/logs/ 目录下，将宿主机目录挂载到容器内部目录后，那么日志就会持久化容器外部的宿主机目录中。

6. maven 打 jar 包

   mvn clean install

7. 运行 Dockerfile

   会先 pull 基础镜像（比如 openjdk），然后再打包镜像，并将镜像部署到远程 docker 运行

   成功后可以看到镜像名为 docker-demo:1.1，容器名为 docker-server

8. 查看日志

   IDEA 的 Docker 容器可以看到 Log 输出到了控制台