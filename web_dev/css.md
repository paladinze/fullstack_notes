# CSS


## why stylesheet
- seperation of concern
- cacheable
- don't bloat html

## syntax
<selector> {
  css_property: value;
}

## selectors
- univerlsal selector: *
- element selector: h1
- id selector: #item-id
- class selector: .class-name
- attribute selector: [disabled]

## combinators
- direct descendent: >
- adjacent sibling: +
- general descendent: " "


## select priorities
- Importance > specific > source order
- 继承的样式和直接指定的样式冲突时，直接指定的样式获胜
- 直接指定的样式发生冲突时，样式权值高者获胜
  - 选择器优先级： !important > inline > #id > .class > tag > \* > 继承 > 默认
  - 选择器 从右往左 解析
- 样式权值相同时，后者获胜

## naming convention: BEM
- purpose
  - guarantee uniqueness across your entire application.
  - avoids specificity and inheritance issues
- format: Blocks__Elements--Modifiers
- never nest selectors or select anything other than one single CSS class in your CSS files

## Design System
- Part 1: Typography
	- typeface (font family)
	- typescale
	- repsonsiveness (size unit & breakpoint)
	- spacing & vertical rhythm
	- colors
- Part 2: Grid & Layout
- Part 3: Colors
- Part 4: Spacing
- Part 5: Icons
- Part 6: Buttons

## flexbox
- define flexbox
  - display: flex
  - justify-content: space-around / space-between
  - align-items: space-around / space-between
- items in flex
  - flex: 2

## css grid
- define grid
  - display: grid
  - grid-gap: 10px
  - `grid-template: <row1-height> <row2-height> / <col1-width> <col2-width>`
    - grid-template-rows
    - grid-template-columns
- items in grid
  - `grid-area: <row-start> / <column-start> / <row-end> / <column-end>`
    - grid-row-start
    - grid-row-end
    - grid-column-start
    - grid-column-end
- examples: 2rows * 3columns
  - 1st row: item2, item3, 3rd column empty
  - 2nd row: item1 spans two columns, 3rd column empty
    ```css
    .container {
      display: grid;
      grid-template: 1fr 1fr / repeat(3, 1fr);
    }
    .item1 {
      grid-area: 2 / 1 / 2 / span 2;
      background: red;
    }
    .item2 {
      background: green;
    }
    .item3 {
      background: yellow;
    }
    ```

## CSS design considerations

- Use Low-Specificity Selectors

```css
/* bad */
.navigation a {
  color: blue;
}

/* good */
.nav-link {
  color: blue;
  font-size: 2rem;
}

.nav-link-red {
  color: red;
}
```

- Don't Use ID or Element Selectors
- Don't Use Inline Styles
- Don't Use !important
- Don't Depend on a Certain Markup Structure

```css
/* bad */
.header ul li a {
  margin-right: 20px;
}

/* good */
.header-link {
  margin-right: 20px;
}
```

- Prefix Modifier Classes

```css
/* bad */
.btn {
  padding: 0.25em;
  background-color: blue;
  color: white;
}

.btn.red {
  background-color: red;
}

/* good */
.btn {
  padding: 0.25em;
  background-color: blue;
  color: white;
}

.btn-red {
  background-color: red;
}
```

- Write Small Rules

```css
.text-white {
  color: #fff;
}

.text-underline {
  text-decoration: underline;
}
```


## 如何计算相对单位的实际像素

- %(font): relative to parents' font-size
- %(length): relative to parents' width
- em(font): relative to parents' font-size
- em(length): relative to current font-size
- rem: relative to root font-size
- vh: 1% of viewport height
- vw: 1% of viewport width

## 盒模型

- 页面渲染 DOM 元素所采用的 布局模型
  - margin + border + padding + content
- 可通过 box-sizing 进行设置。
- 根据计算宽高的方法可分为：
  - content-box (W3C 标准盒模型)
    - 宽高指 content
  - border-box (IE 盒模型)
    - 宽高指 border + padding + content
- 正常模式下所有浏览器都是 W3C 盒子模型

## BFC 是什么？

- 一个独立的渲染区域，让处于 BFC 内部的元素与外部的元素相互隔离，使内外元素的定位不会相互影响。
- 如果一个元素符合成为 BFC 的条件，该元素内部元素的布局和定位就和外部元素互不影响，是一个独立容器
- 形成 BFC 的条件

  - position: absolute/fixed
  - float：除 none 以外的值
  - position：absolute/ fixed
  - display 为以下其中之一的值 inline-blocks，table-cells，table-captions；
  - overflow !== visible

