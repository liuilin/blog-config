### CSS 学习资源

最好的调试方式：加 border.

> 想知道自己 CSS 写的好不好就去 dribble 去找一个来实现

1.  Google: 关键词 MDN
2.  [CSS Tricks](https://css-tricks.com/)
3.  [Google: 阮一峰 css](https://www.google.com/search?q=%E9%98%AE%E4%B8%80%E5%B3%B0+css)
4.  [张鑫旭的 240 多篇 CSS 博客](http://www.zhangxinxu.com/wordpress/category/css/page/25/)
5.  [Codrops 炫酷 CSS 效果](https://tympanus.net/codrops/category/playground/)
6.  [CSS 揭秘](http://www.ituring.com.cn/book/1695)
7.  [CSS 2.1 中文 spec](http://cndevdocs.com/)
8.  [Magic of CSS](http://adamschwartz.co/magic-of-css/) 免费在线书

> 建议：中文学习资源只看大 V 的（毕竟他们要维护形象不能瞎写），英文资源看 CSS Tricks、MDN 和 Codrops。书的话作用不大，最权威的书其实是文档。

-   如果你想快速上手，就先写小 demo 再学理论。
-   如果你想一鸣惊人，就仔细看 CSS 规范文档。

###  知识点

1. 如何做横向布局（左右 float + clearfix）

2. 如何取色、量尺寸、预览字体（Word）

3. 如何使用开发者工具查看样式、继承样式

4. 四种引入 CSS 的方式：style 属性、style 标签、css link、css import

5. 常见 CSS 属性：

- font-family font-size font-weight
- ul、body 的默认 margin 和 padding
- color、background-color、margin、padding
- line-height

### 周边工具

- LESS CSS
  一种简化、功能更多的 CSS 语言 [中文官网](https://www.google.com/search?q=less+css+%E4%B8%AD%E6%96%87) [英文官网](https://www.google.com/search?q=less+css)
- SASS
  一种简化、功能更多的 CSS 语言（请自行搜索中英文官网）
- PostCSS
  一种 CSS 处理程序

我的建议是，先不要看周边工具，学好最朴素的 CSS，然后升级就很容易了。

### 布局与定位

> IDE live template：.clearfix 清除浮动

- 块级元素高度：由内部 **文档流** 高度的总和决定的

- 文档流：内联元素从左往右，块级元素从上到下另起一行

- 内联元素高度（基本不可测）：由字体决定，浏览器会读取字体设计的建议行高

  > 内联元素不接受宽高（宽度由元素决定），把它转为块元素（display:inline-block;）
  >
  > 用 display:inline-block; 转为内联元素后，需要加入 vertical-align：top 来修复尾部 bug
  >
  > 转为内联元素后居中方式：text-align : center;
  >
  > 方应杭 css line height

- 宽高能不写就不写，容易有 bug

  > span 里面用 padding:4px 16px;line-height:22px; 来替换 width:70px; height:29px; line-height:29px; text-align: center; 
  
- 绝对定位是脱离文档流的，那它们就不知道容器有多高（所以要给个高度）

- 推荐优先使用 padding，可以配合 border-box

- 字体之类的就看淘宝、京东这类大网站，天天有人看不会出错

### 在线工具

css3 linear gradient generator：渐变

css animation generator：动画

css shadow generator：阴影

> 出现问题之后看不出来可以去 mdn 找正确的例子，在上面的基础上修改

web page free psd：设计素材

### Tricks

1. 父元素高度有了，子元素高度可写 100%（父变子变）
2. css 层级最好不要超过 5 个，超了就考虑重新起一个名字
3. 命名：bar-inner，<kbd>-</kbd> 只用来做结构（表示内部的 bar），不作为起名字
4. 写 CSS 要从内到外，从上到下