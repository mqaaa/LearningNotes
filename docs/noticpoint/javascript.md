# 开发小帖士

## 背景
最近在公司独立开发一个简单的模块，但是功能虽然简单，可是学问可还真的不少。

因为本人比较菜，初次接触大型项目，还有许多没有顾及到的地方，所以欢迎指正，精杠退去，水逆散去。

如果你想更改文档,欢迎给我提PR ---[GitHub](https://github.com/mqaaa)

*本篇文档仅用来记录自己的一些愚见*

***

## 前言

个人认为拆分组件，是刚接触项目的小白程序员的第一课。

当你看到文件夹混乱不堪，命名天书一样，拼音加英文，公有数据放在不同的文件夹下。

Ajax，jQuery的请求漫天飞，各种url出现在代码的各个角落。

`分分钟想甩手不干` 有木有。

***

## 备注

首先我们谈谈备注，

备注呢，十分重要，十分重要，十分重要！！！

有这么一句笑话，分享给你

> 程序员有4个烦恼，分别是：

> 开发程序前写文档， 开发程序时写备注

> 其他程序员不写备注，其他程序员不写文档

一个程序员能够维护的程序时有限的，但是手头的工作往往是一件又一件，所以呢，备注可以高效的提示我们你要干什么，要怎么干，注意什么。方便我们之后的维护，提高工作效率。不要小看这个，当真正接受项目的时候，不吃几次亏很难记住的。

***

## URL统一管理
在现在网页的前端项目中，React、Vue横行，我们会对后台发起请求，通常就用url，

可是你想想，你的url全部写在一个个文件中是一件多么头痛的问题吗！！！

每个亲求都要配置是多么的低效啊！！！

![](../img/我还能说些什么.gif)

所以呢，专门写个文件，用来存储API多好呀，还能做到`一键更改`，岂不是爽歪歪。

如果你可以在写个请求封装，那不是分分钟可以上天的节奏。

***

## 配置的写法

最近在用vue-webpack，

发现npm run dev/build真的很有门道，还有就是 local——setting.json

有时间咱们细聊

***

## 前端的组件能拆就拆
其实不管是前端，后端也一样，我们尽量的让你的功能组件话，兼容性高。

对于日后的开发效率来说，简直是质的飞跃。简直就是坐上了直升飞机。重要的是风格还一致。

然后好好打理你的项目的目录，公共组件就放在公共组件中，

每个模块一定要有自己的文件夹，和其相关的组件放在一起。方便维护和二次开发。

每个定义的常量还有就是方法，都按照分类，依次处理好。

***

## 命名规范
这个是最基本的我就不再赘述了。