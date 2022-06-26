#### 第一部分：初始化项目

##### 1.创建项目目录

##### 2.初始化package.json

```javascript
npm init
```

##### 3.安装webpack并且添加配置文件

- webpack5之后，需要单独安装webpack-cli，在命令行输入webpack，会执行webpack-cli这个包，详细入口逻辑看node_modules/.bin/webpack.js

```javascript
npm i webpack -D 
npm i webpack-cli -D 
```

- 创建webpack.config.js文件，后续会分为common和pro和dev三部分

------

#### 第二部分：browserslistrc

- 是一个平台，需要搭配插件使用。

- 配置时候可以去网站can i use 来查看浏览器的使用率，然后配合工具做浏览器做兼容

- 配合的工具（当使用下列工具的时候，会自动读取browserslistrc的数据）

  - postcss-preset-env
  - Autoprefixer
  - Babel
  - eslint-plugin-compat
  - stylelint-no-unsupported-browser-features
  - postcss-normalize

- ```javascript
  //文件名.browserslistrc
  > 0.01% 
  last 2 version
  not dead
  ```

  

------

#### 第三部分：loader

- 介绍：让特定类型能转化，转化成webpack能识别的javascript和json文件，读取文件的时候loader就开始运行，比如转化css的loader，读取css文件的时候就开始识别了
- loader使用在module的rules里面，详情看文档。使用顺序是，从右往左，从下往上

##### css部分

1.postcss

- 是一个平台，使用的时候，安装`postcss-loader` 和 `postcss` ,因为是平台，所以需要搭配插件使用
- 搭配插件`autoprefixer` 或者 `postcss-preset-env`，因为``postcss-preset-env`` 是预设插件，即他的功能很广泛，其中包括了`autoprefixer` ，该功能就是给样式添加前缀，所以直接使用`postcss-preset-env`，
- 搭配插件`browserslistrc` ,详情参考 **介绍** 栏目，大概就是配合浏览器使用率，然后只要哪些浏览器才能使用

2.习惯使用sass，所以我们需要安装依赖如下

- sass-loader
- sass-resources-loader

3.所以rules如下

- vue-style-loader是解析vue中的style，css-loader解析css，顺序从下往上
- sass-resources-loader是解析某个文件夹中的sass并且解析其中的@mixin @includes等等语法

- ```javascript
  const commonCssLoader = ["vue-style-loader", "css-loader", "postcss-loader"];
  const cssRules = [
    {
      test: /\.css$/i,
      use: [...commonCssLoader],
    },
    {
      test: /\.(sass|scss)$/i,
      use: [
        ...commonCssLoader,
        "sass-loader",
        {
          loader: "sass-resources-loader",
          options: {
            resources: resolve(__root, "./src/commons/styles/var.scss"),
          },
        },
      ],
    },
  ];
  module: {
     rules: [...cssRules],
  },
  ```

##### js部分

- 浏览器存在很多版本，当你使用一些旧版本的浏览器时，那些浏览器并不识别最新的ES语法
- 但是使用babel可以将高版本的JavaScript代码转为向后兼容的JS代码
- 详细babel说明可以查看 介绍篇章里面的babel

1.babel-loader

2.@babel/core

3.@babel/preset-env

4.@babel/eslint-parser用于.eslintrc.js文件

```
//babel.config.js
module.exports = {
  presets: [
    [
      '@babel/preset-env',
      {
        useBuiltIns: 'usage',
        corejs: 3
      }
    ]
  ]
}
```

##### vue部分

1.vue-loader

- 其中vue-loader要配合vue-template-compiler使用

- vue-loader用来解析.vue文件，并且在，vue-loader要使用^15.0.0版本，因为更高的版本没有complie/sfc模块，要不就装该模块然后用更高的版本，要不就装更低的版本

  ```javascript
  const vueRules = [
    {
      test: /\.vue$/i,
      use: ["vue-loader"],
    },
  ];
  module:{rules: [...vueRules]}
  const { VueLoaderPlugin } = require("vue-loader");
  plugins: [new VueLoaderPlugin()],
  ```


