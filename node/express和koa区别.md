### 区别

- **Express**框架的next不返回promise，**Koa**框架的next会返回一个promise
  - 会导致，当其中一个中间件是异步请求的时候，Express没有Koa那么好处理
- next函数的作用就是调用下一个中间件。