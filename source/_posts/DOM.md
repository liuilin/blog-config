**1**       **DOM 是一棵树（tree）**

**2**       **树上有** **Node**

Node 分为 Document（html）、Element（元素）和 Text（文本），以及其他不重要的。

**3**       **Node 的接口**

\1.  属性

childNodes,firstChild,innerText,lastChild,nextSibling,nodeName,nodeType,nodeValue,outerText,ownerDocument,parentElement,parentNode,previousSibling,textContent

妈的记不住。
 如果记不住就背下以下单词：

- child / children / parent

- node

- first / last

- next / previous

- sibling / siblings

- type

- value / text / content

- inner / outer

- element
 然后互相组合

\2.  方法（如果一个属性是函数，那么这个属性就也叫做方法；换言之，方法是函数属性）

- appendChild()

- cloneNode()

- contains()

- hasChildNodes()

- insertBefore()

- isEqualNode()

- isSameNode()

- removeChild()

- replaceChild()

- normalize() // 常规化

\1.  搞清楚英文单词的意思就知道用法

\2.  如果发现知道英文后依然不明白用法，看 MDN 的例子即可，如 [normalize](https://developer.mozilla.org/en-US/docs/Web/API/Node/normalize)

DOM APi 无外乎「增删改查」

**4**       **Document 接口**

属性

- anchors

- body

- characterSet

- childElementCount

- children

- doctype

- documentElement

- domain

- fullscreen

- head

- hidden

- images

- links

- location

- onxxxxxxxxx

- origin

- plugins

- readyState

- referrer

- scripts

- scrollingElement

- styleSheets

- title

- visibilityState

方法：

- close()

- createDocumentFragment()

- createElement()

- createTextNode()

- execCommand()

- exitFullscreen()

- getElementById()

- getElementsByClassName()

- getElementsByName()

- getElementsByTagName()

- getSelection()

- hasFocus()

- open()

- querySelector()

- querySelectorAll()

- registerElement()

- write()

- writeln()

**5**       **Element 的接口**

**6**       **DOM API 反人类**

\1.  获取元素

以前之后 document.getElementById, document.getElementsByTagName, document.getElementsByClassName
 太反人类，于是有了 jQuery
 后来 DOM API 终于抄袭 jQuery 提供了 document.querySelector 和 document.querySelectorAll
 但是依然没有 jQuery 好用，因为「不一致」

\1.  获取下一个元素

获取兄弟们