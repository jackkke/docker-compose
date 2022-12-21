# 基于 MySql 搭建 Nacos 与 Seata

## 启动 Nacos
### 文件与目录解释
* .env 文件指定镜像版本
* docker-compose.yml 启动脚本
* nacos-standlone-mysql.env 初始配置，包括指定mysql信息等
* init.d 初始化配置，可忽略
### 启动
```shell
cd docker-compose\alibaba\nacos
docker compose up -d
```
### 启动日志
```text
Nacos is starting, you can docker logs your container

         ,--.
       ,--.'|
   ,--,:  : |                                           Nacos 2.1.1
,`--.'`|  ' :                       ,---.               Running in stand alone mode, All function modules
|   :  :  | |                      '   ,'\   .--.--.    Port: 8848
:   |   \ | :  ,--.--.     ,---.  /   /   | /  /    '   Pid: 1
|   : '  '; | /       \   /     \.   ; ,. :|  :  /`./   Console: http://192.168.208.2:8848/nacos/index.html
'   ' ;.    ;.--.  .-. | /    / ''   | |: :|  :  ;_
|   | | \   | \__\/: . ..    ' / '   | .; : \  \    `.      https://nacos.io
'   : |  ; .' ," .--.; |'   ; :__|   :    |  `----.   \
|   | '`--'  /  /  ,.  |'   | '.'|\   \  /  /  /`--'  /
'   : |     ;  :   .'   \   :    : `----'  '--'.     /
;   |.'     |  ,     .-./\   \  /            `--'---'
'---'        `--`---'     `----'

2022-08-17 16:18:16,348 INFO Tomcat initialized with port(s): 8848 (http)

2022-08-17 16:18:16,419 INFO Root WebApplicationContext: initialization completed in 2655 ms

2022-08-17 16:18:20,119 INFO Adding welcome page: class path resource [static/index.html]

2022-08-17 16:18:20,449 WARN You are asking Spring Security to ignore Ant [pattern='/**']. This is not recommended -- please use permitAll via HttpSecurity#authorizeHttpRequests instead.

2022-08-17 16:18:20,451 INFO Will not secure Ant [pattern='/**']

2022-08-17 16:18:20,496 INFO Will secure any request with [org.springframework.security.web.context.request.async.WebAsyncManagerIntegrationFilter@6d0b5baf, org.springframework.security.web.context.SecurityContextPersistenceFilter@7c7d3c46, org.springframework.security.web.header.HeaderWriterFilter@21d8bcbe, org.springframework.security.web.csrf.CsrfFilter@2488b073, org.springframework.security.web.authentication.logout.LogoutFilter@3a94964, org.springframework.security.web.savedrequest.RequestCacheAwareFilter@48c35007, org.springframework.security.web.servletapi.SecurityContextHolderAwareRequestFilter@6722db6e, org.springframework.security.web.authentication.AnonymousAuthenticationFilter@631e06ab, org.springframework.security.web.session.SessionManagementFilter@7383eae2, org.springframework.security.web.access.ExceptionTranslationFilter@31e3250d]

2022-08-17 16:18:20,516 INFO Exposing 1 endpoint(s) beneath base path '/actuator'

2022-08-17 16:18:20,561 INFO Tomcat started on port(s): 8848 (http) with context path '/nacos'

2022-08-17 16:18:20,586 INFO Nacos started successfully in stand alone mode. use external storage
```
### 访问
* [点此访问](http://localhost:8848/nacos)
* 账号：nacos
* 密码：nacos

## 启动Seata
### 文件与目录解释
* .env 文件指定镜像版本
* docker-compose.yml 启动脚本
* seata-server/resources/application.yml 初始化配置
### **你的**自定义配置
.env -> HOSTIP=host.docker.internal 指向宿主机IP。如果启动失败，可以将此改为你本地IP
### 启动
```shell
cd docker-compose\alibaba\seata
docker compose up -d
```
### 启动日志
```text
███████╗███████╗ █████╗ ████████╗ █████╗
██╔════╝██╔════╝██╔══██╗╚══██╔══╝██╔══██╗
███████╗█████╗  ███████║   ██║   ███████║
╚════██║██╔══╝  ██╔══██║   ██║   ██╔══██║
███████║███████╗██║  ██║   ██║   ██║  ██║
╚══════╝╚══════╝╚═╝  ╚═╝   ╚═╝   ╚═╝  ╚═╝


