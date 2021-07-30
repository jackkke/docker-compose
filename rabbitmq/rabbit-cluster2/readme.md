# 设置节点1(磁盘节点)：

```sh
docker exec -it myrabbit1 bash
rabbitmqctl stop_app
rabbitmqctl reset
rabbitmqctl start_app
exit
```

# 设置节点2(内存节点)，加入到集群：

```sh
docker exec -it myrabbit2 bash
rabbitmqctl stop_app
rabbitmqctl reset
rabbitmqctl join_cluster --ram rabbit@rabbitmq_host1
rabbitmqctl start_app
exit
```

# 设置节点3(内存节点)，加入到集群：

```sh
docker exec -it myrabbit3 bash
rabbitmqctl stop_app
rabbitmqctl reset
rabbitmqctl join_cluster --ram rabbit@rabbitmq_host1
rabbitmqctl start_app
exit
```
