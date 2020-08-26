---
title: "Maven"
date: 2020-08-26T11:11:36+08:00
draft: false
---

生成骨架命令
```
mvn archetype:generate -DinteractiveMode=false -DarchetypeCatalog=remote -DarchetypeRepository=https://repo.rdc.aliyun.com/repository/28238-release-F3OKjA -DarchetypeGroupId=com.yunli.smart.archetype -DarchetypeArtifactId=api-spring-cloud-alibaba-archetype -DarchetypeVersion=2.1.1.RELEASE -DgroupId=com.yunli.smart -DartifactId=work-order-service-api -Dversion=1.0.0-SNAPSHOT

mvn archetype:generate -DinteractiveMode=false -DarchetypeCatalog=remote -DarchetypeRepository=https://repo.rdc.aliyun.com/repository/28238-release-F3OKjA -DarchetypeGroupId=com.yunli.smart.archetype -DarchetypeArtifactId=portal-spring-cloud-alibaba-archetype -DarchetypeVersion=2.1.1.RELEASE -DgroupId=com.yunli.smart -DartifactId=work-order-portal -Dversion=1.0.0-SNAPSHOT

mvn archetype:generate -DinteractiveMode=false -DarchetypeCatalog=remote -DarchetypeRepository=https://repo.rdc.aliyun.com/repository/28238-release-F3OKjA -DarchetypeGroupId=com.yunli.smart.archetype -DarchetypeArtifactId=service-spring-cloud-alibaba-archetype -DarchetypeVersion=2.1.1.RELEASE -DgroupId=com.yunli.smart -DartifactId=work-order-service -Dversion=1.0.0-SNAPSHOT
```
