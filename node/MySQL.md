### 账号密码

- 账号：root
- 密码：123456

### 介绍

- **为什么要使用数据库**：
  -  任何的软件系统都需要存放大量的数据，这些数据通常是非常复杂和庞大的；
  -  比如用户信息包括姓名、年龄、性别、地址、身份证号、出生日期等等； 
  -  比如商品信息包括商品的名称、描述、价格（原价）、分类标签、商品图片等等 
  -  比如歌曲信息包括歌曲的名称、歌手、专辑、歌曲时长、歌词信息、封面图片等等； 
- **为什么不直接存储到文件系统中**
  - 可以直接将数据直接存到文件系统中，比如writer存入，但有缺点
  - 比如数据庞大的时候，数据之间是存在关系的，要多张表关联起来，这时候文件系统就很难操作
  - 文件系统很难进行数据共享，比如一个数据库需要为多个程序服务，如何进行很好的数据共享；
  - 需要考虑如何进行数据的高效备份、迁移、恢复；   
  - 文件系统难以对数据进行增删改查中的复杂操作（虽然一些简单确实可以），并且保证单操作的原子性； 
- **什么是保证原子性？**
  - 首先关系型数据库支持事务，对数据的访问更加安全，保证了原子性
  - 大概流程就是：当你对数据库进行操作时，操作的时候就加上锁，这时候别人就操作不了了，
  - 这样就是支持事务，对数据的访问更加安全，保证了原子性

### 关系型数据库

-  关系型数据库：MySQL、Oracle、DB2、SQL Server、Postgre SQL等 
-  关系型数据库通常我们会创建很多个二维数据表； 
-  数据表之间相互关联起来，形成一对一、一对多、多对对等关系；  
-  之后可以利用SQL语句在多张表中查询我们所需的数据； 
-  支持事务，对数据的访问更加的安全； 

### 非关系型的数据库

-  非关系型数据库的英文其实是Not only SQL，也简称为NoSQL，MongoDB、Redis、Memcached、HBse等 
-  相当而已非关系型数据库比较简单一些，存储数据也会更加自由（甚至我们可以直接将一个复杂的json对象直接塞入到数据库中）；  
-  NoSQL是基于**Key-Value**的对应关系，并且查询的过程中不需要经过SQL解析，所以性能更高 
-  NoSQL通常**不支持事务**，需要在自己的程序中来保证一些原子性的操作； 

### MySQL

-  MySQL是一个关系型数据库，其实本质上就是一款软件、一个程序： 
-  这个程序中管理着多个数据库； 
-  每个数据库中可以有多张表 
-  每个表中可以有多条数据； 

###  终端连接数据库

- **方式1**：

  ```javascript
   mysql -uroot -p123456
  ```

  

- **方式2**： 

  ```javascript
  mysql -uroot -p Enter password: your password 
  ```

- 详情终端操作数据 可以查看文档（毕竟一般都是用GUI来操作的，也就是navicat的）

### GUI工具介绍

-  我们会发现在终端操作数据库有很多不方便的地方：
  - 语句写出来没有高亮，并且不会有任何的提示； 
  -  复杂的语句分成多行，格式看起来并不美观，很容易出现错误 
  -  终端中查看所有的数据库或者表非常的不直观和不方便 
-  所以在开发中，我们可以借助于一些GUI工具来帮助我们连接上数据库，之后直接在GUI工具中操作就会非常方便。 
-  常见的MySQL的GUI工具有很多，这里推荐几款： 
  -  Navicat
  -  SQLYog：一款免费的SQL工具； 
  -  TablePlus：常用功能都可以使用，但是会多一些限制（比如只能开两个标签页）； 

### SQL语句

-  我们希望操作数据库（特别是在程序中），就需要有和数据库沟通的语言，这个语言就是SQL： 
  - SQL语句可以用于对数据库进行操作； 
  - 使用SQL编写出来的语句，就称之为SQL语句； 
  -  SQL是Structured Query Language，称之为结构化查询语言，简称SQL； 
