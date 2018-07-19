===================================================================================================================================================================================
V1.5.6
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
server端
依赖：
<dependency>
    <groupId>de.codecentric</groupId>
    <artifactId>spring-boot-admin-server</artifactId>
    <version>1.5.6</version>
</dependency>
<dependency>
    <groupId>de.codecentric</groupId>
    <artifactId>spring-boot-admin-server-ui</artifactId>
    <version>1.5.6</version>
</dependency>
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-netflix-eureka-server</artifactId>
    <version>1.4.4.RELEASE</version>
</dependency>
1、 配置端口 启动类添加@EnableAdminServer 
2、 配置spring.boot.admin.context-path，可调整监控页面访问url
3、 eureka配置
eureka:
  instance:
    leaseRenewalIntervalInSeconds: 10
  client:
    registryFetchIntervalSeconds: 5
    serviceUrl:
      defaultZone: http://localhost:8761/eureka/
4、解决/health端点访问超时配置
management:
  security:
    enabled: false
  health:
    db:
      enabled: false
    mail:
      enabled: false
    redis:
      enabled: false
    mongo:
      enabled: false

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
client端
依赖：
<dependency>
    <groupId>de.codecentric</groupId>
    <artifactId>spring-boot-admin-starter-client</artifactId>
    <version>1.5.6</version>
</dependency>
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-netflix-eureka-server</artifactId>
    <version>1.4.4.RELEASE</version>
</dependency>
1、 配置端口 指定spring.boot.admin.url 为对应server服务IP和端口(http://ip:port)
2、 显示版本信息
info.groupId: @project.groupId@
info.artifactId: @project.artifactId@
info.version: @project.version@
3、注册eureka
spring:
  application:
    name: producer1
eureka:
  client:
    serviceUrl:
      defaultZone: http://localhost:8761/eureka/
management:
  security:
    enabled: false
===================================================================================================================================================================================
配置mail,汇报监控应用程序上线下线

spring:
  mail:
    host: smtp.163.com
    username: xxx@163.com
    password: xxx(授权码)
    properties:
      mail:
        smtp:
          auth: true
          starttls:
            enable: true
            required: true
  boot:
    admin:
      notify:
        mail:
          from: xxx@163.com
          to: yyy@qq.com
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
