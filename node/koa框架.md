### 介绍

- 用node.js为基础的新一代Web框架
- koa是express同一个团队开发的一个新的Web框架：  
- Koa旨在为Web应用程序和API提供更小、更丰富和更强大的能力； 
- 相对于express具有更强的异步处理能力； 
-  Koa的核心代码只有1600+行，是一个更加轻量级的框架，我们可以根据需要安装和使用中间件； 

### 路由的使用

-  koa官方并没有给我们提供路由的库，我们可以选择第三方 库：koa-router 
-  在app中将router.routes()注册为中间件： 
-  注意：allowedMethods用于判断某一个method是否支持： 
  - 如果我们请求 get，那么是正常的请求，因为我们有实 现get； 
  -  如果我们请求 link、copy、lock，那么久自动报错： Not Implemented，状态码：501；  
  -  如果我们请求 put、delete、patch，那么就自动报错： Method Not Allowed，状态码：405； 

### 参数解析

- params/query（get请求，query就是url后面的?name=asdads&age=123），params就是xx/123
  - **URL**： localhost:8000/users/abc?name=qiuhongwei&age=123 
  - 使用koa-router路由插件解析，npm install koa-router
  - 解析后从ctx.request里面获取url,params,query
- json/urlencoded解析
  - 使用 npm install koa-**bodyparser**
- form-data
  - 使用 npm install koa-multer