-  SQL语句的常用规范 
  -  通常关键字是大写的，比如CREATE、TABLE、SHOW等等； 
  -  一条语句结束后，需要以 ; 结尾 
  -  如果遇到关键字作为表明或者字段名称，可以使用``包 
-  常见的SQL语句我们可以分成四类： 
  -  **DDL（Data Definition Language）：数据定义语言**。 可以通过DDL语句对数据库或者表进行：创建、删除、修改等操作；  
  -  **DML（Data Manipulation Language）：数据操作语言。** 可以通过DML语句对表进行：添加、删除、修改等操作  
  -  **DQL（Data Query Language）：数据查询语言 。** 可以通过DQL从数据库中查询记录；（重 
  -  **DCL（Data Control Language）：数据控制语言。** 对数据库、表格的权限进行相关访问控制操作； 

### 编辑数据库

![1644643447346](.\assets\1644643447346.png)

- 其中字符集就是存储到数据库的编码形式，为什么不适用utf8，因为utf8不识别emoji表情，所以使用utf8mb4
- 排序规则，就是根据..暂时没有搜索到

### SQL的数据类型（看文档）

- 数字类型
  -  整数数字类型：INTEGER，INT，SMALLINT，TINYINT，MEDIUMINT，BIGINT； ![1644657092164](.\assets\1644657092164.png)
  -  浮点数字类型：FLOAT，DOUBLE（FLOAT是4个字节，DOUBLE是8个字节）； 
  -  精确数字类型：DECIMAL，NUMERIC（DECIMAL是NUMERIC的实现形式）；
- 日期类型
  -  YEAR以YYYY格式显示值
    - 范围 1901到2155，和 0000 
  -  DATE类型用于具有日期部分但没有时间部分的值
    -  DATE以格式YYYY-MM-DD显示值 ； 
    -  支持的范围是 '1000-01-01' 到 '9999-12-31'； 
  -  DATETIME类型用于包含日期和时间部分的值： 
    -  DATETIME以格式'YYYY-MM-DD hh:mm:ss'显示值； 
    -  支持的范围是1000-01-01 00:00:00到9999-12-31 23:59:5 
  -  TIMESTAMP数据类型被用于同时包含日期和时间部分的值： 
    -  TIMESTAMP以格式'YYYY-MM-DD hh:mm:ss'显示值 
    -  但是它的范围是UTC的时间范围：'1970-01-01 00:00:01'到'2038-01-19 03:14:07'; 
- 字符串类型
  -  CHAR类型在创建表时为固定长度，长度可以是0到255之间的任何值； 
    -  在被查询时，会删除后面的空格； 
  -  VARCHAR类型的值是可变长度的字符串，长度可以指定为0到65535之间的值； 
    -  在被查询时，不会删除后面的空格； 
  -  BINARY和VARBINARY 类型用于存储二进制字符串，存储的是字节字符串； 
  -  BLOB用于存储大的二进制类型 
  -  TEXT用于存储大的字符串类型 

### 表约束



### 数据库的操作

#### DDL ：数据定义语言

