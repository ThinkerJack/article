![](https://img-blog.csdnimg.cn/20211014162816903.png)

android/ios/flutter/angular/java web 5种技术编写的7个demo工程，有点用，可以看看，[github地址](https://github.com/ThinkerJack/jack_demo)，https://github.com/ThinkerJack/jack_demo。

# android_demo

## 1.项目简介

《第一行代码》第二版书中示例demo，时间过去比较久，有一些API变动，自己动手写了一遍。

## 2.环境简介

语言：java 1.8

依赖库：详见android_demo/app/build.gradle下的dependencies

## 3.项目截图

![](https://img-blog.csdnimg.cn/d29d8323a58949a4a952da489d056f23.png)

## 4.开发流程与代码逻辑简述

- 打开Android Studio配置安卓开发环境
- `MainActivity`为入口文件，修改其中的跳转页面，体验不同的demo

## 5.技术准备

- java基础语法
- 《第一行代码》书籍第二版
- [安卓开发官网](https://developer.android.com/)

## 6.总结

因为在学习之前有java基础，直接阅读此书没有遇到什么困难，一些API的变化搜索引擎就解决了。作为一名Flutter工程师，收获了一些安卓系统特有的知识，如服务，内容提提供器，广播，通知，请求权限，调试安卓程序，打包构建等等。FLutter作为依附于native系统的技术，熟悉native系统的特性还是很有比较必要的，虽然大部分知识FLutter工作中用不到，但感觉收获还是蛮大的。在今年的学习计划结束后，后续可能把native系统的学习作为首要目标。

# android_web

## 1.项目简介

自己写的一个登录demo，调用了真实的接口，主要就是想模拟一下真实的android开发流程。

## 2.环境简介

语言：java 1.8

依赖库：详见android_demo/app/build.gradle下的dependencies

## 3.项目截图

![](https://img-blog.csdnimg.cn/9b1016b7e4eb4fe58ae7cf5eb96c096f.png)

## 4.开发流程与代码逻辑简述

- 打开Android Studio配置安卓开发环境
- 编写xml布局文件
- 在Activity中获取页面控件，给按钮添加监听事件
- 将输入框中的元素通过网络请求发送给服务器，拿到返回结果后将json序列化为Java对象。

## 5.技术准备

- java基础语法

- [Android布局技术](https://developer.android.com/guide/topics/ui)

- [okhttp](https://github.com/square/okhttp)

- [GSON](https://github.com/google/gson)

  ```java
  Gson gson = new Gson();
  JsonBean data = gson.fromJson(responseData, JsonBean.class);
  ```

## 6.总结

一个简单的小APP，包含了移动开发中必备的环节，网络请求，获取页面元素，json序列化。官网文档+搜索引擎+一点经验解决工作中百分之九十五的问题。。

# angular_demo

## 1.项目简介

使用Angular框架和TypeScript编写的前端项目。主要包含一些web开发中常用组件的展示。

## 2.环境简介

语言：TypeScript

框架版本：Angular CLI:11.2.6

包管理工具：Node:14.16.0

## 3.项目截图

![](https://img-blog.csdnimg.cn/20211014162817292.png)

![](https://img-blog.csdnimg.cn/20211014162817587.png)

## 4.开发流程与代码逻辑简述

- 搭建开发环境
- 创建工程，安装组件库NG-ZORRO和ng-bootstrap
- 在项目中引入所需要的具体组件
- 在html文件中绘制布局，在ts文件中编写逻辑

## 5.技术准备

- TS语法
- [Angular基础知识](https://angular.cn/)
- 组件库文档[NG-ZORRO](https://ng.ant.design/components/overview/zh)和[ng-bootstrap](https://ng-bootstrap.github.io/#/components/accordion/examples)

## 6.总结

很简单的开源项目，当时写这个主要是为了熟悉一下angular组件。作为github上自己唯一的前端项目，我感觉很没水平，连最起码流程页面都没有一个，不过自己本身前端水平也不高，也不打算长期在这方面发展，计划之内还有其他的事情，只能接受这种不完美了。

在职业生涯的初期，自己一直在写Angular，从Angular.js到Angular7,8,11，由于对前端没有一点的兴趣，唉，工作之外的时间都去学java写后台了，一直也没有深入了解angular，就是CRUD，但是这种工作和私下学习分开的学习方式对我来说效果很不好，导致JAVA服务器端开发和前端开发都没有深入，其实自己现在也面临着这样的问题，工作两年，java web，angualr，flutter，android，iOS，除却FLutter有一些积累外，其他的技术都是勉强应付工作，环境和个人认知导致的吧，自己这只有广度没有深度的技术栈，从资本主义的角度来看，专精一门的工人生产力更高，也就是所谓的大厂螺丝钉。提高自己的生产力，就是让自己更值钱，接下来的一年也会朝着专精一门的方向发展，除却计算机基础知识的学习外，在flutter和android上提高自己的技术深度。争取在工作三年之际给自己一个满意的答案。

虽然自己一直苦于没有技术深度，但是这种技术广度也让自己对整个产品的开发流程更加了解，其实很多技术知识都是可以复用的，像本篇文章中介绍的框架Angular的响应式编程，在FLutter中也同样适用；还有端开发的统一流程，发送请求，获取数据，更新UI；就是后端和前端的某些知识也是可以通用的，在写后台的过程中学习SQL知识，在端开发的本地存储上一样适用；面向对象还能在脚本开发中发挥作用。还有程序架构mvc，mvp，mvvm之类，很多很多吧。

得益于这两年来的自学，不夸张的说，让自己培养出了较强的学习能力，学习能力其实是很抽象的，首先有学习的热情，同样学习热情的两个人，在学习过程中的速度和效果，就可以理解为学习能力。这两年间自己的大脑里已经有了一张图谱，在面对新知识的时候，会敏锐的发现哪些知识和之前学的知识类似，并将他们关联起来，哪些是需要重点学习的新概念，哪些是不太重要的知识。大脑其实是很懒惰的，碰到理解不了的东西他就会分散你的注意力，让你去做一些不需要动脑的事情，我把这些事情称之为精神垃圾。学习分两种，向之前提过的将知识与原来学习过的东西联系起来不算真正意义上的学习，叫复习。只有哪些你理解不了的概念，大脑不想让你继续学下去的知识，才是有效的学习。面对这样的情况，就是用意志力和大脑对抗，我就是要弄懂，一遍不懂就重复看，看懂为止。意志力又是一个新概念了，我觉得很多伟大的文学作品都增强了我的意志力，让我勇于面对生活，活着就挺难了。

没有文档的开源项目相当于没有灵魂，自己专门腾出一些时间，给这些项目赋予灵魂，为测试不同的项目配置了很多环境。好处就是自己的开源项目写的没那么多，工作量尚可，自己的记忆也还不错，项目的一些流程和细节都还能想的起来。还没有灵魂的项目不多了，争取这周搞完，以后写项目写完之后一定要写一份文档，这种堆积起来一次补齐的方式太累了。这两年总是在迷茫和换工作中度过，很多自己想做的事情都被准备面试耽误了，这份工作无论如何也要做一年多，把自己想做的东西，想学的知识有条不紊的完成，也算对得起自己。

# flutter_demo

## 1.项目简介

flutter APP。

项目分五个文件夹:

- 动画组件
- 工作中用到或是一些其他有趣的组件
- 布局相关的组件
- 学习FLutter编写的练习或是测试代码
- 工具类，后面会单独写成一个项目

## 2.环境简介

语言：Dart

fLutter版本：Channel master, 2.3.0-17.0.pre.414

## 3.项目截图

![](https://img-blog.csdnimg.cn/7bfc8de344d34ddea1e7898a16f11ed5.png)

## 4.开发流程与代码逻辑简述

- 组件比较多就不一一介绍了

## 5.技术准备

- Dart基础
- FLutter API

## 6.总结

这个项目维护是比较多的，首页上展示的只有动画和一些有趣的组件，可以下载体验一下，看看有没有感兴趣的功能。这个项目有单独的地址，目前这个demo工程只是一些测试代码。

# IOS_Demo

## 1.项目简介

学习ios写的小demo，比较零碎，看到感兴趣的知识点就自己动手试一下，没有什么下载价值。

## 2.环境简介

语言：Swift 5.4

UI框架：UIKit

## 3.项目截图

![](https://img-blog.csdnimg.cn/09512621e00a4173a5e2ae330b64e9b7.png)![](https://img-blog.csdnimg.cn/a34dc44d550d4ea18c26a348deaa10f7.png)![](https://img-blog.csdnimg.cn/863b4416093e491aa8f5ddefccd237a4.png)![](https://img-blog.csdnimg.cn/d076e1e49377453c823a457d790c8a77.png)

## 4.开发流程与代码逻辑简述

- 更多的使用了storyboard拖拽控件的开发方式，简单体验了一下。

## 5.技术准备

- [Swift基础语法](https://docs.swift.org/swift-book/GuidedTour/GuidedTour.html)

- [UIKit使用](https://developer.apple.com/documentation/uikit/)


## 6.总结

找的不少教程都不写纯代码，都是storyboard拖拽控件结合代码，不太喜欢这种方式.

# 写在末尾

由于更换了电脑，两个java相关的工程需要重新搭建环境补齐文档，暂时不打算更新了，感兴趣的网上随便搜几篇技术文章就能搭。

后续如果自己想写点后台的话，就顺手把这两个readme补齐。

![](https://img-blog.csdnimg.cn/c66cc07b674c424ba11ec6825e22a640.png)

![](https://img-blog.csdnimg.cn/46f9ed15f914479ab130d47e9578e721.png)
