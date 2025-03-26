ch02通过component的方式来配置授权服务器，配置效果与ch01一致。

## component说明

1. **authorizationServerSecurityFilterChain**

   授权服务器的过滤器链。该过滤器链中处理与授权服务相关的请求，要求所有请求需经过认证，未认证请求跳转/login页面。

   注意：授权服务器过滤器链需要在Spring security过滤器链之前。

2. **defaultSecurityFilterChain**

   Spring Security过滤器链，要求所有请求需经过认证。

3. **userDetailsService**

   user详情服务，提供对user的查询功能。

4. **registeredClientRepository**

   client详情服务，提供对client的查询功能。

5. **jwkSource**

   密钥信息，用于生成token的加密器和解密器。一些场景下，token的加密器和解密器不需要jwkSource。

6. **authorizationServerSettings**

   授权服务请求路径配置，不是必须。

## 总结

授权服务配置核心关注的点：

1. 授权服务过滤器链
2. Spring Security过滤器链
3. user详情查询服务
4. clietn详情查询服务
5. token的加密器和解密器

