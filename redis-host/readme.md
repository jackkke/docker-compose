docker network create --subnet 19.7.12.0/24 redisnet

```shell
# redis-cli
127.0.0.1:6379> auth test
OK
127.0.0.1:6379> info replication
# Replication
role:master
connected_slaves:2
slave0:ip=172.19.0.1,port=6379,state=online,offset=308,lag=1
slave1:ip=172.19.0.1,port=6379,state=online,offset=308,lag=1
master_failover_state:no-failover
master_replid:d2a47b5a96b5ee423193d586cb457eb12ddcc39a
master_replid2:0000000000000000000000000000000000000000
master_repl_offset:308
second_repl_offset:-1
repl_backlog_active:1
repl_backlog_size:1048576
repl_backlog_first_byte_offset:1
repl_backlog_histlen:308
127.0.0.1:6379> 
```



sentinel master redis-master-aiman

sentinel slaves mymaster