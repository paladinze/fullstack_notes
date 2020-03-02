## 介绍一下你对浏览器内核的理解？

- 主要分成两部分：渲染引擎和 JS 引擎
- 渲染引擎
  - 取得网页的内容（HTML、XML、图像等等）
  - 整理讯息（例如加入 CSS 等）
  - 计算网页的显示方式，然后会输出至显示器
- JS 引擎

  - 解析和执行 javascript
  - 执行栈

- 主要线程
  - 事件触发线程
    - 消息队列： 微任务 + 宏任务
  - 网络异步线程
  - 定时器线程

## 常见的浏览器内核有哪些？

- Webkit 内核：Chrome, Safari, Edge, 360, opera
- Trident 内核：IE
- Gecko 内核：Firefox

## 跨标签页通讯

- 设置同域下共享的 localStorage
  - 监听 window.onstorage
  - 重复写入相同的值无法触发
  - 会受到浏览器隐身模式等的限制
- 通过父页面 window.open()和子页面 postMessage
- 设置共享 cookie 与不断轮询脏检查(setInterval)

## 浏览器的缓存机制

- 浏览器对于缓存的处理是根据第一次请求资源时返回的响应头来确定的
- 从缓存位置上来说分为四种，并且各自有优先级，当依次查找缓存且都没有命中的时候，才会去请求网络。

- Service Worker
- Memory Cache
  - 样式、脚本、图片
  - 关闭 Tab 页面，内存中的缓存就被释放了
- Disk Cache
  - 会根据 HTTP Header 中的字段判断哪些资源需要缓存，哪些资源可以不请求直接使用，哪些资源已经过期需要重新请求
- Push Cache
  - Push Cache（推送缓存）是 HTTP/2 中的内容
  - 只在会话（Session）中存在，一旦会话结束就被释放，
  - 缓存时间很短暂，在 Chrome 浏览器中只有 5 分钟左右

## 强缓存 vs 协商缓存

- 强缓存

  - 通过设置两种 HTTP Header 实现：Expires 和 Cache-Control。
  - Cache-Control:max-age=300 时，则代表在这个请求正确返回时间（浏览器也会记录下来）的 5 分钟内再次加载资源，就会命中强缓存。
  - Expires： 响应 http 请求时告诉浏览器在过期时间前浏览器可以直接从浏览器缓存取数据，而无需再次请求
    - HTTP/1 的产物,现阶段它的存在只是一种兼容性的写法

- 协商缓存
  - 协商缓存就是强制缓存失效后，浏览器携带缓存标识向服务器发起请求，由服务器根据缓存标识决定是否使用缓存的过程
  - 协商缓存可以通过设置两种 HTTP Header 实现：Last-Modified 和 ETag 。
    - ETag
      - Etag 是服务器响应请求时，返回当前资源文件的一个唯一标识(由服务器生成)，只要资源有变化，Etag 就会重新生成
- 强制缓存优先于协商缓存进行，若强制缓存(Expires 和 Cache-Control)生效则直接使用缓存，若不生效则进行协商缓存(Last-Modified / If-Modified-Since 和 Etag / If-None-Match)
- 协商缓存由服务器决定是否使用缓存，若协商缓存失效，那么代表该请求的缓存失效，返回 200，重新返回资源和缓存标识，再存入浏览器缓存中；生效则返回 304，继续使用缓存

- 实际场景应用缓存策略

  - 频繁变动的资源
    - Cache-Control: no-cache
    - 不能节省请求数量，但是能显著减少响应数据大小
  - 不常变化的资源
    - Cache-Control: max-age=31536000

- 用户行为对浏览器缓存的影响
  - 打开网页，地址栏输入地址：
    - 查找 disk cache 中是否有匹配。如有则使用；如没有则发送网络请求。
  - 普通刷新 (F5)
    - memory cache 是可用的，会被优先使用,其次才是 disk cache。
  - 强制刷新 (Ctrl + F5)：
    - 浏览器不使用缓存，因此发送的请求头部均带有 Cache-control: no-cache
    - 服务器直接返回 200 和最新内容。
