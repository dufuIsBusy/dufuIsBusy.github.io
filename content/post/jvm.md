---
title: "Jvm"
date: 2019-05-31T16:11:18+08:00
draft: false
---
#### 参数
标准参数（-），所有的JVM实现都必须实现这些参数的功能，而且向后兼容;
```
java
```
非标准参数（-X），默认jvm实现这些参数的功能，但是并不保证所有jvm实现都满足，且不保证向后兼容；
```
java -X
```
非Stable参数（-XX），此类参数各个jvm实现会有所不同，将来可能会随时取消，需要慎重使用（但是，这些参数往往是非常有用的）
```
java -XX:+PrintFlagsFinal
```
#### 查看JVM使用的默认的垃圾收集器
```
java -XX:+PrintCommandLineFlags -version
-XX:+PrintGCDetails  -XX:+PrintCommandLineFlags
```

#### 参数使用方式
```
-XX:+\<option\> 开启option参数
-XX:-\<option\> 关闭option参数
-XX:\<option\>=\<value\> 将option参数值设置为value
```

#### 查询参数值
jinfo -flag MaxDirectMemorySize 21184
java -XX:+PrintFlagsFinal

#### 启动tomcat时开启gc日志
在catalina.sh里添加如下变量即可

```
JAVA_OPTS='-verbose:gc -Xloggc:/home/ubuntu/logs/gc.log -XX:+PrintGCDetails -XX:+PrintGCDateStamps'
```

```
JAVA_OPTS='-verbose:gc -Xloggc:/home/ubuntu/logs/gc.log -XX:+PrintGCDetails -XX:+PrintGCDateStamps -XX:+UseGCLogFileRotation -XX:NumberOfGCLogFiles=100 -XX:GCLogFileSize=100K'
```

#### JVM中哪些flag可以被jinfo动态修改

```
java -XX:+PrintFlagsFinal -version|grep manageable
```

#### OOM，直接造成内存溢出错误使得程序退出。OOM又可以分为以下几种：
1. Heap space：堆内存不足
1. PermGen space：永久代内存不足
1. Native thread：本地线程没有足够内存可分配

#### 查看jvm内存使用状况：

```
jmap -heap
```

#### 查看jvm内存存活的对象：

```
jmap -histo:live
```

#### 把heap里所有对象都dump下来，无论对象是死是活：

```
jmap -dump:format=b,file=xxx.hprof
```

#### 先做一次full GC，再dump，只包含仍然存活的对象信息：

```
jmap -dump:format=b,live,file=xxx.hprof
```

#### 频繁GC问题或内存溢出问题定位过程
1. 使用jps查看线程ID
1. 使用jstat -gc 3331 250 20 查看gc情况，一般比较关注PERM区的情况，查看GC的增长情况。
1. 使用jstat -gccause：额外输出上次GC原因
1. 使用jmap -dump:format=b,file=heapDump 3331生成堆转储文件
1. 使用jhat或者可视化工具（Eclipse Memory Analyzer 、IBM HeapAnalyzer）分析堆情况。
1. 结合代码解决内存溢出或泄露问题。

#### 死锁问题定位过程
1. 使用jps查看线程ID
1. 使用jstack 3331：查看线程情况

#### docker里运行jinfo等命令

```
docker run --cap-add=SYS_PTRACE -it bc336035e74e  /bin/bash
```

```
docker run --security-opt seccomp:unconfined(不推荐）
```