```mysql
1、数据表的操作
# 查看所有的表
SHOW TABLES;

# 新建表
CREATE TABLE IF NOT EXISTS `students` (
	`name` VARCHAR(10) NOT NULL,
	`age` int,
	`score` int,
	`height` DECIMAL(10,2),
	`birthday` YEAR,
	`phoneNum` VARCHAR(20) UNIQUE
);

CREATE TABLE IF NOT EXISTS `studentss` (
	`name` VARCHAR(10),
	`age` int,
	`score` int
);

# 删除表
DROP TABLE IF EXISTS `students`;

# 查看表的结构
DESC students;

# 查看创建表的SQL语句
SHOW CREATE TABLE `students`;

-- CREATE TABLE `students` (
--   `name` varchar(10) DEFAULT NULL,
--   `age` int DEFAULT NULL,
--   `score` int DEFAULT NULL
-- ) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci

# 完整的创建表的语法
CREATE TABLE IF NOT EXISTS `users`(
	id INT PRIMARY KEY AUTO_INCREMENT,
	name VARCHAR(20) NOT NULL,
	age INT DEFAULT 0,
	phoneNum VARCHAR(20) UNIQUE DEFAULT '',
	createTime TIMESTAMP
);


# 修改表
# 1.修改表的名字
ALTER TABLE `users` RENAME TO `user`;
# 2.添加一个新的列
ALTER TABLE `users` ADD `updateTime` TIMESTAMP;
# 3.修改字段的名称
ALTER TABLE `users` CHANGE `phoneNum` `telPhone` VARCHAR(20);
# 4.修改字段的类型
ALTER TABLE `user` MODIFY `name` VARCHAR(30);
# 5.删除某一个字段
ALTER TABLE `user` DROP `age`;


# 补充
# 根据一个表结构去创建另外一张表
CREATE TABLE `user2` LIKE `user`;
# 根据另外一个表中的所有内容，创建一个新的表 不过有一些机构是没有复制的，比如主键之类的
CREATE TABLE `user3` (SELECT * FROM `user`); 

2、数据库的操作
# 查看所有的数据库
SHOW DATABASES;

# 选择某一个数据库
USE qiuhongweihub;

# 查看当前正在使用的数据库
SELECT DATABASE();

# 创建一个新的数据库
-- CREATE DATABASE douyu;
-- CREATE DATABASE IF NOT EXISTS douyu;
-- CREATE DATABASE IF NOT EXISTS huya DEFAULT CHARACTER SET utf8mb4
-- 				COLLATE utf8mb4_0900_ai_ci;

# 删除数据库
DROP DATABASE IF EXISTS douyu;

# 修改数据库的编码
ALTER DATABASE huya CHARACTER SET = utf8 
				COLLATE = utf8_unicode_ci;
```

#### DML 数据操作语言

```mysql
 # 插入数据
INSERT INTO `user` VALUES (110, 'why', '020-110110', '2020-10-20', '2020-11-11');
INSERT INTO `user` (name, telPhone, createTime, updateTime)
						VALUES ('kobe', '000-1111111', '2020-10-10', '2030-10-20');
						
INSERT INTO `user` (name, telPhone)
						VALUES ('lilei', '000-1111112');

# 需求：createTime和updateTime可以自动设置值，并且updateTime，每次插入数据的时候会更新(DDL)
ALTER TABLE `user` MODIFY `createTime` TIMESTAMP DEFAULT CURRENT_TIMESTAMP;
ALTER TABLE `user` MODIFY `updateTime` TIMESTAMP DEFAULT CURRENT_TIMESTAMP					ON UPDATE CURRENT_TIMESTAMP;

INSERT INTO `user` (name, telPhone)
						VALUES ('hmm', '000-1111212');

INSERT INTO `user` (name, telPhone)
						VALUES ('lucy', '000-1121212');


# 删除数据
# 删除所有的数据
DELETE FROM `user`;
# 删除符合条件的数据
DELETE FROM `user` WHERE id = 110;

# 更新数据
# 更新所有的数据 因为是对标的数据操作 所以不是update table `user` set name = 'xxx'
UPDATE `user` SET name = 'lily', telPhone = '010-110110';
# 更新符合条件的数据
UPDATE `user` SET name = 'lily', telPhone = '010-110110' WHERE id = 115;
```

#### DQL 数据查询语言

