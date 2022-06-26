#### 全局下

- 全局下，this就是window，因为在GO中，绑定window为this
- 函数调用的时候，都会创建一个函数执行上下文，里面会有this的指向，解析的时候没有定义this的指向。
- this的绑定和定义的位置没有关系
- this的绑定和调用的方式以及调用的位置有关系。

#### 默认绑定

- 独立函数
- 一般不知道是什么调用函数的时候，那就可以当做是独立函数调用，像setTimeout里面的this就会绑定window，但是当setTimeout函数的参数是箭头函数时，箭头函数是不绑定this的，会绑定他父级作用域的this，此时就看setTimeout的外层作用域的this。

#### 隐式绑定

- 对象里面的方法

#### 显示绑定

- apply
- call
- bind

#### new绑定

- new Class{}

#### 规则优先级

- 默认绑定优先级是最低的。
- 显示绑定高于隐式绑定。
- new绑定是高于显示绑定的。

#### 忽略显示绑定

- 当显示绑定比如bind,apply,bind绑定的对象是null或者undefined的时候，那么绑定的this就是window。

#### 箭头函数

- 箭头函数不会绑定this，arguments属性。
- 箭头函数不能作为构造器来使用，不能和new一起来使用。