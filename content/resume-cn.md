---
title: "简历"
date: 2018-04-10
---

### 基本信息

* 男 27 岁
* 北京工业大学 计算机科学与技术 本科

### 技能

* 四年Go经验
* 熟悉Docker
* 熟悉Kubernetes
* 熟悉EFK

### 工作经历
- 才云科技
    - 后端工程师 2017.08 至今
    - 基于K8S的EFK Stack (Elasticsearch + Fluentd + Kibana)

- 探探科技
    - 高级后端开发工程师 2016.03 - 2017.04（1年1个月）
    - 项目：[探探](https://tantanapp.com)
    - 描述：社交APP
    - 职责：后端开发
    - 主要工作：
        - 反作弊的解决方案及后端实现
        - 媒体云服务的调优和高可用
        - 推送服务的调优
        - 代码架构的调整和优化
        - 开发环境的容器化

- 云栈科技
    - 后端开发工程师 2015.05 - 2016.02（9个月）
    - 项目：[cSphere](https://csphere.cn/)
    - 描述：Docker私有云集群管理工具
    - 职责：后端开发
    - 主要工作：
        - 利用Git的Webhook，实现Docker镜像自动构建并Push至私有Registry
        - 实现基于Docker Swarm的自定制Docker Compose
        - 基于Prometheus，实现容器与主机监控报警功能
        - 项目日志审计功能的设计与开发
        - 负责代码审查与合并

- 暖暖游戏
    - 后端开发工程师 2014.07 - 2015.04（9个月）
    - 项目：[奇迹暖暖](https://qjnn.qq.com/)
    - 描述：基于HTTP的短链接游戏服务器
    - 职责：后端开发及运维
    - 主要工作：
        - 应用服务器架构设计
        - 服务器端业务逻辑开发
        - 使用python进行项目发布与开发测试脚本的编写
        - 担任Git Admin
        - 负责压力测试

### 部分项目简介
- EFK
    - 封装ES的DSL，提供Restful查询API
    - 维护EFK
    - 参与开源项目 [elastic/beats](https://github.com/elastic/beats/search?q=walktall&type=Issues&utf8=%E2%9C%93)
    - 日志事件监控，基于 [percolate query](https://www.elastic.co/guide/en/elasticsearch/reference/current/query-dsl-percolate-query.html)

- 探探反作弊
    - 设计并实现客户端请求合法性验证方式
    - 根据Spammers行为建立规则并实现规则
    - 设计并实现用于分析用户注册事件的服务
    - 一些技术细节：
        - 由于旧代码路由无法容易地添加中间件，所以使用[mux](https://github.com/gorilla/mux)重构了路由代码
        - 用户注册事件服务采用了一种[新的包依赖解决方案](https://medium.com/@benbjohnson/standard-package-layout-7cdbc8391fc1#.t402ijwu4)

- 探探媒体云服务
    - 问题：探探有两个对象存储服务用于存储用户上传的媒体文件，然而其中一个当机则用户上传就会直接失败
    - 解决：改为只要有存储服务存活，就不会使上传失败，方法是记录下文件ID，在当机服务恢复时重新上传
    - 其他：
        - 限制用户上传视频长度
        - 编写媒体云机器所需要的RPM Spec及Dockerfile
    - 一些技术细节：
        - [boltdb](https://github.com/boltdb/bolt)用于记录文件ID
        - 实现[circuit breaker](https://martinfowler.com/bliki/CircuitBreaker.html)用于判断对象存储服务存活与否

- 探探推送服务
    - 问题：推送缓慢，图表显示推送量下降
    - 使用[Go-torch](https://github.com/uber/go-torch)定位性能问题
    - 发现的问题：
        - 推送服务打的日志太长导致syslog服务截断日志，日志被打到随机的位置使syslog服务器上硬盘性能下降，导致日志丢失，而图表的数据源是日志所以会显示推送量下降
        - 日志太长且数据结构复杂，导致fmt的时候反射过多性能下降
    - 解决方案：
        - 限制推送日志长度
        - 增大推送并发数

- cSphere自定制Compose
    - 参考[libcompose](https://github.com/docker/libcompose)部分代码实现基于cSphere平台的compose功能
    - 一些技术细节：
        - Docker API的调用
        - 利用mongodb存储信息

- 暖暖架构设计
    - 背景：
        - 小服模式应要求变为大服模式
        - 缓存方案为本地缓存
    - 解决方案：
        - 利用redis存储用户路由信息
        - 请求入口服务用来将用户请求路由到各自的逻辑服务器
        - [sticky session](http://wiki.metawerx.net/wiki/StickySessions)类似的方案
