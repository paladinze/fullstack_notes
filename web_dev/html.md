## 页加载流程

- 浏览器一边下载 HTML 网页，一边开始解析
- 解析过程中，浏览器发现 script 元素，就暂停解析，把网页渲染的控制权转交给 JavaScript 引擎
- 如果 script 元素引用了外部脚本，就下载该脚本再执行，否则就直接执行代码。
- JavaScript 引擎执行完毕，控制权交还渲染引擎，恢复解析 HTML 网页。

## 页面加载中的事件触发顺序
- HTML fully loaded
- DOM tree built
- deferred script executed
- [event] `document.DOMContentLoaded`: can lookup DOM nodes
- all external resources (images, styles) loaded
[event] `window.onload`: styles are applied, image sizes are known

## 页面加载中的阻塞
- non-deferred/non-async script waits for styles
- DOMContentLoaded waits for script

## 异步加载JS的方式有哪些？（防止阻塞页面渲染）
- 将 script 标签放到 body 底部 (本质还是同步的)
  - 缺点：必须先等html加载完
- defer:
  - 异步平行加载js
  - DOM解析完成后才执行
  - js文件之间的相对顺序能保证
  - `DOMContentLoaded`会等待js文件加载完才触发
- async:
  - 异步平行加载js，但执行时会阻塞元素渲染
  - 下载完成后立刻执行
  - 每个script之间完全独立，不确保执行顺序
  - 例子：google analytics
- 动态创建 script，插入到 DOM 中
  - 插入 DOM 后开始加载
  - 默认和 “async” 等价

```js
let script = document.createElement("script");
script.src = "/article/script-async-defer/long.js";
document.body.append(script); // (*)
```

## 浏览器的渲染过程

1. 解析 HTML 生成 DOM 树。
2. 解析 CSS 生成 CSSOM 规则树。
3. 将 DOM 树与 CSSOM 规则树合并在一起生成渲染树。
4. 遍历渲染树开始布局，计算每个节点的位置大小信息。
5. 将渲染树每个节点绘制到屏幕。

## 简述一下你对 HTML 语义化的理解？

- 用正确的标签做正确的事情。
- html 语义化让页面的内容结构化，结构更清晰
- 便于搜索引擎解析

## Doctype 作用？标准模式与兼容模式各有什么区别?

- “<!DOCTYPE html>”声明位于 HTML 文档中的第一行
- 告知浏览器用什么文档标准解析这个文档
- DOCTYPE 不存在或格式不正确会导致文档以兼容模式呈现。
- 标准模式的排版 和 JS 运作模式都是以该浏览器支持的最高标准运行
- 在兼容模式中，页面以宽松的向后兼容的方式显示

## 在哪放置 CSS 和 JS？

- CSS: in '<head>'
  - if not at the top, browsers have to reflow the layout as CSS files load
  - if not, browers will move elements around while the user is trying to interact with the page
- JS: right before </body>
  - browsers have to block processing the HTML while a JavaScript file loads

## img 中的 alt 和元素的 title 属性作用

- img 的 alt 属性
  - 如果无法显示图像，浏览器将显示 alt 指定的内容
- 元素 title 属性
  - 在鼠标移到元素上时显示 title 的内容

## href 和 src 区别

- href
  - href 标识超文本引用，用在 link 和 a 等元素上
  - href 是在当前元素和引用资源之间建立联系
- src
  - src 表示引用资源，替换当前元素，用在 img，script，iframe 上
  - 当浏览器解析到 src ，会暂停其他资源的下载和处理，直到将该资源加载、编译、执行完毕，图片和框架等也如此，

## label 标签有什么作用

`label` 标签通常是写在表单内，它关联一个控件，使用 `label` 可以实现点击文字选取对应的控件。

```html
<input type="checkbox" id="test" /> <label for="test">test</label>
```

## iframe 框架有那些优缺点

#### 优点：

