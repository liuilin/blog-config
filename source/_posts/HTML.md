# HTML

> div{盒子$}*10

1. Google：HTML spec（规范文档specification）

2. 简历模板：https://scardwp.px-lab.com/

3. 验证写的HTML正确性：https://validator.w3.org/

4. HTML（只规定页面上有什么）常见标签：a、form、input、button、h1、p、ul、ol、small、strong、div、span、kbd、video、audio、svg 

   - 除了div和span，其他标签都有默认样式（在Chrome控制台style灰色部分可看到，-webkit）

     > 要给class（驼峰命名），因为div是没有意义的标签，不给class就不知道什么意思。不能只用div和span，那样需要加很多class
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

   - MDN上有所有标签的文档

   > 不知道的单词：iciba.com/导航 => navigation => Google：navigation mdn 找到<nav>标签

5. 如何查看MDN文档（查看是否有此标签）

   e.g. strong mdn

   main md：<main>

6. 查看标签默认属性：如果style里面没看到则到computed里面搜索

7. CSS布局要么横向、要么纵向，这样划分HTML的块容易写CSS（等有Grid的时候也就不用多加div了）

8. npm i -g http-server：http-server -c-1不带缓存开启服务

9. iframe 标签：嵌套页面

   <iframesrc="https://www.baidu.com" name="xxx"></iframe>

10. a 标签：跳转页面（HTTP GET 请求）

    > <a href="javascript:;">QQ</a>
    >
    > 1. //qq. com
    > 2. #xxx?name=qqqq./xxx. html
    >
    > 3. javascript: alert(1); javascript:;
    >
    > <iframe name="xxx" src="./index.html"frameborder=1"0"></iframe>
    ><a href="" target="xxx"></a>（target指跳转到哪）

11. form 标签：跳转页面（HTTP POST 请求）

12. input / button

13. table

> 标签属性Google mdn
>
> 完成w3schools的测试题