笔记少...看文档吧

### Node程序传递参数

- *node .\01参数.js qiuhongwei age=18* 
  - 后面两个就是参数
  - 可以在进程process.argv里面获取

### 特殊的全局对象

![1643550270632](.\assets\1643550270632.png)

### node和浏览器全局对象

- node有模块化的概念
- 当var name  = 'aaa'；window.aa可以拿到，但是global全局对象拿不到aa，因为在浏览器顶层的是没有模块化的概念的
- 那为什么node process在global中，因为做了处理

### 模块

#### path

- ```javascript
  //文件夹和路径 03常见的内置模块/01path.js
  const path = require('path');
  /**
   * resolve方法可以拼接路径，可以根据不同的操作系统来拼接路径
   * 
   * 比如windows 路径分隔符 可以是 \\ \ /，mac linux是/
   * 如果我们直接字符串拼接的话，那么就属于硬编码的，就不能应付不同的操作系统
   */
  const basePath = '/User';
  const fileName = 'qiuhongwei.txt';
  
  const o = path.resolve(basePath, fileName);
  console.log(o);//D:\User\qiuhongwei.txt
  
  /**
   * 获取路径信息
   * 打印信息
   * /User/pc      
   * qiuhongwei.txt
   * .txt
   */
  const file = '/User/pc/qiuhongwei.txt';
  console.log(path.dirname(file));//目录名字，获取当前文件所处于的文件路径
  console.log(path.basename(file));//文件名字
  console.log(path.extname(file));//扩展名
  
  // 获取当前文件所在的文件夹绝对路径
  console.log(__dirname)//D:\qiuhongweiProject\learnNode\03常见的内置模块
  
  /**
   * 拼接路径的话 
   * path有属性join和resolve
   * 区别是 resolve会区分参数是否有路径分隔符
   */
  
  // const basePath1 = '/User/path';
  // const fileName1 = 'qiuhongwei.txt';
  console.log(path.join('/User/path', 'qiuhongwei.txt'));// \User\path\qiuhongwei.txt
  console.log(path.join('User/path', 'qiuhongwei.txt'));// User\path\qiuhongwei.txt
  console.log(path.join('../User/path', 'qiuhongwei.txt'));// ..\User\path\qiuhongwei.txt
  console.log(path.join('./User/path', 'qiuhongwei.txt'));// User\path\qiuhongwei.txt
  
  console.log(path.resolve('/User/path', 'qiuhongwei.txt'));// D:\User\path\qiuhongwei.txt
  console.log(path.resolve('User/path', 'qiuhongwei.txt'));// D:\qiuhongweiProject\learnNode\03常见的内置模块\User\path\qiuhongwei.txt
  console.log(path.resolve('../User/path', 'qiuhongwei.txt'));// D:\qiuhongweiProject\learnNode\User\path\qiuhongwei.txt
  console.log(path.resolve('./User/path', 'qiuhongwei.txt'));// D:\qiuhongweiProject\learnNode\03常见的内置模块\User\path\qiuhongwei.txt
  // __dirname 当前文件 目录 
  console.log(path.resolve(__dirname, 'qiuhongwei.txt'));// D:\qiuhongweiProject\learnNode\03常见的内置模块\qiuhongwei.txt
  console.log(path.resolve(__dirname, '/qiuhongwei.txt'));// qiuhongwei.txt
  ```

- process.cwd()，文件中的任何相对路径，都是相对process.cwd(),process.cwd()就是执行命令的文件中位置

  ```javascript
  /**
   * process.cwd
   * 在learnnode文件中执行 node .\03常见的内置模块\01path.js
   * 此时，process.cwd()指的是执行命令的文件中位置
   */
  console.log(process.cwd())//\qiuhongweiProject\learnNode
  
  // 假设你在某个文件夹的根目录require('./xxx')，也在根目录执行代码，那么就可以正确获取到xxx文件，但是在其他地方就是不行的，
  ```

  



### Node中使用SQL

#### 介绍

- **为什么**：navicat是SQL的gui软件，是用来测试的，正常项目中，操作数据库是使用代码来实现的。
- **Node代码如何执行SQL**，：
  - mysql：最早的Node连接MySQL的数据库驱动
  - mysql2：在mysql的基础之上，进行了很多的优化、改进
- **mysql2优点**
  - 更快/更好的性能； 
  - Prepared Statement（预编译语句）
    - 提高性能：将创建的语句模块发送给MySQL，然后MySQL编译（解析、优化、转换）语句模块，并且存储它但是不执行，之 后我们在真正执行时会给?提供实际的参数才会执行；就算多次执行，也只会编译一次，所以性能是更高的；  
    - 防止SQL注入：之后传入的值不会像模块引擎那样就编译，那么一些SQL注入的内容不会被执行；or 1 = 1不会被执行
  - 支持Promise，所以我们可以使用async和await语法 

#### ORM

- 对象关系映射（英语：Object Relational Mapping，简称ORM，或O/RM，或O/R mapping），是一种程序 设计的方案 
  -  从效果上来讲，它提供了一个可在编程语言中，使用 虚拟对象数据库 的效果（大概就是新建一个对象映射数据库，然后使用对象的方法操作数据，从而不用编写sql语句）
  -  比如在Java开发中经常使用的ORM包括：Hibernate、MyBatis； 
- Node当中的ORM我们通常使用的是 sequelize; 
  - Sequelize是用于Postgres，MySQL，MariaDB，SQLite和Microsoft SQL Server的基于Node.js 的 ORM；
  - 它支持非常多的功能
-  将Sequelize和MySQL一起使用，那么我们需要先安装两个东西： 
  -  mysql2：sequelize在操作mysql时使用的是mysql2；  
  -  sequelize：使用它来让对象映射到表中； 







