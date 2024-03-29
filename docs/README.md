1. ### 快速开始

   ##### 稳定版

   > ##### Maven Release
   >
   > ```xml
   > <repositories>
   >  <repository>
   >      <id>aliyun-maven</id>
   >      <name>aliyun maven</name>
   >      <url>https://maven.aliyun.com/repository/public</url>
   >      <releases>
   >          <enabled>true</enabled>
   >      </releases>
   >      <snapshots>
   >          <enabled>true</enabled>
   >          <updatePolicy>always</updatePolicy>
   >      </snapshots>
   >  </repository>
   > </repositories>
   > ```
   >
   > ```xml
   > <dependencyManagement>
   >  <dependencies>
   >      <dependency>
   >          <groupId>com.github.liaomengge</groupId>
   >          <artifactId>base-framework-bom</artifactId>
   >          <version>${latest-release-version}</version>
   >          <type>pom</type>
   >          <scope>import</scope>
   >      </dependency>
   >  </dependencies>
   > </dependencyManagement>
   > ```
   >
   > ##### Gradle Release
   >
   > ```groovy
   > repositories {
   > mavenLocal()
   > maven { url 'https://maven.aliyun.com/repository/public' }
   > maven { url 'https://maven.aliyun.com/repository/spring' }
   > maven { url 'https://maven.aliyun.com/repository/spring-plugin' }
   > mavenCentral()
   > }
   > ```
   >
   > ```groovy
   > dependencyManagement {
   > imports {
   >  mavenBom "com.github.liaomengge:base-framework-bom:${latest-release-version}"
   > }
   > }
   > ```

   ##### 快照版

   > ##### Maven Snapshot
   >
   > ```xml
   > <repositories>
   >  <repository>
   >      <id>sonatype-nexus-snapshots</id>
   >      <name>Sonatype Nexus Snapshots</name>
   >      <url>https://oss.sonatype.org/content/repositories/snapshots/</url>
   >      <releases>
   >          <enabled>false</enabled>
   >      </releases>
   >      <snapshots>
   >          <enabled>true</enabled>
   >          <updatePolicy>always</updatePolicy>
   >      </snapshots>
   >  </repository>
   > </repositories>
   > 
   > ```
   >
   > ```xml
   > <dependencyManagement>
   >  <dependencies>
   >      <dependency>
   >          <groupId>com.github.liaomengge</groupId>
   >          <artifactId>base-framework-bom</artifactId>
   >          <version>${latest-snapshot-version}</version>
   >          <type>pom</type>
   >          <scope>import</scope>
   >      </dependency>
   >  </dependencies>
   > </dependencyManagement>
   > ```
   >
   > ##### Gradle Snapshot
   >
   > ```groovy
   > repositories {
   > mavenLocal()
   > maven { url 'https://maven.aliyun.com/repository/public' }
   > maven { url 'https://maven.aliyun.com/repository/spring' }
   > maven { url 'https://maven.aliyun.com/repository/spring-plugin' }
   > maven { url 'https://oss.sonatype.org/content/repositories/snapshots/' }
   > mavenCentral()
   > }
   > ```
   >
   > ```groovy
   > dependencyManagement {
   > imports {
   >  mavenBom "com.github.liaomengge:base-framework-bom:${latest-snapshot-version}"
   > }
   > }
   > ```

