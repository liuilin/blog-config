---
title: DOM
date: 2021-03-20 08:41:29
tags: GitHub
---
# GitHub 搭建个人博客

[GitHub+Hexo 搭建个人网站详细教程](https://zhuanlan.zhihu.com/p/26625249)

> 配置代理
>
> git config --global http.proxy'socks5://127.0.0.1:10808'
>
> git config --global https.proxy'socks5://127.0.0.1:10808'

一个最简单的个人博客
1. 新建 GitHub 仓库
2. 开启 GitHub Pages 功能
3. 新建 index.html
4. 购买域名：namesilo.com【namesilo 优惠码】
5. 用 Hexo 生成复杂的页面

（<kbd>Ctrl</kbd> + <kbd>D</kbd> 退出）

删除本地秘钥：

rm ~/.ssh/id_rsa

rm ~/.ssh/known_hosts

### 配置 Git

git config --global user.name GitHub 英文名
git config --global user.email GitHub 邮箱
git config --global push.default matching
git config --global core.quotepath false
git config --global core.editor "vim"

### 配置 GitHub

1. 创建 GitHub 仓库 如：d:\blog

2. ```bash
   进入 blog 目录，逐行复制命令到 gitbash 运行
   echo "# blog" >> README.md
   git init
   git add README.md
   git commit -m "first commit"
   git remote add origin https://github.com/iMugen/blog.git
   git push -u origin master
   ```

3. 最后一句会失败：因为缺少 SSH Key

   Google：GitHub ssh key 复制命令 `ssh-keygen -t rsa -b 4096 -C"your_email@example.com"`接着输入`cat ~/.ssh/id_rsa.pub` 把打印的值添加到 GitHub 的 Personal settings/SSH and GPG keys 的新建中

   然后运行失败的 git push -u origin master

4. 新建 index.html，进入 Settings 的 GitHub Pages，将 Source 改为 master branch。保存后再次拉到此处把新出现的网址复制，点击顶部的项目，点击 Edit 输入网址保存。这样就可以点击网址访问首页了

### Git 命令总结

1. git init，初始化本地仓库.git
2. git status-sb，显示当前所有文件的状态
3. git add 文件路径，用来将变动加到暂存区
4. git commit-m“信息 "，用来正式提交变动，提交至.git 仓库
5. 如果有新的变动，我们只需要依次执行 git add xxx 和 git commit-m'xxx' 两个命令即可。别看本教程废话那么多，其实就这一句有用！先 add 再 commit，行了，你学会 git 了。
6. git log 查看变更历史
7. tree ... 查看某目录

### 其他

- git remote add origin gitegithub.com:xxxxxxx.git 将本地仓库与远程仓库关联
- git remote set-url origin gitegithub.com:xxxxx.git 上一步手抖了，可以用这个命令来挽回
- git branch 新建分支
- git merge 合并分支、
- git stash 通灵术
- git stash pop 反转通灵术
- git revert 后悔了
- git reset 另一种后悔了
- git diff 查看详细变化

### 资源

- 常用 Git 命令清单
- 读懂 diff - 阮一峰
- 搭建一个免费的，无限流量的 Blog----github Pages 和 Jeky 入门 Git 菜鸟教程
- 廖雪峰的 Git 教程
