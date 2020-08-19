# master 查看节点
rabbitmqctl cluster_status

```sh
Cluster status of node mqmaster@2bbfc97b7d21 ...
Basics
Cluster name: mqmaster@2bbfc97b7d21
Disk Nodes
mqmaster@2bbfc97b7d21
Running Nodes
mqmaster@2bbfc97b7d21
Versions
mqmaster@2bbfc97b7d21: RabbitMQ 3.8.6 on Erlang 23.0.3
```
# slave 执行

* rabbitmqctl stop_app 添加集群之前关闭当前的节点
* rabbitmqctl reset
* rabbitmqctl join_cluster --ram mqmaster@2bbfc97b7d21
* rabbitmqctl start_app 重新开启节点

```sh
# 开始添加到 集群当中, @前面是 节点名称， 后面是 host， host 可以在 查看集群状态的时候获得
# --ram选项表示节点以内存存储方式运行，读写速度快，重启后内容会丢失；不加--ram选项，节点则以磁盘存储方式运行，虽然读写速度慢，但是内容一般可以持久保持
Clustering node mqslave1@dd66a7e679fb with mqmaster@2bbfc97b7d21
```

# 添加策略
登录rabbitmq管理页面 ——> Admin ——> Policies ——> Add / update a policy
name：随便取，策略名称
Pattern：^ 匹配符，只有一个^代表匹配所有
Definition：ha-mode=all 为匹配类型，分为3种模式：all（表示所有的queue）

# Spring Cloud 集群配置

```properties
spring:
　　rabbitmq:
　　　　addresses: ip1:port1,ip2:port2,ip3:port3
　　　　username: username
　　　　password: password
```