```mysql
# 创建products的表
CREATE TABLE IF NOT EXISTS `products` (
	id INT PRIMARY KEY AUTO_INCREMENT,
	brand VARCHAR(20),
	title VARCHAR(100) NOT NULL,
	price DOUBLE NOT NULL,
	score DECIMAL(2,1),
	voteCnt INT,
	url VARCHAR(100),
	pid INT
);

# 1.基本查询
# 查询表中所有的字段以及所有的数据
SELECT * FROM `products`;
# 查询指定的字段
SELECT title, price FROM `products`;
# 对字段结果起一个别名
SELECT title as phoneTitle, price as currentPrice FROM `products`;


# 2.where条件
# 2.1. 条件判断语句
# 案例：查询价格小于1000的手机
SELECT title, price FROM `products` WHERE price < 1000;
# 案例二：价格等于999的手机
SELECT * FROM `products` WHERE price = 999;
# 案例三：价格不等于999的手机
SELECT * FROM `products` WHERE price != 999;
SELECT * FROM `products` WHERE price <> 999;
# 案例四：查询品牌是华为的手机
SELECT * FROM `products` WHERE brand = '华为';

# 2.2. 逻辑运算语句
# 案例一：查询1000到2000之间的手机
SELECT * FROM `products` WHERE price > 1000 AND price < 2000;
SELECT * FROM `products` WHERE price > 1000 && price < 2000;
# BETWEEN AND 包含等于
SELECT * FROM `products` WHERE price BETWEEN 1099 AND 2000;

# 案例二：价格在5000以上或者是品牌是华为的手机
SELECT * FROM `products` WHERE price > 5000 || brand = '华为';

# 将某些值设置为NULL
-- UPDATE `products` SET url = NULL WHERE id >= 85 and id <= 88;
# 查询某一个值为NULL
SELECT * FROM `products` WHERE url IS NULL;
-- SELECT * FROM `products` WHERE url = NULL;
-- SELECT * FROM `products` WHERE url IS NOT NULL;

# 2.3.模糊查询 %任意个 _任意一个
SELECT * FROM `products` WHERE title LIKE '%M%';
SELECT * FROM `products` WHERE title LIKE '%P%';
SELECT * FROM `products` WHERE title LIKE '_P%';


# 3.对结果进行排序
SELECT * FROM `products` WHERE brand = '华为' || brand = '小米' || brand = '苹果';
SELECT * FROM `products` WHERE brand IN ('华为', '小米', '苹果') 
ORDER BY price ASC, score DESC;


# 4.分页查询
# LIMIT limit OFFSET offset;
# Limit offset, limit;
SELECT * FROM `products` LIMIT 20 OFFSET 0;
SELECT * FROM `products` LIMIT 40 OFFSET 20;
SELECT * FROM `products` LIMIT 40, 20;

# 1.聚合函数的使用

# 求所有手机的价格的总和 别名
SELECT SUM(price) totalPrice FROM `products`;

# 求所有手机的价格的总和
SELECT SUM(price) FROM `products`;

# 求一下华为手机的价格的总和
SELECT SUM(price) FROM `products` WHERE `brand` = '华为';

# 求华为手机的平均价格
SELECT AVG(price) FROM `products` WHERE brand = '华为';

# 最高手机的价格和最低手机的价格
SELECT MAX(price) FROM `products`;
SELECT MIN(price) FROM `products`;

# 求华为手机的个数
SELECT COUNT(*) FROM `products` WHERE brand = '华为';
SELECT COUNT(*) FROM `products` WHERE brand = '苹果';
SELECT COUNT(url) FROM `products` WHERE brand = '苹果';

SELECT COUNT(price) FROM `products`;
SELECT COUNT(DISTINCT price) FROM `products`;

# 2.GROUP BY的使用 为什么选择brand，因为是根据brand分组的，所以同一组的brand都一样，可以显示
# 如果是选择title，根据brand分组，那么sql就不知道显示哪个title
SELECT brand, AVG(price), COUNT(*), AVG(score) FROM `products` GROUP BY brand;


# 3.HAVING的使用 是对分组后的结果进行筛选，也就是groupby，where是对表进行筛选的
SELECT brand, AVG(price) avgPrice, COUNT(*), AVG(score) FROM `products` GROUP BY brand HAVING avgPrice > 2000;


# 4.需求：求评分score > 7.5的手机的，平均价格是多少？
# 升级：平均分大于7.5的手机，按照品牌进行分类，然后求出平均价格。
SELECT brand, AVG(price) FROM `products` WHERE score > 7.5 GROUP BY brand;
```

