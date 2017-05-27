<header><h2 align="center">Windows搭建GitBook环境</h2></header>

### 安装nvmw进行node版本控制

1. 在终端中执行如下命令

	```bash
	cd ~
	git clone https://github.com/hakobera/nvmw.git .nvmw
	set "PATH=~/.nvmw;%PATH%"
	```
2. 使用`nvmw --version`检查是否成功

### 安装node以及npm

1. `nvm install node`以及`node --version`检查是否成功
2. `curl -L https://www.npmjs.com/install.sh | sh`以及`npm --version`检查是否成功

### 安装GitBook

终端执行`npm install gitbook-cli -g`并使用`gitbook --version`检查是否成功

### 安装calibre

从[官网](https://calibre-ebook.com/dist/win32)下载Calibre安装包，双击安装并检查是否添加到环境变量

*关于GitBook的使用手册详见[GitBook 简明教程](http://www.chengweiyang.cn/gitbook/index.html)*

