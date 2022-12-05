---
title: Linux 命令与 Vim
date: 2021-03-20 08:41:29
tags: 
---
# Linux 命令与 Vim

### Linux 学习资料

[Baeldung on Linux](https://www.baeldung.com/linux/)

### Linux 目录详解

[Linux 目录结构 - 知乎](https://zhuanlan.zhihu.com/p/60423235)

[What does /opt mean in Linux? | Baeldung on Linux](https://www.baeldung.com/linux/opt-directory)

### Linux 命令

[【解析 Linux 命令行参数】explainshell.com - match command-line arguments to their help text](https://explainshell.com/)

[Linux工具快速教程 — Linux Tools Quick Tutorial](https://linuxtools-rst.readthedocs.io/zh_CN/latest/index.html)

[Linux命令搜索引擎 命令，Linux Linux命令搜索引擎 命令详解：最专业的Linux命令大全，内容包含Linux命令手册、详解、学习，值得收藏的Linux命令速查手册。 - Linux 命令搜索引擎](https://wangchujiang.com/linux-command/)

[Linux命令大全(手册) – 真正好用的Linux命令在线查询网站](https://www.linuxcool.com/)

> 搜索 GitHub 上的 Linux 配置 https://gist.github.com/search?o=desc&q=.bashrc&s=stars

### 实用命令

[【Find 实用命令】35 Practical Examples of Linux Find Command](https://www.tecmint.com/35-practical-examples-of-linux-find-command/)

使用名称查找文件，参数 -name 使用名称查找文件；-iname 使用名称并忽略大小写查找文件

查找根目录下的 MySQL 配置 my.cnf

```bash
find / -name 'my.cnf'
```

指定目录下搜索所有文件，且文件内容中包含端口为 “10888” 的文件

```bash
find /opt -type f -name '*' | xargs grep "10888"
```

基于正则表达式匹配文件路径

```shell
find . -regex ".*\(\.java\|\.python\)$"
```

根据文件类型进行搜索：f 普通文件 l 符号连接 d 目录 c 字符设备 b 块设备 s 套接字 p Fifo

```shell
find . -type 类型参数
```

使用名称查找 Java 类型的文件

```bash
find . -type f -name '*.java'
```

磁盘空间不够用时搜索大于 1G 的文件，单位 b c w k M G

```bash
find / -size +1G
```

#### `-exec`选项与其他命令结合使用

查找当前目录下所有.txt文件并把他们拼接起来写入到all.txt文件中

```shell
find . -type f -name "*.txt" -exec cat {} \;> /all.txt
```

找出当前目录下所有.txt文件并以“File:文件名”的形式打印出来

```shell
find . -type f -name "*.txt" -exec printf "File: %s\n" {} \;
```

找到匹配的文件并删除

```bash
find . \( -name '*.png' -o -name '*.jpg' \) -exec rm {} \;
```

#### 常见的自带命令

| **操作**                | **命令**                                                     |
| ----------------------- | ------------------------------------------------------------ |
| 进入目录                | cd                                                           |
| 显示当前目录            | pwd                                                          |
| 创建目录                | mkdir 目录名                                                 |
| 创建目录                | mkdir -p 目录路径                                            |
| 当前登录用户是谁        | whoami                                                       |
| --                      | --                                                           |
| 查看路径                | ls 路径                                                      |
| 查看路径                | ls -a 路径                                                   |
| 查看路径                | ls -l 路径                                                   |
| 查看路径                | ls -al 路径                                                  |
| --                      | --                                                           |
| 创建文件 / 覆盖原有文件 | echo "1" > 文件路径                                          |
| 强制创建文件            | echo "1" >! 文件路径                                         |
| 追加文件内容            | echo "1" >> 文件路径                                         |
| 创建文件                | touch 文件名                                                 |
| 改变文件更新时间        | touch 文件名                                                 |
| --                      | --                                                           |
| 复制文件                | cp 源路径 目标路径                                           |
| 复制目录                | cp -r 源路径 目标路径                                        |
| --                      | --                                                           |
| 移动节点                | mv 源路径 目标路径                                           |
| --                      | --                                                           |
| 删除文件                | rm 文件路径                                                  |
| 强制删除文件            | rm -f 文件路径                                               |
| 删除目录                | rm -r 目录路径                                               |
| 强制删除目录            | rm -rf 目录路径                                              |
| --                      | --                                                           |
| 查看目录结构            | tree                                                         |
| 建立软链接              | ln -s 真实文件 链接                                          |
| --                      | --                                                           |
| 下载文件                | curl -L [https://www.baidu.com](https://www.baidu.com/) > baidu.html |
| 拷贝网页                | wget -p -H -e robots=off [https://www.baidu.com](https://www.baidu.com/) (Windows 不支持 wget) |
| 磁盘占用                | df -kh                                                       |
| 当前目录大小            | du -sh .                                                     |
| 各文件大小              | du -h                                                        |



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



传统起一个服务 shell 脚本：

```shell
#!/bin/bash
baseName='ops-server'
cd /opt/ehr/ops-server
mv ./target/ops-server.jar ops-server.jar
kill -9 `cat java.pid`
nohup java -Djava.security.egd=file:/dev/./urandom -Xms512m -Xmx1024m -server -jar $baseName.jar  --spring.profiles.active=dev   > log.txt 2>&1 &
echo "$!" > java.pid
```



### 实战

实际遇到的问题：早上突然服务接口全部出现 Gateway 504

使用 `cat .bash_history` 发现之前有人执行了以下命令

```shell
cd /opt/ehr/
cd gateway/
./start.sh
cd ops-server/
./startDev.sh
```

他重启了 ops 项目服务，/opt/ehr/ops-server 下的目录如下

```bash
-rw-r--r--. 1 root root       770 Aug 30 15:16 bootstrap.yml
-rw-r--r--. 1 root root       242 Nov  7 16:14 Dockerfile
-rw-r--r--. 1 root root         5 Dec  1 10:04 java.pid
-rw-r--r--. 1 root root         0 Oct 31 17:37 log
drwxr-xr-x. 3 root root        24 Jun 28 16:15 logs
-rw-r--r--. 1 root root   2038118 Dec  1 10:21 log.txt
-rw-------. 1 root root     37064 Aug 30 15:07 nohup.out
-rw-r--r--. 1 root root 141348197 Dec  1 10:04 ops-server.jar
-rwxrwxrwx. 1 root root       332 Aug 30 15:15 startDev.sh
-rw-r--r--. 1 root root       290 Aug 29 15:20 start.sh
drwxr-xr-x. 2 root root         6 Dec  1 10:04 target
```



















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

   > ci" - change inside double quotes
   >
   > ci) - change inside curved brackets
   >
   > ci} - change inside curly brackets
   
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

   config: ~/.vim/vimrc

   let mapleader=" " " 将leader键（\键,类似于Windows键）换成空格（相当于空格键）
   syntax on " 开启语法高亮
   set number " 显示行号
   set relativenumber " 显示从当前行数的前后行数
   set cursorline " 高亮显示当前行
   set wrap " 自动换行
   set showcmd " 显示指令
   set wildmenu " vim 命令行命令补全
   set hlsearch " 高亮显示搜索
   set incsearch " 动态高亮搜索"
   set smartcase " 智能大小写搜索
   set ignorecase " 忽略大小写

   exec "nohlsearch" " 打开是运行指令 取消上回搜索内容的高亮"noremap a b " 将 a 替换为 b 
   "noremap A 5b " 将 A 替换为 5b
   "noremap = nzz " 将 n 替换为 =zz " 用 zz 将该行变成中心点
   "noremap - Nzz " 将 N 替换为 -zz
   noremap <LEADER><CR> :nohlearch<CR> " 将 <LEADER><CR> 替换为 :nohlearch<CR> 用于快捷取消搜索高亮

   map s <nop>  " 将 s 的指令设置为空
   map S :w<CR> " 将 S 的指令设置成 :w  “ <CR> 代表回车
   map Q :q<CR> " 将 Q 的指令设置成 :q
   map R :source $MYVIMRC<CR> " 将 R 的指令设置成 重载vimrc配置

   ":split  " 上下分屏 :q 退出
   ":vsplit " 左右分屏

   " <Operation(操作)> <Motion(动作)>
   " d 剪切操作(剪切可看做删除), y 复制操作, p 粘贴操作， c 剪切后修改操作
   " ← 左动作， → 右动作， 3← 3个左动作， b 选择光标开启到上一个词后的内容， i 指明光标在词中，当前词待操作， w 选择光标开始到下个词前的内容， iw 在当前词之间选择该， y3← 向右复制， f 查找动作

#### 插件

插件管理工具：[junegunn/vim-plug: Minimalist Vim Plugin Manager](https://github.com/junegunn/vim-plug)

example: add below to .vimrc
```vim
call plug#begin('~/.vim/plugged')
Plug 'connorholyday/vim-snazzy'
Plug 'vim-airline/vim-airline'
call plug#end()
```
:PlugInstall

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

### Vim Tricks
[At least one Vim trick you might not know • Hillel Wayne](https://www.hillelwayne.com/post/intermediate-vim/)

" Toggle Spelling Check with <space>sc
" <z=> 智能修改单词
map <LEADER>sc :set spell!<CR>
noremap <C-x> bea<C-x>s
inoremap <C-x> <Esc>ea<C-x>s

Ctrl+o: back to pre edit place
Ctrl+i: back to last edit place

gf: go to file
Ctrl+o: back to pre edit place

:%TOhtml: vim convert file to html

var name='lin'
var name='lin'
var name='lin'
> into vim block mode, 3j :'<,'>norm cs'"
> into vim vusual mode, V2j :'<,'>norm cs'"

gs: toggle code true/false

:w !wl-copy: copy file enable

1. 对齐符号
   > set mouse=a          
   > set encoding=utf-8   
   > set clipboard=unnamed
   :'<,'>Tabularize /=
   r: 调出执行 python 代码
   si | :term: split window and open new terminal
   

   录制宏，代码块格式化等号，可以用 map 更改为快捷键
   qaV}:'<,'>Tabularize /=

   SimpleFold 插件：<leader>o
   ?tagbar : shift+t
   vim-signature: 书签. ma: mark 'a' bookmark. <space> to next marked place
   semshi: 高亮当前光标所在的所有单词
   coc: 重构改变量名: <space>rn
   Far.vim: 搜索代码 <space>f
   FZF: Ctrl+p 跳转文件（文件搜索最强）
   NERDTree: tt 文件目录列表
   vim-table-mode: <space>tm 开启 markdown 自动排版
   vim-startify: 进入最近编辑的文件
   vim-multiple-cursor: 快速选中多行编辑
   wildfire.vim: 类似于 vscode 的 Ctrl+w 选中单词
   thesaurus_query: 近义词插件
   Startify: 进入编辑器显示东西用的
   emmet: 快速写 HTML 插件
   Bullets.vim: 文件中列表累加

   :help NERDTree: 查看插件文档



   ranger:
   S: go to path

   Shift+m: mkdir. create a directory

   Shift+v: touch a file

   cw: rename, 可以用 vim 操作，A 在文件末尾修改

   [: folder switch

   v: select all file

   dU: check file/folder size

   dD: 删除文件夹

   w: task manager

   dd: cancel opration

   c: compress

   X: extract here

   ct: convert to pdf

   ydv: youtube download

   zh: show dotfiles