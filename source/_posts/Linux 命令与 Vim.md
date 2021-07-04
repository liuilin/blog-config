---
title: Linux 命令与 Vim
date: 2021-03-20 08:41:29
tags: 
---
# Linux 命令与 Vim

### Linux 命令
[Linux工具快速教程 — Linux Tools Quick Tutorial](https://linuxtools-rst.readthedocs.io/zh_CN/latest/index.html)

> GitHub：服务器配置 https://gist.github.com/search?o=desc&q=.bashrc&s=stars

#### 常见的自带命令

| ** 操作 **              | ** 命令 **                                                                                     |
| ----------------------- | ---------------------------------------------------------------------------------------------- |
| 进入目录                | cd                                                                                             |
| 显示当前目录            | pwd                                                                                            |
| 创建目录                | mkdir 目录名                                                                                   |
| 创建目录                | mkdir -p 目录路径                                                                              |
| 我是谁                  | whoami                                                                                         |
| --                      | --                                                                                             |
| 查看路径                | ls 路径                                                                                        |
| 查看路径                | ls -a 路径                                                                                     |
| 查看路径                | ls -l 路径                                                                                     |
| 查看路径                | ls -al 路径                                                                                    |
| --                      | --                                                                                             |
| 创建文件 / 覆盖原有文件 | echo "1" > 文件路径                                                                            |
| 强制创建文件            | echo "1" >! 文件路径                                                                           |
| 追加文件内容            | echo "1" >> 文件路径                                                                           |
| 创建文件                | touch 文件名                                                                                   |
| 改变文件更新时间        | touch 文件名                                                                                   |
| --                      | --                                                                                             |
| 复制文件                | cp 源路径 目标路径                                                                             |
| 复制目录                | cp -r 源路径 目标路径                                                                          |
| --                      | --                                                                                             |
| 移动节点                | mv 源路径 目标路径                                                                             |
| --                      | --                                                                                             |
| 删除文件                | rm 文件路径                                                                                    |
| 强制删除文件            | rm -f 文件路径                                                                                 |
| 删除目录                | rm -r 目录路径                                                                                 |
| 强制删除目录            | rm -rf 目录路径                                                                                |
| --                      | --                                                                                             |
| 查看目录结构            | tree                                                                                           |
| 建立软链接              | ln -s 真实文件 链接                                                                            |
| --                      | --                                                                                             |
| 下载文件                | curl -L [https://www.baidu.com](https://www.baidu.com/) > baidu.html                           |
| 拷贝网页                | wget -p -H -e robots=off [https://www.baidu.com](https://www.baidu.com/) (Windows 不支持 wget) |
| 磁盘占用                | df -kh                                                                                         |
| 当前目录大小            | du -sh .                                                                                       |
| 各文件大小              | du -h                                                                                          |

> Google: Linux 查看文件内容
>
> Linux 命令：https://explainshell.com/	只展示精选命令 https://github.com/tldr-pages/tldr

#### 快捷键

- <kbd>↑</kbd> <kbd>↓</kbd> 上一命令 / 下一命令

- <kbd>!</kbd> 上一命令占位符

- <kbd>Tab</kbd> 自动补全路径

- <kbd>Alt</kbd>+<kbd>.</kbd> 上一命令的最后一个参数

- && 前面的执行成功了，再执行后面的

- || 前面的执行失败了，就执行后面的

- ; 前面执行完了，不管成功失败，就执行后面的

- \> 重定向

- | 管道



### Vim

#### 如何学习 vim

1. 在命令行输入 vimtutor ，即可查看官方自带的中文教程

2. [简明 VIM 练级攻略](http://coolshell.cn/articles/5426.html)

3. [一个 vim 游戏](https://vim-adventures.com/)

#### 命令

技巧：Vim 的纵向编辑模式：https://www.ibm.com/developerworks/cn/linux/l-cn-vimcolumn/index.html

1. Vim 分为一个 operation 和一个 motion

2. i 写入模式、i 插入之前、a 插入之后、A 行尾插入、I 行首插入、o 下行插入、O 上行插入 x 删除光标后一个字符，u 是撤销 U、Ctrl+r
   d + ←→删除光标←→字符（d +3←）、dd 删除一行（其实是剪切，p 粘贴）
   y+ ←→复制光标←→字符 （y+3←）
   
   db/dw/de/x
   
   剪切括号等内的内容（进入插入模式）：<kbd>ci”</kbd><kbd>ci’</kbd><kbd>ci [</kbd><kbd>ci (</kbd>
   
   剪切括号等内的内容：dt”、di”、diw
   
   剪切括号等内的内容：yi”
   
   剪切到制定字符：c/d/y f% s
   
   c 删除并进入写入模式、w 光标向下移动一个词、cw 删除一个词并进入写入模式、b 光标到上一个词 、ciw 词中删除一个词并进入写入模式，yi
   
   f：找当前行的词
   / 搜索、n 下 N 上
   
   (n) p/P：粘贴 n 行
   
4. 移到行首：^ 

4. 移到行尾：$

5. 多行缩进：/10,100>

6. V 选区 v 反选：之后 y、p、d

   选中直至末尾：v$；并插入

   删除整页：VGd

   v 选区后，Alt+j 选择并替换

7. 【y i c d f 】
   esc 回到正常模式
   ：w 保存
   ：q 退出 vim
   ：source $MYVIMRC 刷新 vim
   jkhl 上下左右
   ：split 上下分屏 、：vsplit 左右分屏 Q 退出
   ~/.vim/vimrc
   noremap a b a 键改 b 键
   map a b a 键改 b 键
   syntax on 打开高亮
   set number 显示行号
   set wildmenu ：命令补全
   set hlsearch / 搜索高亮
   set incsearch 一面输入一面高亮
   set ignorecase 忽略大小写 43：35 美化！

#### 插件

Google：best vim/idea/vscode config github 找到

vim plugin site:github.com

github：

- vim-plug
- snazzy



<!-- 待整理 -->
## 批量插入

VISUAL 批量选中模式下（<kbd>gg</kbd> - <kbd>V</kbd> - <kbd>G</kbd>），:'<,'>normal Imy-wallpaper-，就会进入 normal 模式，批量在最前面加上 my-wallpaper-

此时我突然不想加前缀 my-，先进入可视块 VISUAL BLOCK 模式（<kbd>Ctrl</kbd> + <kbd>v</kbd> - <kbd>G</kbd>），<kbd>f</kbd> - <kbd>-</kbd> - <kbd>d</kbd>，删除成功。
突然我又看 wallpaper 单词不顺眼，想批量把首字母 w 改为大写，依次输入 <kbd>Ctrl</kbd> + <kbd>v</kbd> - <kbd>G</kbd> - <kbd>g</kbd> - <kbd>U</kbd>

> gu：切换为小写
> gU：切换为大写
> g~：大小写切换
>
> H    移到屏幕顶部,high
> M    移到屏幕中央,middle
> L    移到屏幕底部,low



:e ~/.vimrc：vim normal 模式下编辑文件

### vim 删除当前屏内容命令

<kbd>HVLd</kbd>

### 正则给 markdown 文件批量添加 <kbd> 符号

### 多行折叠为一行
wget
vim
touch

vim command: 
In command mode:

```
[range]j[lines]
```

For example: here you want to do the whole buffer:

```
%j
```

If you just wanted to do 10 lines from the current cursor position:

```
j10
```

If you don’t want to replace the new lines with spaces, use ! after j.

```
%j!
j!10
```

And for the uberfancy:

```
5j20
```

It would go to line 5, and join the next 20 lines.