2.vue-template-compiler

- 作用就是解析.vue文件里面的template里面的代码，生成render函数
- 也就是因为有vue-loader解析.vue文件和vue-template-compiler解析template，所以我们的vue默认导入的是runtime版本，也就是运行时版本，不是完整版，所以内存更小
- 假设是完整版，他可以不用vue-loader解析.vue文件和vue-template-compiler解析template

3.@vue/babel-helper-vue-jsx-merge-props和@vue/babel-preset-jsx

- 上面这两个依赖是开发依赖，参考vue-cli，用来解析.vue文件的render函数里面jsx

4.vuex和vue-router

- 版本是参考vuec-cli创建的vue2，属于生产依赖

- ```javascript
  "vue-router": "^3.5.2",
  "vuex": "^3.6.2"
  ```

  



------

#### 第四部分：plugins

1.clean-webpack-plugin

- 每次打包的时候，清楚打包文件内的内容，现在已被output的clean属性代替

- ```javascript
  plugins:[new CleanWebpackPlugin()]
  ```

2.html-webpack-plugin

- 每次打包的时候，都需要一个html模板，该html模板用来引入静态资源

- 其中ejs是模板，也可以定义其他文件

- templateParameters中的title属性是ejs里面的参数<%= title %>

- ```javascript
  const HtmlWebpackPlugin = require("html-webpack-plugin");
  plugins: [
      new HtmlWebpackPlugin({
        template: "./src/index.ejs",
        templateParameters: {
          title: "bar",
        },
      }),
    ],
  ```

3.copy-webpack-plugin

- 该插件，就是将一些静态资源不被打包，但打包完成后，复制到打包后的文件中
- 使用情况：当你需要把静态资源不被打包并且赋值到打包后的文件时，使用该插件

#### 第五部分：规范

- 安装依赖
  - eslint
  - prettier
  - eslint-config-prettier
  - eslint-plugin-prettier
  - eslint-plugin-vue
- vscode安装Eslint和Prettier-Code formatter

1.eslint

- npm包的eslint详情就是一些代码规范还有错误的问题，详情看文档，vscode的eslint插件，就是在运行的时候可以识别错误（设置setting.json），npm的eslint也可以识别错误，但是要运行命令，他带一些默认的eslint的rule
- 在.eslintec.js的extend： extends: ['eslint:recommended']

2.prettier

- Prettier-Code formatter就是vscode跟npm中prettier一起格式化代码规范的工具（设置setting.json..比如什么自动保存之类的）

3.eslint-config-prettier和eslint-plugin-prettier

- 因为eslint和prettier会有冲突，因为他们都有共同就是处理代码规范问题，这时候，就可以使用上面两个插件来解决冲突
- 他是解决跟prettier冲突的eslint规则（覆盖）
- 在.eslintec.js的extend放到最后一位就好了 extend:[...'plugin:prettier/recommended']，

4.eslint-plugin-vue

- 它可以解析.vue文件里面的template和script和style,并且他是带默认的vue的rule，
- 所以.eslintec.js添加parser: 'vue-eslint-parser'（看文档），并且extends:['plugin:vue/recommended']，但不是最后一位（看文档）
- 并且他也是一个插件，plugins: ['eslint-plugin-vue'],

5.至于环境那些还是看文档，所以.eslintec.js

```javascript
module.exports = {
  env: {
    browser: true,
    es2021: true,
    node: true,
  },
  parser: 'vue-eslint-parser',
  extends: [
    'eslint:recommended',
    'plugin:vue/recommended',
    'plugin:prettier/recommended',
  ],
  parserOptions: {
    ecmaVersion: 'latest',
    sourceType: 'module',
    ecmaFeatures: {
      jsx: true,
    },
  },
  plugins: ['eslint-plugin-vue', 'eslint-plugin-prettier'],
};
```





