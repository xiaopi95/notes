### less

Less是一门向后兼容的CSS扩展语言。因为less和css非常的相似，因此很容易学习。而且less仅对CSS语言增加了少许方便的扩展，这就是less易学的原因。

注意：浏览器是不支持less，只有把less转换成css浏览器才能支持

less编译的时候可以使用node来编译。`lessc style.less > style.css`,也可以使用https://cdnjs.cloudflare.com/ajax/libs/less.js/3.11.1/less.min.js这上面的，下载之后引入就可以了。

注意：引入less的时候要把stylesheet改成stylesheet/less

### less的基本用法：

1. 变量的设置与使用：

   设置变量，封装样式

   ```less
   @main-color：#5b83ad
   
   使用的时候
   
   body{
     background-color:@main-color;
   }
   
   也可以这样写：
   .xk{
     width:400px;
     height:400px;
     border : 1px solid #ccc;
   }
   
   .box{
     .xk;//可以引用.xk的样式
   }
   ```

2. 也可以使用函数:

   ```less
   @main-color : red;
   .xk{
     width:400px;
     height:400px;
     border:1px solid #ccc;
   }
   
   .lcbutton(@bgcolor这里是一个变量，使用的时候像函数一样传递参数就行了){
     .xk;
     background-color:@bgcolor;
   }
   
   .readButton{
     .lcbutton(@main-color)
   }
   ```

3. 关于默认参数

   ```less
   .lcbutton(@main-color:#ccc){
     background-color : @main-color;
   }
   
   body{
     .lcbutton()
   }
   ```

4. 运算

   包含加减乘的，需要用括号来拼接，操作的对象主要是数字、颜色、变量等，配置基础样式，封装样式

   ```less
   @width:3rem;
   
   .container{
     width: @width * 2;
     height: 100px;
     background-color: #cccccc;
   }
   ```

5. 嵌套

   嵌套关系主要是父子级的关系层，但是不建议大家使用，该方式不便代码的维护管理，尽可能使用class来规划业务层级问题；

   ```less
   .list{
     width : 10rem;
     margin: 3rem auto;
     padding : 30px;
     li{
       height : 400px;
       line-height:10px;
       margin:40px;
     }
   }
   ```

6. 懒人必备的arguments变量

   使用arguments的好处就是可以帮你自动填充所有的变量

   封装样式：

   ```less
   .border_arg(@width:10px,@color:red,@style:solid){
     border:arguments
   }
   
   //渲染结果
   .border_arg{
     border : 10px solid red;
   }
   ```







### less小技巧：

#### 注释问题：

/**/使用这个注释，在编译之后会被保留

//使用这种注释，编译知乎不会被保留

关于：！important，使用他的时候，浏览器会先执行有！important的选择器

#### 避免编译：

如果你不想让这个参数被编译的话，在字符串前面加上一个`～`