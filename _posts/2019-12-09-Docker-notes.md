---
layout: post
title:  "Docker notes 2 - Using Dockerfile to build own image"
date:   2019-12-09 11:11:18 +0800
categories: tutorial
---

![Picture](/images/2019/001.jpg "Picture")

## 1. Create a file called “Dockerfile”, the content like below

    FROM python:3.7

    COPY . /app
    WORKDIR /app

    RUN pip install -r requirements.txt

    CMD ["python", "src/main.py"]

## 2.Build commends

    docker build -t woffee/nlp:test .

Then you can use cmd `docker images` to see your result.

## 3.Upload it to Docker hub

    docker push woffee/nlp:nvidia

## PS: other cmd list

    docker run                # 此命令具有自动pull image 文件的功能
    docker kill [containID]   # 终止不会自动停止的容器
    docker rm [containerID]   # 删除容器文件（终止运行的容器文件，依然会占据硬盘空间）
    docker run --rm           # rm参数可在容器终止运行后自动删除容器文件
