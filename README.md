# qbgc-test-zuul
# Zuul
### 功能：
* 路由转发 （主要功能）
* 过滤器（主要功能）
* Authentication
* Insights
* Stress Testing
* Canary Testing
* Dynamic Routing
* Service Migration
* Load Shedding
* Security
* Static Response handling
* Active/Active traffic management
* ***
##### 路由转发：
* 添加zuul的依赖
* 添加注解@EnableZuulProxy，开启Zuul功能
* 配置分发的路由：
```
zuul:
  routes:
    api-feign:
      path: /api/feign/**
      serviceId: qbgc-test-feign
    api-ribbon:
      path: /api/ribbon/**
      serviceId: qbgc-test-ribbon
```
* 例子访问http://gaochao:7002/api/ribbon/ribbon
***
##### 过滤器
* 新建一个过滤类继承ZuulFilter
* 然后在里面添加逻辑即可
* 意外收获：如获取请求处理之后发送到前台显示。
```
    // 获取当前上下文
    RequestContext context = RequestContext.getCurrentContext();
    // 获取request
    HttpServletRequest request = context.getRequest();
    Object token = request.getParameter("token");
    if (token == null) {
        context.setSendZuulResponse(false);
        context.setResponseStatusCode(401);
        try {
            context.getResponse().getWriter().write("token is empty");
        } catch (IOException e) {
            e.printStackTrace();
        }
        return null;
    }
```
***
