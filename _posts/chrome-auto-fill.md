---
title: chrome记住密码自动填充表单黄色背景
date: 2016-03-19
tags: chrome自动填充背景
categories: work
---
很多时候我们在使用chrome时，会使用它的记住密码功能，当再次登录表单自动填充后，input文本框的背景会变成黄色（图1），通过审查元素可以看到这是由于chrome会默认给自动填充的input表单加上input:-webkit-autofill私有属性（图2），然后赋予以下样式：

<!--more-->
```css
input:-webkit-autofill {
    background-color: rgb(250, 255, 189);
    background-image: none;
    color: rgb(0, 0, 0);
}
```

图一:
![chrome自动填充表单背景](http://cherrycookies.cc/wp-content/uploads/2017/03/auto_full_input-300x159.png)

图二:
![chrome自动填充表单背景](http://cherrycookies.cc/wp-content/uploads/2017/03/24e74a2d6d8ee844af634b14488fa8eb-300x66.png)

有些情况下会影响我们界面的设计（就算不影响看起来也不爽吧），对于input背景是纯色的，可以用内部阴影（box-shadow）去遮盖:

```css
input:-webkit-autofill {  
-webkit-box-shadow: 0 0 0px 1000px white inset;  
border: 1px solid #CCC!important;  
} 
```

结果如下:
![chrome自动填充表单背景](http://cherrycookies.cc/wp-content/uploads/2017/03/81234eeaab39be44b4f5c5f3ac837b32-300x159.png)

对于背景为非纯色（图片），实现比较复杂，可以在form标签加上autocomplete属性，值设为off，从而禁用自动填充。