# docker-compose
 docker-compose


# .gitignore
以斜杠/开头表示目录；
以星号*通配多个字符；
以问号?通配单个字符
以方括号[]包含单个字符的匹配列表；
以叹号!表示不忽略(跟踪)匹配到的文件或目录；

此外，git 对于 .ignore 配置文件是按行从上到下进行规则匹配的，意味着如果前面的规则匹配的范围更大，则后面的规则将不会生效；
# zookeeper
进入集群查看集群状态
```sh
docker exec -it zookeeper /bin/sh
cd bin
zkServer.sh status
```

deploy标签生效
docker-compose --compatibility up