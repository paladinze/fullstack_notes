# Optimization

## get current performance in chrome
- open chrome dev tools
- click audit tab
- generate report
  - click view trace to see rendering timestamps
- key metrics
  - first image or text is painted: `first contentful paint (fcp)` <== **how fast to load**
  - primary content visible: `first meaningful paint (fmp)`
  - how quickly contents are visible: `speed index`
  - main thread quite enough to handle input: `first CPU idle`
  - time till fully interactive: `time till interactive (tti)`
  - duration of longest task: `maxium possible first input delay (fid)` <== **how responsive during load**

## 整体优化策略
- FE
  - critical render path
    - CSS placed in Head
    - JavaScript at the end of body
  - optimized code
  - progressive web app
- Network
  - minimize files
    - code: minify + uglify
    - image: use image compressor (ex. PngQuant, jpegoptim)
      png: pngquant --quality 60-75 --ext .png  **/*.png - --force
      - jpeg: jpegoptim  -m 75 **/*.jpg
      - 使用 CDN 加速
    - online service: tinypng
  - minimize deliverty
- BE
  - CDN
  - caching
  - load balancing
  - db scaling
  - enable gzip compression for static resources


## 前端性能优化
- 减少 HTTP 请求次数
  - 在客户端重复利用数据
- 合理控制 cookie 大小（每次请求都会包含 cookie）
- DOM优化
  - 用innerHTML代替DOM操作
  - 减少 DOM 操作次数
  - 避免不必要的重绘与重排
- CSS优化
  - 优化 CSS 选择器（从右向左匹配）
  - 当需要设置的样式很多时设置className而不是直接操作style
  - 使用 CSS Sprite
  - 避免使用CSS Expression（css表达式)又称Dynamic properties(动态属性)


## 页面大量图片，如何优化加载，优化用户体验
- 图片懒加载。在页面的未可视区域添加一个滚动事件，判断图片位置与浏览器顶端的距离与页面的距离，如果前者小于后者，优先加载。
- 如果为幻灯片、相册等，可以使用图片预加载技术，将当前展示图片的前一张和后一张优先下载。
- 如果图片为css图片，可以使用CSSsprite，SVGsprite等技术。
- 如果图片过大，可以使用特殊编码的图片，加载时会先加载一张压缩的特别厉害的缩略图，以提高用户体验。
- 如果图片展示区域小于图片的真实大小，应在服务器端根据业务需要先进行图片压缩，图片压缩后大小与展示一致。


## 首屏时间、白屏时间
Performance 接口可以获取到当前页面中与性能相关的信息。<br>
该类型的对象可以通过调用只读属性 Window.performance 来获得。<br>
白屏时间：
```
performance.timing.responseStart - performance.timing.navigationStart
```
首屏时间
```
window.onload = () => {
    new Date() - performance.timing.responseStart
}
```
https://developer.mozilla.org/zh-CN/docs/Web/API/Performance



* What tools would you use to find a performance bug in your code?
* What are some ways you may improve your website's scrolling performance?
* Explain the difference between layout, painting and compositing.