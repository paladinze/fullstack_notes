# 设计模式

## 设计模式有哪些

- 工厂模式
- 装饰器模式
- 适配器模式
- 发布订阅模式
- 代理模式
- Prototype Pattern
- Observer Design Pattern

## SOLID principles
- Single responsibility principle
	- do one thing and do it well
- Open–closed principle
	- extensible but cannot directly modify internal state from outside
- Liskov substitution principle
	- objects can be safely replaced with its subtype
- Interface segregation principle
	- don't create general-purpose interface
- Dependency inversion principle
	- depend upon abstractions, not concretions

## 使用 Ajax 的优缺点分别是什么

**优点**

- 来自服务器的新内容可以动态更改，无需刷新
- 减少与服务器的连接，因为脚本和样式只需要被请求一次。
- 状态可以维护在一个页面上

**缺点**

- 动态网页很难收藏。
- 有些网络爬虫不执行 JavaScript

## 从输入 url 到展示的过程 （复杂版）

https://github.com/skyline75489/what-happens-when-zh_CN/blob/master/README.rst?utm_medium=social&utm_source=wechat_session&from=timeline&isappinstalled=0

1、浏览器会开启一个线程来处理这个请求，对 URL 分析判断如果是 http 协议就按照 Web 方式来处理;
2、调用浏览器内核中的对应方法，比如 WebView 中的 loadUrl 方法;
3、通过 DNS 解析获取网址的 IP 地址，设置 UA 等信息发出第二个 GET 请求;
4、进行 HTTP 协议会话，客户端发送报头(请求报头);
5、进入到 web 服务器上的 Web Server，如 Apache、Tomcat、Node.JS 等服务器;
6、进入部署好的后端应用，如 PHP、Java、JavaScript、Python 等，找到对应的请求处理;
7、处理结束回馈报头，此处如果浏览器访问过，缓存上有对应资源，会与服务器最后修改时间对比，一致则返回 304;
8、浏览器开始下载 html 文档(响应报头，状态码 200)，同时使用缓存;
9、文档树建立，根据标记请求所需指定 MIME 类型的文件（比如 css、js）,同时设置了 cookie;
10、页面开始渲染 DOM，JS 根据 DOM API 操作 DOM,执行事件绑定等，页面显示完成。

## 从输入 url 到展示的过程 （简化版）

- DNS 解析
- TCP 三次握手
- 发送请求，分析 url，设置请求报文(头，主体)
- 服务器返回请求的文件 (html)
- 浏览器渲染
  - HTML parser --> DOM Tree
    - 标记化算法，进行元素状态的标记
    - dom 树构建
  - CSS parser --> Style Tree
    - 解析 css 代码，生成样式树
  - attachment --> Render Tree
    - 结合 dom 树 与 style 树，生成渲染树
  - layout: 布局
  - GPU painting: 像素绘制页面

## 什么叫优雅降级和渐进增强？

- 优雅降级

  - 针对新环境设计，针对旧环境兼容

- 渐进增强：
  - 针对旧环境设计，针对新环境优化

## 知道什么是 singleton, factory, strategy, decrator， MVVM 么?

MVC
	model
	view
	controller
MVP
	model
	view
	presenter
MVVM
	view (React)
	view model
	model

## 介绍下观察者模式和订阅-发布模式的区别，各自适用于什么场景

- 观察者模式中主体和观察者是互相感知的，发布-订阅模式是借助第三方来实现调度的，发布者和订阅者之间互不感知
