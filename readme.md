[TOC]

# 简介
boot4j是一款基于SpringBoot企业后台解决方案

# 依赖版本
spring boot 1.5.7.RELEASE
# 0.0.1-beta1
1. 实现ehcache本地缓存，以及监听本地缓存的使用情况
2. 实现redis远端缓存
3. 基于Spring Security的权限控制、Oauth2.0认证
4. 将Session保存到redis
5. 基于Hibernate的后台持久化
6. 使用jpa链接Mysql数据库
7. 基于Swagger2接口调试
8. 用于对Bean的值进行加密的注解，为做演示，暂时只支持字符字段的加密 @see ValueEncrypt.java
9. 标准的基于领域模型的开发
10.支持一键式集成测试
11.支持JdbcTokenStore和RedisTokenStore灵活使用，如果存在Redis配置，则使用RedisTokenStore

# 优化
1.@RedisCacheable：使用Redis远端缓存，@Cacheable使用EhCache本地缓存，优先使用本地缓存(✅)
2.如果Redis不存在，则自动将缓存切换到本地缓存。(✅)
3.如果Redis存在，则根据@RedisCacheable注解，按需切换缓存。(✅)
4.即使使用了@RedisCacheable注解，但是当系统不使用Redis的时候，自动切换到EhCache，效果同@Cacheable。(✅)
5.Dubbo服务化和普通@Service服务能够灵活切换。当开启Dubbo服务化时，则使用Dubbo服务，需要启动Zookeeper。

# 现象
> 手工在数据库中修改数据，后台没有及时查询到真实数据，需要等待约2分钟。
```
解释：Hibernate有三个状态，即：
1.瞬时态：Transient, 刚new出来的对象，没有保存到数据库。
2.持久态：Persistent, 已经保存到数据库中。
3.离线态：Detached, 数据库中有数据，但是Session中不存在该对象。
```

# 测试
> 统一的测试入口：cn.boot4j.ProductDemoPostmanTests
```
右键，run -> Junit Test
```

# 执行
```
git https://github.com/iBoot4j/boot4j.git
mvn clean 
mvn package
```