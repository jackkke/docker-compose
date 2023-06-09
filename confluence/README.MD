# Confluence

## 测试通过最高版本
7.19.0
测试不通过版本 8.0.0-m023

## 启动

> 注意，database 字符集 必须为 "utf8mb4_bin" 或 "utf8_bin"  
```cmd
docker compose up -d
```

## 访问
[站点首页](http://localhost:18090)
访问后，记录你的server id，例如 “BSMM-WSS3-024O-N0P4”

## 配置
> [大神主页](https://zhile.io/2018/12/20/atlassian-license-crack.html)
> [下载连接](https://pan.baidu.com/s/1-hdPFmIEb7yD5S9M7nXMGg) 提取码：s8uw
```shell
# 通过下面命令生成 confluence key (此方法同样适用 atlassian 其他产品)
java -jar atlassian-agent.jar -p conf -m jackkke@jackkke.com -n jackkke -o https://jackkke.github.io -s BSMM-WSS3-024O-N0P4

# 通过下面命令生成插件 key（-p 参数为应用密钥）
java -jar atlassian-agent.jar -p org.swift.confluence.markdown -m jackkke@jackkke.com -n jackkke -o https://jackkke.github.io -s BSMM-WSS3-024O-N0P4
java -jar atlassian-agent.jar -p mohamicorp-render-markdown -m jackkke@jackkke.com -n jackkke -o https://jackkke.github.io -s BSMM-WSS3-024O-N0P4

```

## 附件下载
* 蓝奏云  
[链接](https://jackkke.lanzouv.com/b03p772sd) 密码:1nkw  
* 百度云  
[链接](https://pan.baidu.com/s/1PbiHbIvlmxSsMdOXyceNQQ) 提取码：csnh
