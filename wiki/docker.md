##docker
对原生rocketMQ添加docker支持，主要的想法是让broker能根据环境变量注册自己。而不是完全读取网卡信息。同时为了让rocketMQ运行在云环境中，特变更了-c参数，使它能支持URL的方式读取配置文件。

###使用方式
在rocketMQ启动时需要注册IP,端口，HA IP，HA端口。在环境变量中分别配置：
```
rocketmq.ip=192.168.1.1
rocketmq.port=1234
rocketmq.ha.ip=192.168.1.1
rocketmq.ha.port=1235
```

默认情况下会使用docker宿主机的IP，以及docker随机的端口。


###运行

运行namesrv
```
docker run -it  juqkai/rocketmq-broker
```

运行broker
```
docker run -it -e rocketmq.ip=192.168.1.1 -e rocketmq.ip=1234 -e rocketmq.ha.ip=192.168.1.1 -e rocketmq.ha.port=1235 -p 1234:10911 -p 1235:10912 juqkai/rocketmq-broker
```
不指定IP与端口
```
docker run -it -P juqkai/rocketmq-broker
```

指定远程配置文件

```
docker run -it -P juqkai/rocketmq-broker -c http://192.168.1.2/broker-a.properties
```
