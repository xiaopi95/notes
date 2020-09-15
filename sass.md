### Sass

* 特性：
  * 兼容CSS
  * 特性丰富
  * 成熟



### 变量声明：

```scss
$hightlight-color:#F90
```

sass中不仅可以在外部声明变量，也可以在内部声明变量;

```scss
$nav-color : #F90;
nav{
  $width : 100px;
  width : $width;
  color:$nav-color;
}

//编译后
nav{
  width : 100px;
  color : #F90;
}
```



### 变量声明用中划线还是下划线声明

中划线和下划线都是可以的，这完全取决于个人的喜好。`sass`并不强迫任何人一定要使用中划线或者是下划线，所以这两种用法是相互兼容。

```scss
$link-color:blue;
a{
  color : $link_color;
}
```





### 关于嵌套的规则

sass的嵌套和less是一样的，sass和less两个都要注意，嵌套最好是两层或者是三层，不要太多了;

```scss
#content{
  artivce{
    h1{color:#333;}
    p{margin-bottom:1.4em}
  }
  aside{background-color:#EEE;}
}
```





### 父选择器的标识符`&`

在使用嵌套规则的时候，父选择器能够对于嵌套规则如何解开提供更好的控制。他就是一个简单的`&`符号，且可以放在任何一个选择器出现的地方。当包含父选择器标识符的嵌套规则被打开之后，他不会像后代选择器那样进行拼接，而是`&`被父选择器直接替换。

```sccc
artice a{
color : blue;
&:hover{color:red}
}

//编译
artice a{color : blue}
artoce a:hover{color:red}


#content aside{
color:red;
body.ie &{color:green}
}

//编译
#content aside{color:red}
body.ie #content aside{color:green}
```





### 群组选择器的嵌套

当一个父元素里面有许多子元素需要定义样式的时候

```scss
.container h1, .container h2, .container h3{margin:80px}

//我们可以这样写
.container{
  h1,h2,h3{magin:80px;}
}


//还可以这样写，nav里面和asid里面都有a标签，都需要定义样式
nav,aside{
  a{color:red};
}
//编译之后

nav a,aside a{color:red}
```





### 嵌套属性

在sass，除了css选择器，属性也是可以进行嵌套的。

```scss
例如：
nav{
  border-style:solid;
  border-width:1px;
  border-color:#ccc;
}
```

嵌套属性的规则是这样的，把属性名从中间线-的地方断开，在根属性后边添加一个冒号：，紧跟着一个`{}`块，把字属性部分放在这个块里面，

```scss
nav{
  border:{
    style:solid;
    width:1px;
    color:red;
  }
}
```





### 默认值

sass和less一样都是可以设置默认值的。但是一般情况之下，你反复声明一个变量，只有最后一处声明是有效的，并且他会覆盖前面的值。

```scss
$link-color:blue;
$link-color:red;
a{
  color:$link-color;
}
```





### 混合器

如果你整个网站中有几处小小的样式类似，那么使用变量来统一处理这种情况是非常不错的选择。但是当你的样式变得越来越复杂的时候，你需要大段大段的重用样式的代码，这个时候独立的变量就没有办法应付这种情况了。可以使用`sass的混合器`来实现大段样式的重用。

使用混合器的时候使用`@mixin`标识符来定义。看上去很像css@标识符

```scss
@mixin rounded-corners{
  -moz-border-radius:5px;
  -webkit-border-radius :5px;
  border-radius:5px;
}
```

使用的时候使用`@include`来使用这个混合器。

```scss
.container{
  background-color:green;
  @include rounded-corners
}
```





### 混合器中的css规则

当一个包含css规则的混合器通过`@include`包含在一个父规则中时，在混合器中的规则最终会生成父规则中的嵌套规则。

```scss
@mixin no-bullets {
  list-style: none;
  li {
    list-style-image: none;
    list-style-type: none;
    margin-left: 0px;
  }
}

ul.plain{
  color:#444;
  @include no-bullets;
}
```

Sass的`@include`指令会将引入混合器的那行代码替换成混合器里面的内容。

```scss
ul.plain{
  color:#444;
  list-style:none;
}
ul.plain li{
  list-style-image: none;
    list-style-type: none;
    margin-left: 0px;
}
```





### 混合器也是可以给传递参数的

这种传递参数的方式和js中的function很相似.

```scss
@mixin link-color($normal,$hover,$visited){
  color:$normal;
  &:hover{color:$hover}
  &:visited{color:$visited}
}
```

当混合器被`@include`的时候，你可以把它当作一个css函数来编写。

```scss
a{
  @include link-color(blue,red,green)
}

//sass最终生成的是
a{color:red}
a:hover{color:red}
a:visited{color:green}
```