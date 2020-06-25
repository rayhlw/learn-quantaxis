# Docker

Docker 基础使用教程
macOS 使用Homebrew进行安装，命令行如下：
berw cask install docker


# Docker 简明原理

- Docker关系逻辑：(  电脑  (  sandbox  (  app  )  )  )
    - app --> 你的程序 / 你的环境
    - sandbox --> docker runtime 可以无缝的在任何系统上进行整体迁移

- 当有多个app需要在一个场景下被拉起的时候：场景 --> 模拟盘
    - 写策略的容器 / 运行策略的容器
    - 可视化的容器
    - 一个可以模拟账户 / 接收订单 / 处理交易的程序
    - MongoDB 数据库
    - MessageQueue 跨进程的消息传递
    - 需要一个行情接收 / 转发的程序

- Docker-compose
    - 基于一个固定的场景，组合你所需要的容器
    - 给多个容器一个虚拟的网卡，方便容器之间相互通信

- Docker基础命令
    - docker-compose pull               更新这个场景下的所有的容器
    - docker-compose ps                 查看所有容器的运行状态
    - docker-compose up                 拉起来（重启）所有的容器
    - docker-compose up -d              后台重新启动服务
    - docker images                     列出本地主机上的镜像
    - docker stop $(docker ps -a -q)    停止所有容器
    - docker stop $(docker ps -a -q)    删除所有容器

- 服务端口(localhost:)
    - 27017     mongodb 数据库
    - 8888      jupyter 代码编辑器
    - 8010      quantaxis_webserver 后端服务
    - 81        quantaxis_community 社区版界面
    - 61208     系统监控
    - 15672     qa-eventmq