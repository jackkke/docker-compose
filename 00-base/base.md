# Docker 全家桶 

## 基础
1. 网络
    ```shell
   docker network create --driver bridge --subnet 19.7.12.0/24 --gateway 19.7.12.1 zion
    ```
2. 卷
   

## Portainer

```shell
docker volume create portainer
```

## Registry

```shell
docker volume create registry
```


## Redis

```shell
docker volume create redis-master
docker volume create redis-slave1
docker volume create redis-slave2
docker volume create redis-sentinel1
docker volume create redis-sentinel2
docker volume create redis-sentinel3
```

## MySQL

```shell
docker volume create mysql
```


## NACOS

```shell
docker volume create nacos
```


## xxljob

```shell
docker volume create xxljob
```

## mongodb

```shell
docker volume create mongodb
```

