## 						一、WebPack是什么🐟他的五个核心概念

### 1.1 WebPack是什么

webpack是一种前端资源构建工具，是一个静态的模块打包器。在webpack看来，前端所有的资源文件都会作为模块处理。他将根据模块的依赖关系进行静态分析，打包生成对应的静态资源。

使用webpack的时候，要先下载`webpack` 与 `webpack-cli`

### 1.2 WebPack的五个核心概念

* #### 1.2.1 Entry

  * 入口（entry）指示webpack以哪一个文件为入口起点开始打包，分析构建内部的依赖图。

* #### 1.2.2 OutPut

  * 输出（output）指示webpack打包后的资源bundles输出到哪里去，以及如何命名。

* #### 1.2.3 Loader

  * loader让webpack能够去处理那些非js文件（webpack自身只能理解javascript）。

* #### 1.2.4 Plugins

  * 插件（plugins）可以用于执行范围更广的任务。插件的范围包括，从打包优化和压缩，一直到重新定义环境中的变量等。

* #### 1.2.5 Mode

  * 模式（mode）指示webpack使用相应模式的配置

    ![](/Users/quinlan/Desktop/王培申的demo文件/WebPack/QQ20200907-164037@2x.png)

### 1.3 运行指令

* 开发环境：

  ```js
  //webpack会以 ./src/index.js 为文件入口开始打包，打包后输出到./build.build.js 整体打包环境是开发环境
  webpack ./src/index.js -o ./build/build.js --mode=development
  ```

* 生产环境

  ```js
  //生产环境下他会压缩代码
  webpack ./src/index.js -o ./build/build.js --mode=production 
  ```

### 1.4 页面引入

* 注意：页面引入的时候，是要引入打包好了的文件。

### 1.5 注意事项

* webpack**本身**还可以打包JSON资源，但是不能打包样式资源和图片资源（css、img）。
* webpack打包的时候要把所有的文件引入到入口文件然后一起打包。
* 生产环境和开发环境将ES6模块化编译成浏览器能够识别的模块化



## 二、WebPack的配置文件、打包样式资源、html资源和图片资源

### 2.1webpack.config.js

* Webpack.config.js是webpack的配置文件，他的作用就是指示webpack要干哪些活（当你运行webpack的时候会加载里面的配置）
* 所有的构建工具就是基于nodejs来运行的，模块化默认采用的是commonjs。



### 2.2 打包样式资源

* 打包样式资源的话需要下载style-loader、css-loader、less-loader

```js
//resolve是用来拼接绝对路径的方法
const {resolve} = require("path");

module.exports = {
    //webpack配置

    //入口起点文件
    entry : "./src/index.js",
    //输出到哪个文件
    output : {
        //输出的文件名
        filename : "built.js",
        //输出路径
        path : resolve(__dirname,"build"),
    },
    //loader的配置，就是能够帮助我们做一些翻译，就是处理那些非js的文件
    module : {
        rules : [
            //这里面就是写详细的配置
            {
                //匹配哪一些文件,这是一个正则表达式
                //我要匹配的文件名是以.css结尾的
                test : /\.css$/,
                //使用哪些loader来进行处理
                use : [
                    //use数组中loader执行顺序，是从右到左，从下到上，依次执行
                    //创建style标签，将js中的样式资源插入，添加到head中生效
                    'style-loader',
                    //将css文件变成commonjs模块加载到js中，里面的内容是样式字符串
                    'css-loader'
                ],
            },
            {
                test : /\.less$/,
                use : [
                    //创建style标签，将js中的样式资源插入，添加到head中
                    "style-loader",
                    //然后把css文件加载到js文件中
                    "css-loader",
                    //因为浏览器是不支持less文件，所以要先把less转换成css文件
                    "less-loader"
                ]
            }
        ],
    },
    //plugins的配置
    plugins : [
        //详细的plugins配置
    ],
    //模式，就只有两种开发模式（development）和生产模式（production）
    mode : "development"
}
```



### 2.3 打包HTML资源

* 首先打包HTML资源的时候，我们要先下载HTML的插件，对，是插件，`yarn add html-webpack-plugin`,然后在引入

  ```js
  const {resolve} = require("path");
  const HtmlWebpackPlugin = require("html-webpack-plugin");
  module.exports = {
      //入口起点文件
      entry: "./src/index.js",
      //输出到哪个文件
      output: {
          //输出的文件名
          filename: "built.js",
          //输出的路径
          path : resolve(__dirname,"build")
      },
      //loader配置
      module : {
          rules: [
              {}
          ]
      },
      plugins : [
          //plugins
          //HtmlWebpackPlugin
          //功能：默认会创建一个空的HTML，自动引入打包输出的所有资源（js/css）
          //需求：需要有结构的HTML文件
          new HtmlWebpackPlugin({
              //他会复制一个index.html文件，并且自动引入打包输出的所有资源（JS/CSS）
              template : "./src/index.html"
          })
      ],
      mode : "development"
  }
  
  ```