### 多表

#### 多表插入

- 现在假设有A和B表，A是products表，B是brand表，A表外键brand_id 与 B表外键id关联

- 左连接是以左边的表为主，右连接是以右边的表为主，查询的前提是以on的条件筛选，筛选后，会根据外键来将表合并（情况，一对一  一对多  多对多），如果没有对应的，那么合并的其中一部分（就是灭有对应那部分的内容都是null）。

- 下面情况就是A表和B表的对应关系，是一对多

  - **左1是左连接**

  - 查询所有的手机（包括没有品牌信息的手机）以及对应的品牌 null 

  - 所以图中是 A和B的相交 + A

    ```mysql
    SELECT * FROM `products` LEFT OUTER JOIN `brand` ON products.brand_id = brand.id
    ```

    

  - **左2是左连接**，因为where条件，所以筛选出brand.id=null；

  - 查询所有的手机（A表），然后将对应的品牌为null的数据筛选出来

  - 所以图中是 A和B的相交 + A - A和B的相交 = A

    ```mysql
    SELECT * FROM `products` LEFT JOIN `brand` ON products.brand_id = brand.id WHERE brand.id IS NULL;
    ```

  - **右1是右连接**

  - 筛选的是，所有品牌对应的手机的表，还有品牌对应手机但是为null的表的合集

  - 所以图中是A和B的交集和B

  - ```mysql
    SELECT * FROM `products` RIGHT OUTER JOIN `brand` ON products.brand_id = brand.id;
    ```

    

  - **右1是右连接**

  - 筛选的是，所有品牌对应的手机的表，还有筛选对应手机为null的表，也就是查询没有对应手机的品牌信息

  - ```mysql
    SELECT * FROM `products` RIGHT JOIN `brand` ON products.brand_id = brand.id WHERE products.brand_id IS NULL;
    ```

  - **中间的是内连接**

  - 内连接相交的部分并且没有null值，查询的是手机对应的品牌合集表 并且没有null值

  - ```mysql
    SELECT * FROM `products` JOIN `brand` ON products.brand_id = brand.id;
    ```

  - **下左是全连接**

  - SQL规范中，全连接是full join，但是mysql没有实现，UNION联合的话会去重

  - ```mysql
    (SELECT * FROM `products` LEFT OUTER JOIN `brand` ON products.brand_id = brand.id)
    UNION
    (SELECT * FROM `products` RIGHT OUTER JOIN `brand` ON products.brand_id = brand.id)
    ```

  - **下右是全连接**

  - ```mysql
    (SELECT * FROM `products` LEFT OUTER JOIN `brand` ON products.brand_id = brand.id WHERE brand.id IS NULL)
    UNION
    (SELECT * FROM `products` RIGHT OUTER JOIN `brand` ON products.brand_id = brand.id WHERE products.brand_id IS NULL)
    ```

    

- ![1645264292676](D:\qiuhongweiProject\note\node\assets\1645264292676.png)

#### 多表设计