08:19:17.094  INFO --- [                     main] io.seata.server.ServerApplication        : Starting ServerApplication using Java 1.8.0_212 on seata-server with PID 1 (/seata-server/classes started by root in /seata-server)
08:19:17.109  INFO --- [                     main] io.seata.server.ServerApplication        : No active profile set, falling back to default profiles: default
08:19:18.500  INFO --- [                     main] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat initialized with port(s): 7091 (http)
08:19:18.515  INFO --- [                     main] o.a.coyote.http11.Http11NioProtocol      : Initializing ProtocolHandler ["http-nio-7091"]
08:19:18.516  INFO --- [                     main] o.apache.catalina.core.StandardService   : Starting service [Tomcat]
08:19:18.516  INFO --- [                     main] org.apache.catalina.core.StandardEngine  : Starting Servlet engine: [Apache Tomcat/9.0.55]
08:19:18.597  INFO --- [                     main] o.a.c.c.C.[Tomcat].[localhost].[/]       : Initializing Spring embedded WebApplicationContext
08:19:18.598  INFO --- [                     main] w.s.c.ServletWebServerApplicationContext : Root WebApplicationContext: initialization completed in 1439 ms
08:19:19.417  INFO --- [                     main] o.s.b.a.w.s.WelcomePageHandlerMapping    : Adding welcome page: class path resource [static/index.html]
08:19:19.589  INFO --- [                     main] o.s.s.web.DefaultSecurityFilterChain     : Will secure Ant [pattern='/'] with []
08:19:19.589  INFO --- [                     main] o.s.s.web.DefaultSecurityFilterChain     : Will secure Ant [pattern='/**/*.css'] with []
08:19:19.589  INFO --- [                     main] o.s.s.web.DefaultSecurityFilterChain     : Will secure Ant [pattern='/**/*.js'] with []
08:19:19.589  INFO --- [                     main] o.s.s.web.DefaultSecurityFilterChain     : Will secure Ant [pattern='/**/*.html'] with []
08:19:19.590  INFO --- [                     main] o.s.s.web.DefaultSecurityFilterChain     : Will secure Ant [pattern='/**/*.map'] with []
08:19:19.590  INFO --- [                     main] o.s.s.web.DefaultSecurityFilterChain     : Will secure Ant [pattern='/**/*.svg'] with []
08:19:19.591  INFO --- [                     main] o.s.s.web.DefaultSecurityFilterChain     : Will secure Ant [pattern='/**/*.png'] with []
08:19:19.596  INFO --- [                     main] o.s.s.web.DefaultSecurityFilterChain     : Will secure Ant [pattern='/**/*.ico'] with []
08:19:19.599  INFO --- [                     main] o.s.s.web.DefaultSecurityFilterChain     : Will secure Ant [pattern='/console-fe/public/**'] with []
08:19:19.599  INFO --- [                     main] o.s.s.web.DefaultSecurityFilterChain     : Will secure Ant [pattern='/api/v1/auth/login'] with []
08:19:19.627  INFO --- [                     main] o.s.s.web.DefaultSecurityFilterChain     : Will secure any request with [org.springframework.security.web.context.request.async.WebAsyncManagerIntegrationFilter@5fb5ad40, org.springframework.security.web.context.SecurityContextPersistenceFilter@34009349, org.springframework.security.web.header.HeaderWriterFilter@48f2054d, org.springframework.security.web.authentication.logout.LogoutFilter@5b066c33, io.seata.console.filter.JwtAuthenticationTokenFilter@615439f7, org.springframework.security.web.savedrequest.RequestCacheAwareFilter@4faf1f4, org.springframework.security.web.servletapi.SecurityContextHolderAwareRequestFilter@56a05324, org.springframework.security.web.authentication.AnonymousAuthenticationFilter@632cf7d3, org.springframework.security.web.session.SessionManagementFilter@76a9a009, org.springframework.security.web.access.ExceptionTranslationFilter@5520f675, org.springframework.security.web.access.intercept.FilterSecurityInterceptor@7a3f08b6]
08:19:19.701  INFO --- [                     main] o.a.coyote.http11.Http11NioProtocol      : Starting ProtocolHandler ["http-nio-7091"]
08:19:19.718  INFO --- [                     main] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat started on port(s): 7091 (http) with context path ''
08:19:19.733  INFO --- [                     main] io.seata.server.ServerApplication        : Started ServerApplication in 3.937 seconds (JVM running for 4.604)
08:19:20.701  INFO --- [                     main] com.alibaba.druid.pool.DruidDataSource   : {dataSource-1} inited
08:19:20.758  INFO --- [                     main] c.a.n.client.config.impl.ClientWorker    : [fixed-192.168.33.37_8848-seata] [subscribe] store.db.distributedLockTable+SEATA_GROUP+seata
08:19:20.760  INFO --- [                     main] c.a.nacos.client.config.impl.CacheData   : [fixed-192.168.33.37_8848-seata] [add-listener] ok, tenant=seata, dataId=store.db.distributedLockTable, group=SEATA_GROUP, cnt=1
08:19:20.760  INFO --- [                     main] c.a.nacos.client.config.impl.CacheData   : [fixed-192.168.33.37_8848-seata] [add-listener] ok, tenant=seata, dataId=store.db.distributedLockTable, group=SEATA_GROUP, cnt=2
08:19:20.760 ERROR --- [                     main] i.s.s.s.d.l.DataBaseDistributedLocker    : The distribute lock table is not config, please create the target table and config it
08:19:21.124  INFO --- [                     main] i.s.core.rpc.netty.NettyServerBootstrap  : Server started, service listen port: 8091
08:19:21.153  INFO --- [                     main] com.alibaba.nacos.client.naming          : initializer namespace from System Property :null
08:19:21.171  INFO --- [                     main] com.alibaba.nacos.client.naming          : [BEAT] adding beat: BeatInfo{port=8091, ip='192.168.33.37', weight=1.0, serviceName='SEATA_GROUP@@seata-server', cluster='default', metadata={}, scheduled=false, period=5000, stopped=false} to beat map.
08:19:21.176  INFO --- [                     main] com.alibaba.nacos.client.naming          : [REGISTER-SERVICE] seata registering service SEATA_GROUP@@seata-server with instance: Instance{instanceId='null', ip='192.168.33.37', port=8091, weight=1.0, healthy=true, enabled=true, ephemeral=true, clusterName='default', serviceName='null', metadata={}}
08:19:21.227  INFO --- [                     main] io.seata.server.ServerRunner             : seata server started in 1491 millSeconds
```
### 访问
* [点此访问](http://localhost:7091)
* 账号：seata
* 密码：seata
