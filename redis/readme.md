# Redis 主从集群哨兵集群逻辑网络模式

## 使用
* 将 .conf 内所有 IP 为 192.168.33.37 改为你本地IP
* 执行 "docker compose up -d" 启动

## 检查
### 查看主从节点信息
```shell
# 连接 redis server 默认 127.0.0.1 6379
/data # redis-cli
# 验证主从节点密码
127.0.0.1:6379> auth test
OK
# 查看节点信息
127.0.0.1:6379> info replication
# Replication 主
role:master
connected_slaves:2
slave0:ip=host.docker.internal,port=6380,state=online,offset=798,lag=0
slave1:ip=host.docker.internal,port=6381,state=online,offset=798,lag=1
master_failover_state:no-failover
master_replid:5b6c8191a38b899dfe3586268537553da9357be2
master_replid2:0000000000000000000000000000000000000000
master_repl_offset:798
second_repl_offset:-1
repl_backlog_active:1
repl_backlog_size:1048576
repl_backlog_first_byte_offset:1
repl_backlog_histlen:798


# Replication 从
role:slave
master_host:192.168.33.37
master_port:6379
master_link_status:up
master_last_io_seconds_ago:2
master_sync_in_progress:0
slave_read_repl_offset:868
slave_repl_offset:868
slave_priority:100
slave_read_only:1
replica_announced:1
connected_slaves:0
master_failover_state:no-failover
master_replid:5b6c8191a38b899dfe3586268537553da9357be2
master_replid2:0000000000000000000000000000000000000000
master_repl_offset:868
second_repl_offset:-1
repl_backlog_active:1
repl_backlog_size:1048576
repl_backlog_first_byte_offset:1
repl_backlog_histlen:868
127.0.0.1:6379>
```


### 查看哨兵节点跟追主从节点信息
```shell
# 连接 redis server 默认 127.0.0.1 6379
/data # redis-cli
# 验证哨兵节点密码
127.0.0.1:6379> auth sentinel
OK
127.0.0.1:6379> info sentinel
# 返回哨兵信息
# Sentinel
sentinel_masters:1
sentinel_tilt:0
sentinel_running_scripts:0
sentinel_scripts_queue_length:0
sentinel_simulate_failure_flags:0
master0:name=mymaster,status=ok,address=192.168.33.37:6379,slaves=2,sentinels=3
127.0.0.1:6379> sentinel master mymaster
# 返回主节点信息
 1) "name"
 2) "mymaster"
 3) "ip"
 4) "192.168.33.37"
 5) "port"
 6) "6379"
 7) "runid"
 8) "1dede4e2d3bb0598f5079b2b5b392805790df59c"
 9) "flags"
10) "master"
11) "link-pending-commands"
12) "0"
13) "link-refcount"
14) "1"
15) "last-ping-sent"
16) "0"
17) "last-ok-ping-reply"
18) "259"
19) "last-ping-reply"
20) "259"
21) "down-after-milliseconds"
22) "5000"
23) "info-refresh"
24) "1791"
25) "role-reported"
26) "master"
27) "role-reported-time"
28) "72253"
29) "config-epoch"
30) "0"
31) "num-slaves"
32) "2"
33) "num-other-sentinels"
34) "2"
35) "quorum"
36) "2"
37) "failover-timeout"
38) "10000"
39) "parallel-syncs"
40) "1"
127.0.0.1:6379> sentinel slaves mymaster
# 返回两个从节点信息
1)  1) "name"
    2) "192.168.33.37:6381"
    3) "ip"
    4) "192.168.33.37"
    5) "port"
    6) "6381"
    7) "runid"
    8) "26df331d27b2c06cf63a068d5bdc7f98ed064d6c"
    9) "flags"
   10) "slave"
   11) "link-pending-commands"
   12) "0"
   13) "link-refcount"
   14) "1"
   15) "last-ping-sent"
   16) "0"
   17) "last-ok-ping-reply"
   18) "932"
   19) "last-ping-reply"
   20) "932"
   21) "down-after-milliseconds"
   22) "5000"
   23) "info-refresh"
   24) "5433"
   25) "role-reported"
   26) "slave"
   27) "role-reported-time"
   28) "95915"
   29) "master-link-down-time"
   30) "0"
   31) "master-link-status"
   32) "ok"
   33) "master-host"
   34) "192.168.33.37"
   35) "master-port"
   36) "6379"
   37) "slave-priority"
   38) "100"
   39) "slave-repl-offset"
   40) "19289"
   41) "replica-announced"
   42) "1"
2)  1) "name"
    2) "192.168.33.37:6380"
    3) "ip"
    4) "192.168.33.37"
    5) "port"
    6) "6380"
    7) "runid"
    8) "f0a0cba8df07263352cbe93dce8c99a1d5f2b0fb"
    9) "flags"
   10) "slave"
   11) "link-pending-commands"
   12) "0"
   13) "link-refcount"
   14) "1"
   15) "last-ping-sent"
   16) "0"
   17) "last-ok-ping-reply"
   18) "932"
   19) "last-ping-reply"
   20) "932"
   21) "down-after-milliseconds"
   22) "5000"
   23) "info-refresh"
   24) "5433"
   25) "role-reported"
   26) "slave"
   27) "role-reported-time"
   28) "95905"
   29) "master-link-down-time"
   30) "0"
   31) "master-link-status"
   32) "ok"
   33) "master-host"
   34) "192.168.33.37"
   35) "master-port"
   36) "6379"
   37) "slave-priority"
   38) "100"
   39) "slave-repl-offset"
   40) "19289"
   41) "replica-announced"
   42) "1"
127.0.0.1:6379>
```



## 问题
* 主从节点警告信息
> 1:S 25 Jul 2022 07:28:34.120 # WARNING overcommit_memory is set to 0! Background save may fail under low memory condition. To fix this issue add 'vm.overcommit_memory = 1' to /etc/sysctl.conf and then reboot or run the command 'sysctl vm.overcommit_memory=1' for this to take effect.
```shell
# 执行命令行
sysctl vm.overcommit_memory=1

# 或者
vi /etc/sysctl.conf
# 文件末尾追加
vm.overcommit_memory = 1
# 执行命令配置生效
sysctl -p
```