```mysql
#外键的作用，当使用多表设计的时候，外键的作用是约束 只有外键才可以实现多表查询
# 1.创建brand的表和插入数据
CREATE TABLE IF NOT EXISTS `brand`(
	id INT PRIMARY KEY AUTO_INCREMENT,
	name VARCHAR(20) NOT NULL,
	website VARCHAR(100),
	phoneRank INT
);

#创建的时候创建外键
FOREIGN KEY (brand_id) REFERENCES brand(id) 

INSERT INTO `brand` (name, website, phoneRank) VALUES ('华为', 'www.huawei.com', 2);
INSERT INTO `brand` (name, website, phoneRank) VALUES ('苹果', 'www.apple.com', 10);
INSERT INTO `brand` (name, website, phoneRank) VALUES ('小米', 'www.mi.com', 5);
INSERT INTO `brand` (name, website, phoneRank) VALUES ('oppo', 'www.oppo.com', 12);

INSERT INTO `brand` (name, website, phoneRank) VALUES ('京东', 'www.jd.com', 8);
INSERT INTO `brand` (name, website, phoneRank) VALUES ('Google', 'www.google.com', 9);


# 2.给brand_id设置引用brand中的id的外键约束
# 添加一个brand_id字段
ALTER TABLE `products` ADD `brand_id` INT;
-- ALTER TABLE `products` DROP `brand_id`;

# 修改brand_id为外键
ALTER TABLE `products` ADD FOREIGN KEY(brand_id) REFERENCES brand(id);

# 设置brand_id的值
UPDATE `products` SET `brand_id` = 1 WHERE `brand` = '华为';
UPDATE `products` SET `brand_id` = 2 WHERE `brand` = '苹果';
UPDATE `products` SET `brand_id` = 3 WHERE `brand` = '小米';
UPDATE `products` SET `brand_id` = 4 WHERE `brand` = 'oppo';

# 3.修改和删除外键引用的id
UPDATE `brand` SET `id` = 100 WHERE `id` = 1;


# 4.修改brand_id关联外键时的action
# 4.1.获取到目前的外键的名称
SHOW CREATE TABLE `products`;


-- CREATE TABLE `products` (
--   `id` int NOT NULL AUTO_INCREMENT,
--   `brand` varchar(20) DEFAULT NULL,
--   `title` varchar(100) NOT NULL,
--   `price` double NOT NULL,
--   `score` decimal(2,1) DEFAULT NULL,
--   `voteCnt` int DEFAULT NULL,
--   `url` varchar(100) DEFAULT NULL,
--   `pid` int DEFAULT NULL,
--   `brand_id` int DEFAULT NULL,
--   PRIMARY KEY (`id`),
--   KEY `brand_id` (`brand_id`),
--   CONSTRAINT `products_ibfk_1` FOREIGN KEY (`brand_id`) REFERENCES `brand` (`id`)
-- ) ENGINE=InnoDB AUTO_INCREMENT=109 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci

# 4.2.根据名称将外键删除掉
ALTER TABLE `products` DROP FOREIGN KEY products_ibfk_1;

# 4.2.重新添加外键约束  下面的设置是更新的时候可以联动 不给删除
ALTER TABLE `products` ADD FOREIGN KEY (brand_id) REFERENCES brand(id) 
ON UPDATE CASCADE
ON DELETE RESTRICT;

UPDATE `brand` SET `id` = 100 WHERE `id` = 1;
```

#### 多表查询

