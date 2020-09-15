# Vue.config.js，常用配置文件

```js
const path = require('path') //路径
const UglifyJsPlugin = require('uglifyjs-webpack-plugin');  //npm install uglifyjs-webpack-plugin --save-dev
//生产环境
const isProduction = process.env.NODE_ENV === 'production';
//引入文件的方法
function resolve (dir) {
    return path.join(__dirname, dir)
}
module.exports = {
    //基本路径
    publicPath: './',
    //输入文件目录
    outputDir:"dist",
    lintOnSave:false,
    devServer: {
        compress:false，
        //open:true,
        proxy:{
            './api':{
                  target: 'http:xxx.com.cn', //需要代理服务器
                   ws:true //websocket,
                   changeOrigin:true,
                   pathRewrite:{
                          './api': '/'
                    }
             }
        }
    },
    //css相关配置
    css:{
        //是否使用css分离插件
        extract: true,
        //是否开启错误定位
        sourceMap: false,
        //css预设置配置项
        loaderOptions:{
            scss:{
                // 注意：在 sass-loader v7 中，这个选项名是 "data"
                // 默认情况下 `sass` 选项会同时对 `sass` 和 `scss` 语法同时生效
                // 因为 `scss` 语法在内部也是由 sass-loader 处理的
                // 但是在配置 `data` 选项的时候
                // `scss` 语法会要求语句结尾必须有分号，`sass` 则要求必须没有分号
                prependData:`@import "~@/assets/scss/common.scss";`
            }
        },
        //是否启用css modules for all css
        modules: false
    },
    chainWebpack: config => {
       //配置别名
       config.resolve.alias
         .set("@",resolve("src"))
         .set("@img",resolve("src/assets/img"))
         .set("@scss",resolve("src/assets/css/common"))
        //生产环境配置
        if(isProduction){
            //删除预加载
            config.plugins.delete('preload');
            config.plugins.delete('prefetch');
            //压缩代码 
            config.optimization.minimize(true);
            //分割代码
            config.optimization.splitChunks({
                chunks: 'all'
            })
        }
    },
    configureWebpack:config=>{
        //为生产环境配置
        if(isProduction){
            //为生产环境修改配置
            config.plugins.push(
                new UglifyJsPlugin({
                    uglifyOptions:{
                        compress:{
                            drop_debugger: true,
                            drop_console: true
                        }
                    },
                    //是否生成sourceMap
                    sourceMap: false,
                    //是否多进程运行提高构建效率
                    parallel: true
                })
            )
        }
    },
    //生产环境是否生成 sourceMap 文件
    productionSourceMap: false,
    //启用并行化 默认并发运行数 os.cpus().length - 1 ,并行化可以显著加速构建
    parallel: require('os').cpus().length > 1
}
```