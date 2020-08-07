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

### mysql压力测试
```
sysbench --mysql-host=127.0.0.1 --mysql-port=3306 --mysql-user=root --mysql-password=root \
--mysql-db=sbtest --report-interval=10 --time=120 --tables=4 --table-size=10000000 --threads=1 \
/usr/share/sysbench/oltp_read_write.lua prepare

docker run --rm=true --name=sb-prepare severalnines/sysbench sysbench --db-driver=mysql --oltp-table-size=100000 \
--oltp-tables-count=24 --threads=1 --mysql-host=192.168.1.30 --mysql-port=3306 --mysql-user=root --mysql-password=root \
/usr/share/sysbench/tests/include/oltp_legacy/parallel_prepare.lua run

sysbench --mysql-host=192.168.0.26 --mysql-port=3306 --mysql-user=root --mysql-password=root \
--mysql-db=sbtest --report-interval=10 --time=120 --tables=4 --table-size=10000000 --threads=1 \
/usr/share/sysbench/oltp_read_write.lua run

docker run --name=sb-run severalnines/sysbench sysbench --db-driver=mysql --report-interval=10 --mysql-table-engine=innodb \
--oltp-table-size=100000 --oltp-tables-count=24 --threads=64 --time=120 --mysql-host=192.168.1.30 --mysql-port=3306 \
--mysql-user=root --mysql-password=root /usr/share/sysbench/tests/include/oltp_legacy/oltp.lua run

sysbench --mysql-host=127.0.0.1 --mysql-port=3306 --mysql-user=root --mysql-password=root \
--mysql-db=sbtest --report-interval=10 --time=120 --tables=4 --table-size=10000000 --threads=1 \
/usr/share/sysbench/oltp_read_write.lua cleanup
```