- BFC 布局规则

  - 内部的 Box 会在垂直方向，一个接一个地放置。
  - Box 垂直方向的距离由 margin 决定。属于同一个 BFC 的两个相邻 Box 的 margin 会发生重叠
  - 每个元素的 margin box 的左边， 与包含块 border box 的左边相接触(对于从左往右的格式化，否则相反)。即使存在浮动也是如此。
  - BFC 的区域不会与 float box 重叠。
  - BFC 就是页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面的元素。反之也如此。
  - 计算 BFC 的高度时，浮动元素也参与计算

- 有什么用
  - 自适应两栏布局
  - 可以阻止元素被浮动元素覆盖
  - 阻止 margin 重叠

## 清除浮动

- 方法 1：使用带 clearfix 的空元素
  - 在浮动元素后使用一个空元素如<div class="clearfix"></div>，并在 CSS 中赋予{clear:both;}

```css
.clearfix {
  clear: both;
}
```

- 方法 2：使用 CSS 的:after 伪元素
  - 给浮动元素的容器添加一个 clearfix 的 class，然后给这个 class 添加一个:after 伪元素实现元素末尾添加一个看不见的块元素（Block element）清理浮动。

```css
.row:after {
  content: "";
  display: box;
  clear: both;
}
```

## 层叠上下文

- 元素提升为一个比较特殊的图层，在三维空间中 (z 轴) 高出普通元素一等
- 触发条件
  - 根层叠上下文(html)
  - position
  - css3 属性
    - flex
    - transform
    - opacity
    - filter
    - will-change
- 层叠等级：层叠上下文在 z 轴上的排序
  - 在同一层叠上下文中，层叠等级才有意义

## 块级元素 vs 行内元素

- 块级元素（block）
  - 占据其父元素（容器）的整个空间
  - 通常浏览器会在块级元素前后另起一个新行
  - 例子：div，h1，p，ul
- 行内元素（inline）
  - 一个行内元素只占据它对应标签的边框所包含的空间
  - 包含其自身及其他行内元素
  - 例子：span，a，input，button
- 行内块元素（inline-block）
  - 和 inline 一样，但可以设宽高
- 区别
  - 一般行内元素只能包含数据和其他行内元素，块级元素可以包含行内元素和自身及其他块级元素。
  - 默认情况下块级元素占用一整行，而行内元素占据自身宽度空间
  - 宽高只对块级元素生效
  - 行内元素只能设置 padding 及左右 margin，上下 margin 无用
  - 设置 padding 时左右推开距离，上下会延申出去，但不会增加上下两行间的距离。
  - 如果给行内元素设定绝对定位，会隐形的改变 a 的 display 为 inline-block，此时就可以把 a 当成块元素一样设置宽高了。

## position 的定位区别：

- absolute 生成绝对定位的元素，相对于 static 定位以外的第一个祖先元素进行定位。
- fixed 生成绝对定位的元素，相对于浏览器窗口进行定位（老 IE 不支持）。
- relative 生成相对定位的元素，相对于其在普通流中的位置进行定位。
- static 默认值。没有定位，元素出现在正常的流中（忽略 top, bottom,
- left, right z-index 声明）。
- inherit 规定从父元素继承 position 属性的值。

## 垂直水平剧中方案

```html
<div class="father">
  <div class="child"></div>
</div>
```

- method 1: flexbox + margin

```css
.father {
  display: flex;
}
.child {
  margin: auto;
}
```

- method 2: flexbox + justify + align

```css
.father {
  display: flex;
  justify-content: center;
  align-items: center;
}
.child {
}
```

- method3: absolute + translate

```css
.father {
  position: relative;
}
.child {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
```

## 隐藏方案

```
{ display: none; }  <= 导致页面重绘，不占用空间
{ visibility: hidden; } <= 不会导致页面重绘，仍占用空间
{ height: 0; overflow: hidden; }
{ position: absolute; top: -999em; }
{ position: relative; top: -999em; }
{ position: absolute; visibility: hidden; }
```

## link 与 @import 的区别

- link 功能较多，可以定义 RSS，定义 Rel 等作用，而@import 只能用于加载 css
- 当解析到 link 时，页面会同步加载所引的 css，而@import 所引用的 css 会等到页面加载完才被加载
- link 可以使用 js 动态引入，@import 不行

# web design best practices

- text font-size: 15px - 25px
- line spacing: 120% - 150%
- characters per line: 45 - 90
- font： sans , serif, lato
  color:
