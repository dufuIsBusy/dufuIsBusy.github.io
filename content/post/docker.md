---
title: "Docker"
date: 2019-06-12T17:23:03+08:00
---

### 使用docker连接redis
```
docker pull redis
docker run -it --name yunli-redis -d  -p6379:6379 redis
docker exec -it yunli-redis /bin/bash -c "cd /usr/redis/src && ./redis-cli -h ip"
```

### 使用docker连接mysql
```
docker run -it --name yunli-sql -d  -p3306:3306 -e MYSQL_ROOT_PASSWORD=root alisql/alisql
docker exec -it yunli-sql /bin/bash -c "mysql -h ip -u root -p123456"
```
### 使用docker导出表结构
```
docker exec -it yunli-sql /bin/bash -c "mysqldump -uroot -proot -hlocalhost -P3306 --databases call_service --no-data" > ./call_service.sql
docker exec -it yunli-sql /bin/bash -c "mysqldump -uroot -proot -h localhost -P3306 call_service call_voice_model" > ./call_service.sql
```
