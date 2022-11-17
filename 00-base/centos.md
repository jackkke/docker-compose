# CentOS 7 

## 1. 固定IP

## 2. 更新+自动更新
```shell
yum update -y
yum -y install cronie yum-cron

vi /etc/yum/yum-cron.conf

update_messages = yes
download_updates = yes
apply_updates = yes

systemctl restart crond.service
systemctl restart yum-cron.service
```

## 3. 安装必备

```bash
yum install -y vim git zip unzip
```

## 4. 确认环境信息
```bash
[root@zion ~]# python -V
Python 2.7.5
```

## 5. 安装docker
```bash
curl -fsSL https://get.docker.com | bash -s docker --mirror Aliyun

mkdir /etc/docker

sudo tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["https://e8nts1n5.mirror.aliyuncs.com"]
}
EOF

docker info | grep aliyun
```

```bash
[root@zion ~]# docker -v
Docker version 20.10.21, build baeda1f
[root@zion ~]# docker compose version
Docker Compose version v2.12.2
```