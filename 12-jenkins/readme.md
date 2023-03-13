## 1. 安装jenkins
## 2. 升级war
```shell
docker exec -it -u root jenkins bash
cd /usr/share/jenkins/
mv jenkins.war jenkins.war.bak
wget https://mirrors.tuna.tsinghua.edu.cn/jenkins/war-stable/latest/jenkins.war
ls -l
exit
docker restart jenkins
```
## 3. 重启
按照推荐 安装插件
查看默认用户 **admin** 密码 _4f009c0431b349eeb81536a029f7d9fe_
```shell
docker exec -it -u root jenkins bash
cat /var/jenkins_home/secrets/initialAdminPassword
```

## 4. 一些在用插件
* publish over ssh
* subversion
* Maven Integration


## 5. 一些技巧

### 5.1 默认 jdk 信任证书, 增加 jre 文件夹与两个必备jar
```shell
docker exec -it -u root jenkins bash
cd /opt/java/openjdk/bin
keytool -import -v -trustcacerts -alias maven -file /var/jenkins_home/maven.crt -storepass changeit -keystore /opt/java/openjdk/lib/security/cacerts
mkdir /opt/java/openjdk/jre
mkdir /opt/java/openjdk/jre/lib
mv /var/jenkins_home/*.jar /opt/java/openjdk/jre/lib/
```

### 5.2 node 安装失败
alpine linux 使用国内镜像源进行加速  
默认的源地址为：http://dl-cdn.alpinelinux.org/，修改地址可以编辑源文件 /etc/apk/repositories。
```shell
cat /etc/apk/repositories
sed -i ‘s/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g’ /etc/apk/repositories
#sed -i ‘s/dl-cdn.alpinelinux.org/mirrors.ustc.edu.cn/g’ /etc/apk/repositories
#sed -i ‘s/dl-cdn.alpinelinux.org/mirrors.tuna.tsinghua.edu.cn/g’ /etc/apk/repositories

apk update
apk upgrade
#apk add bash
#apk add bash-doc
#apk add bash-completion

apk add nodejs
apk add npm
```