### 2.4打包图片资源

* 打包图片资源的话，我们需要下载`url-loader`与`file-loader`两个配置文件，因为url-loader是依赖于file-loader的，还需要设置一个options配置参数。

  ```js
  const {resolve} = require("path");
  const HtmlWebpackPlugin = require("html-webpack-plugin")
  module.exports = {
      entry : "./src/index.js",
      output: {
          filename: "built.js",
          path : resolve(__dirname,"build")
      },
      module : {
          rules : [
              {
                  test : /\.less$/,
                  //使用多个规则处理那么就是用use
                  use : ["style-loader", "css-loader", "less-loader"]
              },
              {
                  //处理图片资源
                  test : /\.(jpg|jpeg|png|git)$/,
                  //如果只是使用一个规则的话，那么就是用loader
                  loader : "url-loader",
                  options : {
                      //图片大小小于8kb，就会被base64处理
                      //优点，减少请求的数量（减轻服务器的压力）
                      //缺点：图片的体积会更大（文件的请求速度变慢）
                      limit : 70 * 1024
                  }
              },
              {
                  test : /\.html$/,
                  //这个是处理html文件中img图片（负责引入img，从而能够被url-loader进行处理）
                  loader : "html-loader"
              }
          ]
      },
      plugins: [
          new HtmlWebpackPlugin({
              template: "./src/index.html"
          })
      ],
      mode : "development"
  }
  
  
  ```

* 之前的版本会有一个[object Module]，为什么会出现这个问题呢，因为url-loader是使用的ES6模块化解析，而html-loader引入的图片是commonjs的。解决的方法，在limit下面加上esModule ： false就可以了；如何给图片重新命名呢？？取图片的hash的前十位，[hash:10]，[ext]取文件原来的扩展名，`name : '[hash:10].[ext]'`



### 2.5打包其他资源

* 打包其他的资源（除了html、js、css资源以外的资源）,可以使用exclude来排除资源,处理其他的资源是需要使用`file-loader`库的

  ```js
  const { resolve } = require('path');
  const HtmlWebpackPlugin = require('html-webpack-plugin');
  
  module.exports = {
    entry: './src/index.js',
    output: {
      filename: 'built.js',
      path: resolve(__dirname, 'build')
    },
    module: {
      rules: [
        {
          test: /\.css$/,
          use: ['style-loader', 'css-loader']
        },
        // 打包其他资源(除了html/js/css资源以外的资源)
        {
          // 排除css/js/html资源
          exclude: /\.(css|js|html|less)$/,
          loader: 'file-loader',
          options: {
            name: '[hash:10].[ext]'
          }
        }
      ]
    },
    plugins: [
      new HtmlWebpackPlugin({
        template: './src/index.html'
      })
    ],
    mode: 'development'
  };
  
  ```





## 									三、关于devServer

### 3.1 devServer

* 首先要使用devServer的话，那么我们就需要先下载`webpack-dev-server`库。devServer是用来自动化的（自动编译，自动打开浏览器，自动刷新浏览器）。他的特点是：只会在内存中编译打包，不会有任何的输出。

* 启动指令为：`npx webpack-dev-server`

  ```js
  const { resolve } = require('path');
  const HtmlWebpackPlugin = require('html-webpack-plugin');
  
  module.exports = {
    entry: './src/index.js',
    output: {
      filename: 'built.js',
      path: resolve(__dirname, 'build')
    },
    module: {
      rules: [
        {
          test: /\.css$/,
          use: ['style-loader', 'css-loader']
        },
        // 打包其他资源(除了html/js/css资源以外的资源)
        {
          // 排除css/js/html资源
          exclude: /\.(css|js|html|less)$/,
          loader: 'file-loader',
          options: {
            name: '[hash:10].[ext]'
          }
        }
      ]
    },
    plugins: [
      new HtmlWebpackPlugin({
        template: './src/index.html'
      })
    ],
    mode: 'development',
  
    //开发服务器devServer，就是用来自动化的（自动编译，自动打开浏览器，自动刷新浏览器）
    devServer : {
      //项目构建后index.html的路径
      contentBase : resolve(__dirname,"build"),
      //启动gzip压缩,compress就是压缩的意思
      compress : true,
      //设置端口号
      port : 3000,
      //自动打开浏览器
      open : true
    }
  };
  对的对的
  this 【表情】
  ```