```mysql
#多表查询
#多表查询就是，A和B表之间，建立了一个关系表C表，C表存放的是 A表和C表之间的关系

# 1.获取到的是笛卡尔乘积
SELECT * FROM `products`, `brand`;
SELECT * FROM `products`;
SELECT * FROM `brand`;
# 获取到的是笛卡尔乘积进行筛选
SELECT * FROM `products`, `brand` WHERE products.brand_id = brand.id;

# 2.左连接 left join 表示左边的表都可以显示  不只是显示跟右边的表有链接的
# 2.1. 查询所有的手机（包括没有品牌信息的手机）以及对应的品牌 null 
SELECT * FROM `products` LEFT OUTER JOIN `brand` ON products.brand_id = brand.id;
SELECT * FROM `products`;

# 2.2. 查询没有对应品牌数据的手机
SELECT * FROM `products` LEFT JOIN `brand` ON products.brand_id = brand.id WHERE brand.id IS NULL;
-- SELECT * FROM `products` LEFT JOIN `brand` ON products.brand_id = brand.id WHERE brand_id IS NULL;


# 3.右连接
# 3.1. 查询所有的品牌（没有对应的手机数据，品牌也显示）以及对应的手机数据；
SELECT * FROM `products` RIGHT OUTER JOIN `brand` ON products.brand_id = brand.id;

# 3.2. 查询没有对应手机的品牌信息
SELECT * FROM `products` RIGHT JOIN `brand` ON products.brand_id = brand.id WHERE products.brand_id IS NULL;


# 4.内连接
SELECT * FROM `products` JOIN `brand` ON products.brand_id = brand.id;
SELECT * FROM `products` JOIN `brand` ON products.brand_id = brand.id WHERE price = 8699;

# 5.全连接
# mysql是不支持FULL OUTER JOIN
SELECT * FROM `products` FULL OUTER JOIN `brand` ON products.brand_id = brand.id;

# 联合 联合会自动去除重复的
(SELECT * FROM `products` LEFT OUTER JOIN `brand` ON products.brand_id = brand.id)
UNION
(SELECT * FROM `products` RIGHT OUTER JOIN `brand` ON products.brand_id = brand.id)

(SELECT * FROM `products` LEFT OUTER JOIN `brand` ON products.brand_id = brand.id WHERE brand.id IS NULL)
UNION
(SELECT * FROM `products` RIGHT OUTER JOIN `brand` ON products.brand_id = brand.id WHERE products.brand_id IS NULL)

#创建表 
CREATE TABLE IF NOT EXISTS `brand`(
	id INT PRIMARY KEY AUTO_INCREMENT,
	`name` VARCHAR(20) NOT NULL,
	website VARCHAR(100),
	phoneRank INT,
-- 	FOREIGN KEY(brand_id) REFERENCES brand(id) 创建外键 引用brand的id
);

#插入
INSERT INTO `brand` (`name`,website,phoneRank) VALUES ('华为','www.huawei.com',2);
INSERT INTO `brand` (`name`,website,phoneRank) VALUES ('苹果','www.apple.com',10);
INSERT INTO `brand` (`name`,website,phoneRank) VALUES ('小米','www.mi.com',5);
INSERT INTO `brand` (`name`,website,phoneRank) VALUES ('oppo','www.oppo.com',12);
INSERT INTO `brand` (`name`,website,phoneRank) VALUES ('京东','www.jd.com',8);
INSERT INTO `brand` (`name`,website,phoneRank) VALUES ('Google','www.google.com',9);

#添加字段
ALTER TABLE `products` ADD `brand_id` INT;

#设置为外键 给products的brand_id设置引用brand中的id的外键约束
ALTER TABLE `products` ADD FOREIGN KEY(brand_id) REFERENCES brand(id);

#设置外键
UPDATE `products` SET `brand_id` = 1 WHERE `brand` = '华为';

#删除或者更新某个记录的时候，默认属性下，会检查该记录是否有关联的外键记录，有的话会报错 不给删除
```

### sql一些简单的数据转化

```mysql
# 将联合查询到的数据转成对象（一对多）
# 转化为JSON对象
-- 查询后的表格为 只显示id title price 还有brand字段，不过brand字段是包括 brand 的id name website
SELECT 
	products.id id, products.title title, products.price price,
	JSON_OBJECT('id', brand.id, 'name', brand.name, 'website', brand.website) brand
FROM `products`
LEFT JOIN `brand` ON products.brand_id = brand.id;

# 将查询到的多条数据，组织成对象，放入到一个数组中(多对多)
-- 打印 
-- id name age kecheng
-- 1	why	18	[{"id": 1, "name": "英语", "price": 100.0}, {"id": 3, "name": "数学", "price": 888.0}, {"id": 4, "name": "历史", "price": 80.0}]
-- 3	lilei	25	[{"id": 2, "name": "语文", "price": 666.0}, {"id": 4, "name": "历史", "price": 80.0}]
-- 5	lily	20	[{"id": 2, "name": "语文", "price": 666.0}, {"id": 3, "name": "数学", "price": 888.0}, {"id": 4, "name": "历史", "price": 80.0}]
SELECT 
	stu.id, stu.name, stu.age,
	JSON_ARRAYAGG(JSON_OBJECT('id', cs.id, 'name', cs.name, 'price', cs.price)) kecheng
FROM `students` stu
JOIN `students_select_courses` ssc ON stu.id = ssc.student_id
JOIN `courses` cs ON ssc.course_id = cs.id
GROUP BY stu.id;

SELECT * FROM products WHERE price > 6000;
```



