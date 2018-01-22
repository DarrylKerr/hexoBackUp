---
title: PHP开发如何存储（处理）emoji表情
date: 2017-05-09
categories: work
tags: mysql存储emoji
---
最近几个月做微信开发比较多，存储微信昵称必不可少,本来没什么。可这万恶的微信支持emoji表情做昵称，这就有点蛋疼了，MMP...

一般Mysql表设计时，都是用UTF8字符集的。把带有emoji的昵称字段往里面insert一下就没了，整个字段变成了空字符串。这是怎么回事呢？
<!--more-->
通过翻阅文档，原来是因为Mysql的utf8字符集是3字节的，而emoji是4字节，这样整个昵称就无法存储了。这要怎么办呢？介绍几种常用的处理方法

## 1、使用utf8mb4字符集

如果你的mysql版本>=5.5.3，你大可直接将utf8直接升级为utf8mb4字符集
这种4字节的utf8编码可完美兼容旧的3字节utf8字符集，并且可以直接存储emoji表情，是最好的解决方案
至于字节增大带来的性能损耗，我看过一些评测，几乎是可以忽略不计的

## 2、使用base64编码

如果你因为某些原因无法使用utf8mb4的话，你还可以使用base64来曲线救国
使用例如base64_encode之类的函数编码过后的emoji可以直接存储在utf8字节集的数据表中，取出时decode一下即可

## 3、干掉emoji表情

emoji表情是个麻烦的东西，即使你能存储，也不一定能完美显示。在iOS以外的平台上，例如PC或者android。如果你需要显示emoji，就得准备一大堆emoji图片并使用第三方前端类库才行。即便如此，还是可能因为emoji图片不够全而出现无法显示的情况

在大多数业务场景下，emoji也不是非要不可的。我们可以适当地考虑干掉它，节约各种成本

所以你可以这样干:

``` bash
// 过滤掉emoji表情
function filterEmoji($str)
{
    $str = preg_replace_callback(
            '/./u',
            function (array $match) {
                return strlen($match[0]) >= 4 ? '' : $match[0];
            },
            $str);

     return $str;
 }
```