- iframe 能够原封不动的把嵌入的网页展现出来。
- 如果有多个网页引用 iframe，那么你只需要修改 iframe 的内容，就可以实现调用的每一个页面内容的更改，方便快捷。

#### 缺点：

- 搜索引擎的爬虫程序无法解读这种页面
- 框架结构中出现各种滚动条
- iframe 页面会增加服务器的 http 请求

## 什么是 window 对象? 什么是 document 对象?

- window 对象是指浏览器打开的窗口。
- document 对象是 Documentd 对象（HTML 文档对象）的一个只读引用，window 对象的一个属性。

## documen.write 和 innerHTML 的区别

- document.write 只能重绘整个页面
- innerHTML 可以重绘页面的一部分

## DOM 操作——怎样添加、移除、移动、复制、创建和查找节点?

- 创建新节点
  - createDocumentFragment() //创建一个 DOM 片段
  - createElement() //创建一个具体的元素
  - createTextNode() //创建一个文本节点\*
- 添加、移除、替换、插入
  - appendChild() \* removeChild()
  - replaceChild() \* insertBefore() //在已有的子节点前插入一个新的子节点
- 查找
  - getElementsByTagName() //通过标签名称
  - getElementsByName() //通过元素的 Name 属性的值(IE 容错能力较强，会得到一个数组，其中包括 id 等于 name 值的)
  - getElementById() //通过元素 Id，唯一性

## 重绘与回流

- 当元素的样式发生变化时，浏览器需要触发更新，重新绘制元素。这个过程中，有两种类型的操作，即重绘与回流。
- 回流必定触发重绘，重绘不一定触发回流。重绘的开销较小，回流的代价较高

- 重绘(repaint):

  - 当元素样式的改变不影响布局时，浏览器将使用对元素进行更新
  - 只需要 UI 层面的重新像素绘制，损耗较少

- 回流(reflow):

  - 当元素的尺寸、结构或触发某些属性时，浏览器会重新渲染页面，称为回流
  - 浏览器需要重新经过计算，计算后还需要重新页面布局，因此是较重的操作

## 会触发回流的操作

- 页面初次渲染
- 浏览器窗口大小改变
- 元素尺寸、位置、内容发生改变
- 元素字体大小变化
- 添加或者删除可见的 dom 元素
- 激活 CSS 伪类（例如：:hover）
- 查询某些属性或调用某些方法
  - clientWidth
  - scrollTo()

## Ascii、GBK、UTF、Unicode
- Ascii（1 个字节）
- GBK 是国内的编码标准（2 个字节）
- Unicode 是国际编码标准（2 个字节）
- UTF 是 Unicode 实现的另一个标准
- UTF-8 就是每次 8 个位传输数据： 联网上使用最广的一种 unicode 的实现方式
- UTF-8 最大的一个特点，就是它是一种变长的编码方式。
  - 它可以使用 1~4 个字节表示一个符号，根据不同的符号而变化字节长度，当字符在 ASCII 码的范围时，就用一个字节表示，保留了 ASCII 字符一个字节的编码做为它的一部分，注意的是 unicode 一个中文字符占 2 个字节，而 UTF-8 一个中文字符占 3 个字节）。
- 从 unicode 到 utf-8 并不是直接的对应，而是要过一些算法和规则来转换。

## 事件冒泡
- event bubbling: event bubbles up the dom tree, calling all the event handlers on the path
- `this` (event.currentTarget): the current element with event handler
- `event.target`: element that initiated the event
- `event.stopPropagation()`: stop event bubbling

## 事件捕捉
- event capturing: 
- 3 phases of dom events
  - Capturing phase – the event goes down to the element. <===
  - Target phase – the event reached the target element.
  - Bubbling phase – the event bubbles up from the element.
- syntax: `element.addEventListener(..., true)`

## 事件代理
- define event handler on the common parent
- check if event.target is within the element of interest
- handle the event

## requestAnimationFrame vs setTimeout
- requestAnimationFrame execute in sync with monitor refresh
- requestAnimationFrame doesn't wait for sync task in the main thread
