---
title: Ubuntu 安装 chromedriver
date: 2021-06-10 13:25:54
tags: Ubuntu
---
### Download Chromedriver

This should download the latest version of Chromedriver, and extract it to the correct location, with the correct permissions.

```
version=$(curl -s "https://chromedriver.storage.googleapis.com/LATEST_RELEASE")
wget -qP /tmp/ "https://chromedriver.storage.googleapis.com/${version}/chromedriver_linux64.zip"
sudo unzip -o /tmp/chromedriver_linux64.zip -d /usr/bin
```

The permissions should be `755` by default, but if they aren't, you can run:

```
sudo chmod 755 /usr/bin/chromedriver
```

If you want a specific version, see the [index page](https://chromedriver.storage.googleapis.com/index.html), or the [website](https://chromedriver.chromium.org/).
You can also edit the above commands to use `LATEST_RELEASE_80`, if you wanted version 80, for example.

* * *

### Update to latest Chrome

If you don't already have the latest version of Google Chrome, you may need to update it with:

```
sudo apt-get --only-upgrade install google-chrome-stable
```

### 参考来源
[How To Install Chromedriver on Ubuntu 20.04 without snap | TheNerdLife Blog: ](https://www.thenerdlife.com/blog/how-to-install-chromedriver-on-ubuntu/)
[command line - How to update Chromedriver on Ubuntu? - Stack Overflow: ](https://stackoverflow.com/questions/48649230/how-to-update-chromedriver-on-ubuntu/50117805)