2. ### 模块说明

   ```
   **base**
   ├── base-common-cache -- 一二级缓存（维护）
   ├── base-common-dayu -- redis熔断降级（维护）
   ├── base-common-middleware -- activemq/rabbitmq封装（维护）
   ├── base-common-starter -- 常用starter（持续开发）⭐
   ├── base-common-utils -- 常用工具集（持续开发）⭐
   ├── base-dubbo-framework -- 项目dubbo简易封装（维护）
   ├── base-spring-cloud-framework -- 项目springcloud封装（持续开发）⭐
   └── base-platform-bom -- sb/sc/sca等依赖bom（持续开发）⭐
        ├── base-framework-bom -- base-framework依赖bom（持续开发）⭐
   ```

   **注：**目前主要持续开发的是`base-common-utils，base-common-starter，base-spring-cloud-framework，base-platform-bom`等分支，其他moudle已经很久没有迭代开发了 ~~~

   - **base-common-utils**

     基础util包，提供项目中常使用的工具集

   - **base-common-starter**

     基础starter包，提供项目常用的starter，便于快速使用（以只列出部分功能，更多使用参考源码，后续会附上每个的case案例）

     > 1. *base-apollo-spring-boot-starter*
     >    - 支持EnvironmentChangeEvent，@RefreshScope实时刷新
     >    - 支持部分@ConditionalOnProperty@Bean指定Bean动态创建/销毁
     > 2. *base-async-spring-boot-starter*
     >    - 支持@Async异步异常日志
     >    - 结合base-thread-pool-spring-boot-starter，支持注解指定线程池，统一管理线程池
     > 3. *base-base-mybatis-spring-boot-starter*
     >    - 支持druid和hikari数据源
     >    - 支持sqlId流控以及sql日志打印
     >    - 支持主从切换以及自定义mapper包切面处理
     > 4. *base-cache-spring-boot-starter*
     >    - 基础自定义一二级缓存starter
     > 5. *base-dayu-spring-boot-starter*
     >    - 支持guava，sentinel，自定义限流
     >    - 支持自定义sentinel数据源
     > 6. *base-design-patterns-spring-boot-starter*
     >    - 部分常见设计模式
     > 7. *base-endpoint-spring-boot-starter*
     >    - 扩展info端点
     > 8. *base-eureka-spring-boot-starter*
     >    - 支持eureka主从开关以及新增元数据
     >    - 支持eureka拉入拉出
     > 9. *base-fastjson-spring-boot-starter*
     >    - fastjson封装
     > 10. *base-feign-spring-boot-starter*
     >
     >    - 支持hystrix和sentinel注解fallback（默认：打印fallback日志，可以定制返回结果集）
     >    - 支持feign日志，header传递，以及封装okhttp等
     >    - 新增@FeignClient缓存，便于动态新增Eager加载
     >
     > 11. *base-framework-spring-boot-starter*
     >     - 封装framework常用的使用
     > 12. *base-graceful-spring-boot-starter*
     >     - 支持tomcat和undretow优雅停机（2.3.0之前）
     > 13. *base-health-check-spring-boot-starter*
     >     - 新增常用的健康检查
     > 14. *base-influx-spring-boot-starter*
     >     - 封装influx使用
     > 15. *base-jackson-spring-boot-starter*
     >     - 封装统一jackson
     > 16. *base-logger-spring-boot-starter*
     >     - 支持动态变更日志级别
     >     - 集成log4j2
     > 17. *base-mail-spring-boot-starter*
     >     - 支持常用邮件处理
     > 18. *base-metric-spring-boot-starter*
     >     - 常用资源池监控metric
     > 19. *base-mongo-spring-boot-starter*
     >     - 支持mongo封装
     > 20. *base-mq-lock-spring-boot-starter* & *base-mq-spring-boot-starter*
     >     - activemq和rabbitmq封装
     > 21. *base-multi-mybatis-spring-boot-starter*
     >     - 支持base-base-mybatis-spring-boot-starter以及多数据源
     > 22. *base-multi-shardingsphere-spring-boot-starter*
     >     - 支持shardingsphere多数据源
     > 23. *base-mybatis-spring-boot-starter*
     >     - 支持mybatis主从数据源
     > 24. *base-nacos-spring-boot-starter*
     >     - 支持nacos主从开关以及新增元数据
     >     - 支持nacos拉入拉出
     > 25. *base-quartz-lock-spring-boot-starter*
     >     - 分布式quartz lock starter
     > 26. *base-quartz-spring-boot-starter*
     >     - 基于jdk quartz封装（yml统一管理配置使用）
     > 27. *base-redis-spring-boot-starter*
     >     - jedis，spring-data，redission等封装
     > 28. *base-rest-template-spring-boot-starter*
     >     - rest template封装使用
     > 29. *base-retrofit-spring-boot-starter*
     >     - retrofit封装使用
     > 30. *base-ribbon-spring-boot-starter*
     >     - 自动初始化加载@FeignClient下的服务以及设置默认的ribbon重试策略
     >     - 集成ribbon以及spring loadbalance
     > 31. *base-sentinel-spring-boot-starter*
     >     - sentinel cluster封装（配合apollo sentinel整改）
     > 32. *base-swagger-spring-boot-starter*
     >     - 集成knife4j，含授权
     > 33. *base-thread-pool-spring-boot-starter*
     >     - 使用properties/yml统一管理线程池，避免项目各地方线程池乱用
     >     - 支持通过apollo动态变更线程池
     > 34. *base-webflux-spring-boot-starter*
     >     - WebExchange上下文传递以及WebClient封装
     > 35. *base-xxl-job-spring-boot-starter*
     >     - xxl-job starter服务

   - **base-spring-cloud-framework**

     基础springboot包，快速搭建springboot项目

   - **base-platform-bom**

     基础bom包，统一管理项目依赖Jar

   - **base-skeleton-initializr（未开源）**

     base脚手架，快速搭建项目（分层模式，DDD）

3. ### 迭代升级

   base-* 2020.x.x 支持（同步更新springcloud 2020.x.x）

4. ### 规划base-plus-*（暂不开源）

   > **蓝绿灰度**
   >
   > - 可以参考nepxion，见总结[Nepxion整理](https://github.com/liaomengge/base-doc/blob/main/Nepxion.md)
   >
   > **无损流量**
   >
   > - 无损上下线，provider上下线，及时通知对应consumer刷新调用实例
   >
   > **预热，动态权重**
   >
   > - 依据provider实例运行状态，打分决策（实例启动时间；cpu、内存、磁盘等负载；线程池情况等），分配不同的权重
   >
   > ......

5. ### 待开源项目

   > - [X-Job](https://github.com/liaomengge/base-doc/blob/main/X-Job.md) 【基于xxl-job 2.3.0版本二开】
   > - [X-Gateway](https://github.com/liaomengge/base-doc/blob/main/X-Gateway.md) 【界面类似apisix功能，依赖springcloud gateway H版本开发】

6. ### 附

   [gradle mybatis自动生成](https://github.com/liaomengge/base-mybatis-generator-plugin)

   [mybatis插件定制](https://github.com/liaomengge/base-mybatis-plugin)

