<header><h2 align="center">Linux中搭建GitBook环境</h2></header>

### 安装nvm进行node版本控制

1. 在终端中执行如下命令

	```bash
	cd ~
	git clone https://github.com/creationix/nvm.git .nvm
	```
2. 在"~/.profile"或"./bashrc"中添加如下命令

`source ~/.nvm/nvm.sh`

3. 在终端中`source ~/.profile` 或者`source ~/.bashrc`使更改生效，并使用`nvm --version`检查是否成功

### 安装node以及npm

1. `nvm install node`以及`node --version`检查是否成功
2. `curl -L https://www.npmjs.com/install.sh | sh`以及`npm --version`检查是否成功

### 安装gitbook

终端执行`npm install gitbook-cli -g`并使用`gitbook --version`检查是否成功

### 安装calibre

1. 在终端中执行`sudo -v && wget --no-check-certificate -nv -O- https://download.calibre-ebook.com/linux-installer.py | sudo python -c "import sys; main=lambda:sys.stderr.write('Download failed\n'); exec(sys.stdin.read()); main()"`
2. 如果不成功请安装如下[依赖](https://github.com/kovidgoyal/build-calibre/blob/master/scripts/sources.json)
3. 如果仍旧不成功参考如下教程
	- [在Ubuntu上设置并运行Calibre2014的终极解决方案](http://www.ictown.com/thread-98838-1-1.html "http://www.ictown.com")
	- [Download for linux](http://calibre-ebook.com/download_linux "http://calibre-ebook.com")

*关于gitbook的使用手册详见[GitBook 简明教程](http://www.chengweiyang.cn/gitbook/index.html)以及[GitBook Github主页](https://github.com/GitbookIO/gitbook)*
