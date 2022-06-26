### 看官方文档很重要！！

### 介绍

- **为什么**：Node的http内置模块可以搭建Web服务器，但是操作起来比较麻烦，比如url，method，逻辑之类的判断。
- **原理**：原理就是中间件，中间件就是回调函数。

### 安装

![1644415186223](.\assets\1644415186223.png)

### 中间件

- **Express**的原理就是中间件， **Express**是一个路由和中间件的Web框架 
- **本质**： 中间件的本质是传递给express的一个回调函数； 
- **执行任务**
  -  执行任何代码； 
  -  更改请求（request）和响应（response）对象； 
  -  结束请求-响应周期（返回数据）；  
  -  调用栈中的下一个中间件 ；
-  如果当前中间件功能没有结束请求-响应周期，则必须调用next()将控制权传递给下一个中间件功能，否则，请求 将被挂起。 
  - 没有结束请求，就是没有response.end/next()，next作用就是传递给下一个中间件
  - 其中多个中间件可以同时被触发，但是不能同时res.end。
  - 中间件是根据路由匹配的，如果是app.use(callback)，那么就是匹配所有的路由，多个中间件如果匹配到路径，中间件里面必须有next进行调用下一个中间件，且最后的中间件要有res.end()来结束响应周期。

### 解析方式

-  post请求

  - JSON方式请求

    - expres内置的中间件，app.use(express.json());
    - 使用body-parser来完成;

  - form表单方式请求

    - app.use(express.urlencoded({extended:true}))

  - from-data请求方式

    -  multer 模块来处理

    - ```javascript
      const multer = require('multer');
      const upload = multer();
      app.use(upload.any());
      ```

### 静态资源服务器

- **静态资源服务器**：打包后的文件就是静态资源服务器

- Nginx可以部署静态资源服务器，Node也可以

  ```javascript
  const express = require('express');
  
  const app = express();
  // build就是打包后的文件
  app.use(express.static('./build'));
  
  app.listen(8000, () => {
    console.log("路由服务器启动成功~");
  });
  ```

  