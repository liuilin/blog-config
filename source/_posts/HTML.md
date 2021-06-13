---
title: HTML
date: 2021-03-20 08:41:29
tags: HTML
---
# HTML

> div {盒子 $}*10

1. Google：HTML spec（规范文档 specification）

2. 简历模板：https://scardwp.px-lab.com/

3. 验证写的 HTML 正确性：https://validator.w3.org/

4. HTML（只规定页面上有什么）常见标签：a、form、input、button、h1、p、ul、ol、small、strong、div、span、kbd、video、audio、svg 

   - 除了 div 和 span，其他标签都有默认样式（在 Chrome 控制台 style 灰色部分可看到，-webkit）

     > 要给 class（驼峰命名），因为 div 是没有意义的标签，不给 class 就不知道什么意思。不能只用 div 和 span，那样需要加很多 class
     >
     > ul：un-order list
     >
     > li：list item
     >
     > dl：description list
     >
     > dt：description term
     >
     > dd：description definition

   - MDN 上有所有标签的文档

   > 不知道的单词：iciba.com/ 导航 => navigation => Google：navigation mdn 找到 <nav> 标签

5. 如何查看 MDN 文档（查看是否有此标签）

   e.g. strong mdn

   main md：<main>

6. 查看标签默认属性：如果 style 里面没看到则到 computed 里面搜索

7. CSS 布局要么横向、要么纵向，这样划分 HTML 的块容易写 CSS（等有 Grid 的时候也就不用多加 div 了）

8. npm i -g http-server：http-server -c-1 不带缓存开启服务

9. iframe 标签：嵌套页面

   <iframesrc="https://www.baidu.com" name="xxx"></iframe>

10. a 标签：跳转页面（HTTP GET 请求）

    > <a href="javascript:;">QQ</a>
    >
    > i. //qq. com
    >
    > ii. #xxx?name=qqqq./xxx. html
    >
    > iii. javascript: alert (1); javascript:;
    >
    > <iframe name="xxx" src="./index.html"frameborder=1"0"></iframe>
    ><a href=""target="xxx"></a>（target 指跳转到哪）

11. form 标签：跳转页面（HTTP POST 请求）

12. input /button

13. table

> 标签属性 Google mdn
>
> 完成 w3schools 的测试题
