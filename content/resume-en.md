---
title: "Resume"
date: 2018-04-10
---

### Basic Information

* Male 27 years old
* Bachelor degree in Computer Science and Technology, Beijing University of Technology
* E-mail: zh-@outlook.com
* Github: https://github.com/walktall

### Skills

* 4 years Go experience
* Familiar with Docker
* Familiar with Kubernetes
* Familiar with EFK

### Work Experience
- Caicould
    - Backend Engineer 2017.08 until now
    - Focus on EFK (Elasticsearch + Fluentd + Kibana) stack on kubernetes

- Tantan Tech
    - Senior Backend Engineer 2016.03 - 2017.04 (1 year and 1 month)
    - Project: [Tantan](https://tantanapp.com)
    - Description: Social APP
    - Responsibilities: Backend development
    - The main work:
        - Antispam solutions and backend implementations
        - Media cloud service optimization and high availability
        - Push service optimization
        - Code architecture adjustment and optimization
        - The containerization of the development environment

- Nicescale Tech
    - Backend Engineer 2015.05 - 2016.02 (9 months)
    - Project: [cSphere](https://csphere.cn/)
    - Description: Docker container management
    - Responsibilities: Backend development
    - The main work:
        - Use Git's Webhook to automate building Docker image and push to docker registry
        - Customize Docker Compose based on Docker Swarm
        - Based on Prometheus, to achieve container and host monitoring and alarming
        - Design and Development of audit log feature
        - Responsible for code review

- Nikki Game
    - Backend Engineer 2014.07 - 2015.04 (9 months)
    - Project: [Miracle Nikki](https://qjnn.qq.com/)
    - Description: HTTP-based game
    - Responsibilities: Backend development and devops
    - The main work:
        - Application server architecture design
        - Game logic development
        - Use python for project publishing and development of test scripts
        - Git Admin
        - Stress testing

### Some project introductions
- EFK in Caicloud
    - API for easily quering kubernets resources log based on EFK
    - EFK stack maintenance
    - Make some contributions on [elastic/beats](https://github.com/elastic/beats/search?q=walktall&type=Issues&utf8=%E2%9C%93)
    - Log stream monitoring based on [percolate query](https://www.elastic.co/guide/en/elasticsearch/reference/current/query-dsl-percolate-query.html)

- Antispam in Tantan
    - Design and implement the client request validation code
    - Define rules and implement rules based on Spammers behavior
    - Design and implement services for analyzing user registration events
    - Some technical details:
        - Since it is hard to add middleware in old code, So use [mux](https://github.com/gorilla/mux) instead to refactor router
        - Use [new package layout](https://medium.com/@benbjohnson/standard-package-layout-7cdbc8391fc1#.t402ijwu4) to write service

- Media Cloud in Tantan
    - Problem: There are two object storage services used to store the media file uploaded by user, but if one of services died, uploading will be rejected
    - Solution: As long as there is a storage service to survive, it will not make the upload failed by recording the file ID and re-uploading when the crash service is back
    - Other issues:
        - Limit file size uploaded by user
        - Write RPM Spec and Dockerfile
    - Some technical details:
        - [Boltdb](https://github.com/boltdb/bolt) for recording file ID
        - Implement [circuit breaker](https://martinfowler.com/bliki/CircuitBreaker.html) for service availability checking

- Push service in Tantan
    - Problem: Slow push, The chart shows a decrease in push amount
    - Use [Go-torch](https://github.com/uber/go-torch) for tracing problem
    - Discovered Problems:
        - Push log is too long to cause the syslog service to cut off the log, log entry hit the random location on disk leading to a poor performance of the syslog server disk, resulting in the log losing, and the source of chart data is the log so it went down too
        - Big and complex log entry make fmt using too much reflections
    - Solutions:
        - Limit the length of the push log
        - Increase the number of push concurrency

- Compose in cSphere
    - Based on [libcompose](https://github.com/docker/libcompose) implements the docker compose feature
    - Some technical details:
        - Docker API Call
        - Using mongodb for saving metadata

- Arch design in Nikki
    - Background:
        - The small service should be changed into a large service mode
        - Using local cache in app server
    - Solutions:
        - Use redis for saving users cache location
        - Portal services used for users routing
        - Similar to [sticky session](http://wiki.metawerx.net/wiki/StickySessions)
