# Ubuntu 开发环境配置

## Dev on Windows with WSL

[Node.js | Dev on Windows with WSL](https://dowww.spencerwoo.com/3-vscode/3-6-nodejs.html#安装-node-js)

## 配置 Shell 基础环境

1. [Shell 环境，更换软件镜像源| Dev on Windows with WSL](https://dowww.spencerwoo.com/2-cli/2-2-shell.html#更换软件源镜像)

2. [记录一次 WSL2 的网络代理配置 | jiayaoO3O's Blog](https://jiayaoo3o.github.io/2020/06/23/记录一次WSL2的网络代理配置/)

   > v2ray 要开启允许局域网连接

3. 安装 zsh

   ```bash
   sudo apt install zsh -y
   ```

   > echo $0 # 查看当前 shell 类型

4. install oh-my-zsh

   ```bash
   sh -c "$(curl -fsSL -x socks5://$(ip route | grep default | awk '{print $3}'):10808 https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
   ```

5. TODO 把 GitHub 上的 .zshrc 文件下载下来覆盖

   **然后一定要新开窗口，不然配置不生效**

## 安装 mackup 备份还原 dotfiles 配置

[lra/mackup: Keep your application settings in sync (OS X/Linux)](https://github.com/lra/mackup)

创建用户：sudo adduser xxx

[curl 设置代理 - 知乎](https://zhuanlan.zhihu.com/p/58690128)

1. Ubuntu-22.04 本身就自带 Python3(3.10.4) 最新版，无需安装

2. [Installation - pip documentation v22.0.4 安装最新版 pip](https://pip.pypa.io/en/stable/installation/)

   采用 `get-pip.py` 脚本的方式

   ```bash
   # run the following command to download the get-pip.py file，下面 $(ip route | grep default | awk '{print $3}') 获取 WSL 动态 IP，用于 v2ray 代理
   curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
   # To install PIP type in the following
   python3 get-pip.py
   # WARNING: The script wheel is installed in '~/.local/bin' which is not on PATH.
   # 此时 pip 没有环境变量，所以命令未生效。使用 add alias 来调用
   alias pip='~/.local/bin/pip3'
   pip -V
   ```

   如果是 zsh 的话（想要一直生效的话），还需要把 alias 配置到 .zshrc 里面

   > note: 不要用 Ubuntu 自带的 apt 方式安装，因为 Python3 是最新版而 apt 安装出来的较低版本，会导致与 Python 最新版那边不兼容，从而 pip 安装软件时会报错
   >
   > [python - ImportError: cannot import name 'html5lib' from 'pip._vendor' (/usr/lib/python3/dist-packages/pip/_vendor/__init__.py) - Stack Overflow](https://stackoverflow.com/questions/70431655/importerror-cannot-import-name-html5lib-from-pip-vendor-usr-lib-python3)
   >
   > [Pip is not working for Python 3.10 on Ubuntu - Stack Overflow](https://stackoverflow.com/questions/69503329/pip-is-not-working-for-python-3-10-on-ubuntu/69527217#69527217)
   >
   > This is likely caused by a too old system `pip` version.
   >
   > Install the latest with:
   > `curl -sS https://bootstrap.pypa.io/get-pip.py | python3.10`
   >
   > [How To Install Python 3 and Set Up a Programming Environment on Ubuntu 22.04 | DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-install-python-3-and-set-up-a-programming-environment-on-ubuntu-22-04)

3. install mackup with pip

   ```bash
   # Install Mackup with PIP
   pip install --upgrade mackup
   alias mackup='~/.local/bin/mackup'
   
   # Launch it and back up your files
   mackup backup
   ```

4. 下载 mackup 配置文件并更新

   ```bash
   # 代理下载文件到当前目录
   curl -x socks5://WSL 代理 IP:10808 https://github.com/liuilin/dotfiles/raw/master/.mackup.cfg -OL
   # 修改配置文件
   sudo vim .mackup.cfg
   ```

   > [git - Download single files from GitHub - Stack Overflow](https://stackoverflow.com/questions/4604663/download-single-files-from-github)
   >
   > You can use `curl` this way:
   >
   > ```bash
   > curl -OL https://raw.githubusercontent.com/<username>/<repo-name>/<branch-name>/path/to/file
   > ```
   >
   > `O` means that curl downloads the content
   > `L` means that curl follows the redirection

5. 恢复所有备份的配置

   https://drive.google.com/drive/folders/1LrGZMV4aQYLIGTwoHodb3eJ1GE3JbqJV

   修改当前用户的全局设置，使 mackup 环境变量生效

   **不要恢复 .bash_logout 文件！！！否则会报错**

   ```bash
   sudo vim ~/.bashrc
   export PATH=/home/daniel/.local/bin/mackup:$PATH
   source .bashrc
   sudo vim .mackup.cfg
   # 修改存储路径 path = /mnt/c/Users/liuqiang/
   # TODO 考虑安装完 zsh 再 mackup restore 恢复配置，不然会被覆盖
   mackup restore
   ```

6. Google Drive 自动同步文件夹 /mnt/c/Users/Daniel/dotfiles

7. todo 运行代理加速

   ```bash
   # 运行 .zshrc 里面配置的命令来自动配置全局代理
   proxy
   # 查看 http.https://github.com.proxy 配置是否生效，q：退出交互界面
   git config -l
   ```

   配置 mackup 环境变量

   ```bash
   sudo vim ~/.zshrc
   export PATH=/home/daniel/.local/bin/mackup:$PATH
   ```

> [Yadm：我是如何同步并管理我的 Dotfiles 的？ - Spencer's Blog](https://spencerwoo.com/blog/how-i-manage-my-dotfiles)

### 安装 oh-my-zsh 插件

1. 插件 autojump：[wting/autojump: A cd command that learns - easily navigate directories from the command line](https://github.com/wting/autojump#)

   ```bash
   sudo apt install autojump
   ```

2. 插件 zsh-autosuggestions：[zsh-autosuggestions/INSTALL.md at master · zsh-users/zsh-autosuggestions](https://github.com/zsh-users/zsh-autosuggestions/blob/master/INSTALL.md#oh-my-zsh)

   ```bash
   git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
   ```

3. 插件 zsh-syntax-highlighting：[zsh-syntax-highlighting/INSTALL.md at master · zsh-users/zsh-syntax-highlighting](https://github.com/zsh-users/zsh-syntax-highlighting/blob/master/INSTALL.md)

   ```bash
   git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
   ```

4. 安装主体模板：

   ```bash
   git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k
   ```

   - [Windows 安装 Nerd Font（Sauce Code Pro Nerd Font）字体](https://www.nerdfonts.com/font-downloads)：解压到 C:\Windows\Fonts 路径下
   - 主体配置：One half dark
   - 背景不透明度：66

   > 字体显示问题（NERD FONT）：[romkatv/nerd-fonts: Iconic font aggregator, collection, & patcher. 3,600+ icons, 50+ patched fonts: Hack, Source Code Pro, more. Glyph collections: Font Awesome, Material Design Icons, Octicons, & more](https://github.com/romkatv/nerd-fonts#option-5-clone-the-repo)
   >
   > 
   >
   > 静默覆盖文件：yes | cp -rf xxx xxx

5. 重新打开一个会话窗口 Restart zsh (such as by opening a new instance of your terminal emulator).

### 配置 Node 环境

### 配置 Java 环境

1. 安装 openjdk

   ```bash
   sudo apt install openjdk-11-jdk
   ```

   > 安装 jdk 报错的话
   >
   > The following packages have unmet dependencies:
   >  debianutils : Breaks: x11-common (< 1:7.7+23~) but 1:7.7+19ubuntu14 is to be installed
   >  libglx-mesa0 : Depends: libx11-xcb1 (>= 2:1.6.9) but it is not installable
   > E: Error, pkgProblemResolver::Resolve generated breaks, this may be caused by held packages.
   >
   > 解决：
   >
   > ```bash
   > sudo apt install libx11-xcb1
   > sudo apt install libglx-mesa0
   > ```
   >
   > 还是提示 
   >
   > The following packages have unmet dependencies:
   >  debianutils : Breaks: x11-common (< 1:7.7+23~) but 1:7.7+19ubuntu14 is to be installed
   > E: Error, pkgProblemResolver::Resolve generated breaks, this may be caused by held packages.
   >
   > 使用一个强大的包管理工具
   >
   > ```bash
   > $ sudo apt install aptitude
   > # debianutils 版本太新了，根据提示选 n 不保留当前版本，把 debianutils 降级
   > $ sudo aptitude install x11-common
   > 
   > The following NEW packages will be installed:
   >   x11-common
   > 0 packages upgraded, 1 newly installed, 0 to remove and 0 not upgraded.
   > Need to get 22.3 kB of archives. After unpacking 321 kB will be used.
   > The following packages have unmet dependencies:
   >  debianutils : Breaks: x11-common (< 1:7.7+23~) but 1:7.7+19ubuntu14 is to be installed
   > The following actions will resolve these dependencies:
   > 
   >      Keep the following packages at their current version:
   > 1)     x11-common [Not Installed]
   > 
   > Accept this solution? [Y/n/q/?] n
   > The following actions will resolve these dependencies:
   > 
   >      Downgrade the following packages:
   > 1)     debianutils [5.5-1ubuntu2 (now) -> 4.9.1 (focal)]
   > 
   > Accept this solution? [Y/n/q/?] Y
   > The following packages will be DOWNGRADED:
   >   debianutils
   > The following NEW packages will be installed:
   >   x11-common
   > 0 packages upgraded, 1 newly installed, 1 downgraded, 0 to remove and 0 not upgraded.
   > Need to get 108 kB of archives. After unpacking 307 kB will be used.
   > Do you want to continue? [Y/n/?] Y
   > Get: 1 https://mirrors.tuna.tsinghua.edu.cn/ubuntu focal/main amd64 debianutils amd64 4.9.1 [85.8 kB]
   > Get: 2 https://mirrors.tuna.tsinghua.edu.cn/ubuntu focal/main amd64 x11-common all 1:7.7+19ubuntu14 [22.3 kB]
   > Fetched 108 kB in 1s (94.5 kB/s)
   > dpkg: warning: downgrading debianutils from 5.5-1ubuntu2 to 4.9.1
   > (Reading database ... 36541 files and directories currently installed.)
   > Preparing to unpack .../debianutils_4.9.1_amd64.deb ...
   > Unpacking debianutils (4.9.1) over (5.5-1ubuntu2) ...
   > Setting up debianutils (4.9.1) ...
   > Selecting previously unselected package x11-common.
   > (Reading database ... 36537 files and directories currently installed.)
   > Preparing to unpack .../x11-common_1%3a7.7+19ubuntu14_all.deb ...
   > dpkg-query: no packages found matching nux-tools
   > Unpacking x11-common (1:7.7+19ubuntu14) ...
   > Setting up x11-common (1:7.7+19ubuntu14) ...
   > update-rc.d: warning: start and stop actions are no longer supported; falling back to defaults
   > invoke-rc.d: could not determine current runlevel
   > Processing triggers for man-db (2.10.2-1) ...
   > Scanning processes...
   > Scanning processor microcode...
   > Scanning linux images...
   > 
   > Failed to retrieve available kernel versions.
   > 
   > Failed to check for processor microcode upgrades.
   > 
   > No services need to be restarted.
   > 
   > No containers need to be restarted.
   > 
   > No user sessions are running outdated binaries.
   > 
   > No VM guests are running outdated hypervisor (qemu) binaries on this host.
   > ```

2. 安装 Maven

   ```bash
   sudo apt install maven -Y
   mkdir ~/.m2 && cp -r /usr/share/maven/conf/settings.xml ~/.m2/settings.xml
   ```

   修改 settings 的中央仓库：[阿里云云效仓库服务](https://developer.aliyun.com/mvn/guide)

## Question

1. 查看当前 Shell 环境

   ```bash
   echo $0
   ```

2. `history | grep "git clone"`这个命令就能找到近期 clone 了哪些库，省却了写一堆代码的功夫。

3. 给 root 用户设置密码

   ```bash
   sudo passwd root
   su root # 切换到 root 用户
   usermod -aG sudo xxx # 给 xxx 用户赋予 root 权限
   ```

4. 获取 WSL 动态 IP

   ```bash
   # 获取 WSL IP，用于下面临时 v2ray 代理
   ip route | grep default | awk '{print $3}'
   ```

   示例：curl -x socks5://$(ip route | grep default | awk '{print $3}'):10808 https://bootstrap.pypa.io/get-pip.py -o get-pip.py