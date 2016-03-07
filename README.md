# LESS学习笔记
------
2016-3-7
## 1. 变量
```
@color: red;
#header {
    color: @color;
}
h2 {
    color: @color;
}
```
编译之后的CSS就是：
```
#header {
    color: red;
}
h2 {
    color: red;
}
```
> 变量是“按需加载”（lazy loaded）的，因此不必强制在使用之前声明。> 

## 2. 混合
混合可以将一个定义好的class A引入到class B中，实现class B的继承性。
```
.rounded-corners (@radius: 5px) {
    -webkit-border-radius: @radius;
    -moz-border-radius: @radius;
    -ms-border-radius: @radius;
    -o-border-radius: @radius;
    border-radius: @radius;
}

#header {
    .rounded-corners;
}
#footer {
    .rounded-corners(10px);
}
```
编译之后的css：
```
#header {
    -webkit-border-radius: 5px;
    -moz-border-radius: 5px;
    -ms-border-radius: 5px;
    -o-border-radius: 5px;
    border-radius: 5px;
}
#footer {
    -webkit-border-radius: 10px;
    -moz-border-radius: 10px;
    -ms-border-radius: 10px;
    -o-border-radius: 10px;
    border-radius: 10px;
}
```

## 3. 嵌套
可以在一个选择器中嵌套另一个选择器来实现继承。
```
#header {
    h1 {
        font-size: 26px;
        font-weight: bold;
    }
    p {
        font-size: 12px;
        a {
            text-decoration: none;
            &:hover {
                border-width: 1px;
            }
        }
    }
}
```
编译之后：
```
#header h1 {
  font-size: 26px;
  font-weight: bold;
}
#header p {
  font-size: 12px;
}
#header p a {
  text-decoration: none;
}
#header p a:hover {
  border-width: 1px;
}
```

> &表示串联选择器

## 4. 函数和运算
运算提供了加，减，乘，除操作；我们可以做属性值和颜色的运算，这样就可以实现属性值之间的复杂关系。

## 5. 导入（Import）
在LESS中，你既可以导入CSS文件，也可以导入LESS文件。但只有导入的LESS文件才会被处理（编译），导入的CSS文件会保持原样。如果你希望导入一个CSS文件，保留.css后缀即可。编译过程中，对导入CSS文件只做一处处理：将导入的语句提到最前

- [ ] 命名空间
- [ ] 作用域
- [ ] 混合   注：需要细细看看