- use only one base color
- text over image
- white text over dark background
- overlay image with dark layer
- floor fade
- icon: use icon font whenever possible

## 用 css 画一个三角形

```css
.caret {
  width: 0;
  height: 0;
  border: 50px solid transparent;
  border-top-color: black;
}
```

## 响应式设计

- fluid grid: layout sized in relative units
  - examples:
    - https://github.com/grahammiller/ResponsiveGridSystem
- images: sized ized in relative units
- media queries: different css rules based on width

* Viewport meta tag

```html
<meta
  name="viewport"
  content="width=device-width,height=device-height,inital-scale=1.0,maximum-scale=1.0,user-scalable=no;"
/>
```

- 栅格系统

```css
 8 *{
 9     box-sizing:border-box;
10 }
15 /* 所有列左浮动 */
16 [class*="col-"]{
17     float:left;
18     padding:15px;
19     border:1px solid red;
20 }
21 /* 清除浮动 */
22 .row:after{
23     content:"";
24     display:block;
25     clear:both;
26 }
27 /* 每列的百分比： */
28 .col-1{width:8.33%;}
29 .col-2{width:16.66%;}
30 .col-3{width:25%;}
31 .col-4{width:33.33%;}
32 .col-5{width:41.66%;}
33 .col-6{width:50%;}
34 .col-7{width:58.33%;}
35 .col-8{width:66.66%;}
36 .col-9{width:75%;}
37 .col-10{width:83.33%;}
38 .col-11{width:91.66%;}
39 .col-12{width:100%;}
```


- media query
  common breakpoints
  ipad mini: 1024
  ipad: 1024
  ipad pro 10.5: 1112
  ipad pro 12.9: 1366
  small laptop: 1280


```css
@media (min-width:320px)  { /* smartphones, portrait iPhone, portrait 480x320 phones (Android) */ }
@media (min-width:480px)  { /* smartphones, Android phones, landscape iPhone */ }
@media (min-width:600px)  { /* portrait tablets, portrait iPad, e-readers (Nook/Kindle), landscape 800x480 phones (Android) */ }
@media (min-width:801px)  { /* tablet, landscape iPad, lo-res laptops ands desktops */ }
@media (min-width:1025px) { /* big landscape tablets, laptops, and desktops */ }
@media (min-width:1281px) { /* hi-res laptops and desktops */ }

```

```css
/* 移动端优先: */
[class*="col-"] {
  width: 100%;
}
@media only screen and (min-width: 768px) {
  /* 桌面： */
  .col-1 {
    width: 8.33%;
  }
  .col-2 {
    width: 16.66%;
  }
  .col-3 {
    width: 25%;
  }
  .col-4 {
    width: 33.33%;
  }
  .col-5 {
    width: 41.66%;
  }
  .col-6 {
    width: 50%;
  }
  .col-7 {
    width: 58.33%;
  }
  .col-8 {
    width: 66.66%;
  }
  .col-9 {
    width: 75%;
  }
  .col-10 {
    width: 83.33%;
  }
  .col-11 {
    width: 91.66%;
  }
  .col-12 {
    width: 100%;
  }
}
```

- 图片

  - 如果 width 属性设置为 100%，图片会根据上下范围实现响应式功能
  - max-width 属性设置为 100%，图片永远不会大于其原始大小

- 框架：Bootstrap
  - 必须理解容器（container）、行（row）和列（column）之间的层级关系。
  - container 是网格的容器，row（.row）必须位于 container 的内部，column（如 .col-sm-4）必须位于 row 的内部


## CSS history
	css 1: 1996
	css 2: 1998
	css 3: in dev
		the final version, future version tracked in feature modules

why stylesheet
	seperation of concern
	cacheable
	don't bloat html

check current browser font setting
	settings => appearance => customize font


## more questions
- What's the difference between "resetting" and "normalizing" CSS? Which would you choose, and why?
- Describe Floats and how they work.
- Describe z-index and how stacking context is formed.
- Describe BFC (Block Formatting Context) and how it works.
- What are the various clearing techniques and which is appropriate for what context?
- How would you approach fixing browser-specific styling issues?
- Are you familiar with styling SVG?
- Can you give an example of an `@media` property other than `screen`?
- Explain how a browser determines what elements match a CSS selector.
- What's the difference between the "nth-of-type()" and "nth-child()" selectors?
- What's the difference between a relative, fixed, absolute and statically positioned element?
- Have you ever worked with retina graphics? If so, when and what techniques did you use?
- Is there any reason you'd want to use `translate()` instead of _absolute positioning_, or vice-versa? And why?