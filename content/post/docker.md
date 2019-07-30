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
