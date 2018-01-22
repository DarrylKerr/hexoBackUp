---
title: document.getElementsByClassName的兼容性问题
date: 2016-02-07
tags: JavaScript
categories: work
---
## 定义和使用

getElementsByClassName() 方法返回文档中所有指定类名的元素集合，作为 NodeList 对象。
NodeList 对象代表一个有顺序的节点列表。NodeList 对象 我们可通过节点列表中的节点索引号来访问列表中的节点(索引号由0开始)。
<!--more-->
## 浏览器支持

| Chrome       | IE    | Firefox    |   Safari      |   Opera       |
|--------------|-------|------------|---------------|---------------|
| 4.0          | 9.0   |    3.0     |       3.1     |      9.5      |

## 兼容性问题

IE8及其以下版本不支持getElementsByClassName这个方法，但是很多时候需要兼容这些浏览器，目前可以这么解决，判断浏览器支不支持这个方法，如果支持就不管；如果不支持，就在document对象里加入getElementsByClassName这个方法，这样的写法有一个好处，即不管有没有原生函数你都不用去修改代码。
写法（已通过IE8、IE7测试）:

```js
    if(!document.getElementsByClassName){
    document.getElementsByClassName=function(param){
    var arr=document.getElementsByTagName('*');
    var arrAll=[];
    for(var i=0;i< arr.length;i++){
        var className=arr[i].className;
        var arrClass=className.split(' ');		
        for(var k=0;k< arrClass.length;k++){	
            if(arrClass[k]==param)		
            arrAll.push(arr[i]);
            }
        }
    return arrAll;
    };
}
```