<header><h2 align="center">Linux 安装后的配置总结，不断更新中......</h2></header>

[TOC]

### 更新软件源

	```bash
	sudo apt-get update
	sudo apt-get upgrade
	sduo apt-get autoremove
	```

### 搭建gitbook环境

#### 安装nvm进行node版本控制

1. 在终端中执行如下命令

	```bash
	cd ~
	git clone https://github.com/creationix/nvm.git .nvm
	```
2. 在"~/.profile"或"./bashrc"中添加如下命令

`source ~/.nvm/nvm.sh`

3. 在终端中`source ~/.profile` 或者`source ~/.bashrc`使更改生效，并使用`nvm --version`检查是否成功

#### 安装node以及npm

1. `nvm install node`以及`node --version`检查是否成功
2. `curl -L https://www.npmjs.com/install.sh | sh`以及`npm --version`检查是否成功

#### 安装gitbook

终端执行`npm install gitbook-cli -g`并使用`gitbook --version`检查是否成功

#### 安装calibre

1. 在终端中执行`sudo -v && wget --no-check-certificate -nv -O- https://download.calibre-ebook.com/linux-installer.py | sudo python -c "import sys; main=lambda:sys.stderr.write('Download failed\n'); exec(sys.stdin.read()); main()"`
2. 如果不成功请安装如下[依赖](https://github.com/kovidgoyal/build-calibre/blob/master/scripts/sources.json)
3. 如果仍旧不成功参考如下教程
	- [在Ubuntu上设置并运行Calibre2014的终极解决方案](http://www.ictown.com/thread-98838-1-1.html "http://www.ictown.com")
	- [Download for linux](http://calibre-ebook.com/download_linux "http://calibre-ebook.com")

#### 关于gitbook的使用手册详见[GitBook 简明教程](http://www.chengweiyang.cn/gitbook/index.html)


### 添加中文支持—搜狗输入法

1. 菜单->首选项->语言，在语言界面安装或更改相应的语言支持，在输入法页面安装简体中文输入法(可能需要拖动中文至最顶行)，并在输入法下拉框中选择Fcitx
2. 在终端中执行`sudo im-config`，连续选择确定，在输入法配置界面选择Fcitx
3. 从搜狗输入法[官网](http://pinyin.sogou.com/linux/)下载64位的.deb安装包，双击安装(可能需要重启生效)
4. 菜单->首选项->Fcitx配置，在输入法中对于目前已有的进行排序，将搜狗输入法置于最前位置
5. 如果仍旧不成功参考如下教程
	- [Ubuntu14.04.2中文语言支持与输入法设置](http://blog.csdn.net/q1302182594/article/details/47065309)
	- [Ubuntu14.04.2安装搜狗输入法](http://blog.csdn.net/q1302182594/article/details/47068641)


### 搭建Jekyll环境

#### 安装RVM进行Ruby版本控制
1. 在终端中执行如下命令

```bash
gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3
curl -sSL https://get.rvm.io | bash -s stable
# if it failed with the cmd above, try the following one:
curl -L https://raw.githubusercontent.com/wayneeseguin/rvm/master/binscripts/rvm-installer | bash -s stable
```
2. 按照提示进行"source"操作
3. 修改RVM下载Ruby的镜像源
`echo "ruby_url=https://cache.ruby-china.org/pub/ruby" > ~/.rvm/user/db`

#### 安装Ruby 

1. 在终端中执行如下命令

```
rvm requirements
rvm install ruby
rvm install jruby
```
2. 执行`ruby -v`和`gem -v`检查是否成功

3. 安装Bundler `gem install bundler`并使用`bundler -v`检查是否成功
4. 安装rails `gem install rails`并使用`rails -v`检查是否成功

*关于Ruby的使用手册详见[Ruby China](http://ruby-china.org/wiki/rvm-guide)*

#### 安装Jekyll

在终端中执行如下命令`gem install jekyll`并使用`jekyll --version`检查是否成功

*关于Jekyll的使用手册详见[Basic Usage of Jekyll](https://jekyllrb.com/docs/usage/)*


### Python网站搭建

#### 安装Nginx

1. 在终端中执行`sudo apt-get install nginx`，
2. 获取Nginx的配置目录，生成网站的server配置文件，一个常见的示例如下

	```bash
	server {
		listen 90;
		#server_name 127.0.0.1;
		charset utf-8;

		#index index.html
		error_page 404 500 503 /index.htm;

		location / {
			root /home/user/project;
			#access_log "/home/user/project/logs/project_access.log" main;
			uwsgi_pass 127.0.0.1:9002;
			uwsgi_param UWSGI_CHDIR /home/user/project;
			uwsgi_param UWSGI_SCRIPT main:app;
			# 也可以用以下配置等价代替
			# uwsgi_param UWSGI_MODULE main;
			# uwsgi_param UWSGI_CALLABLE app;

			# uwsgi_param SCRIPT_NAME  /app;
			include  uwsgi_params;
			}
		}
	```

3. 在终端中执行`service nginx start|stop|restart|upgrade`进行操作

#### 安装uwsgi

1. 在终端中执行`sudo pip install uwsgi flasky`安装uwsgi和flasky
2. 在工程目录中生成uwsgi.ini，一个常见的示例如下

	```
	[uwsgi]
	socket = 127.0.0.1:9002 # 与nginx中uwsgi_pass相同
	master = true
	vhost = true
	worker = 2
	reload-mercy = 10
	emperor-tyrant = true
	daemonize = /Users/xxx/Desktop/logs/uwsgi.log
	```
3. 在终端中执行`uwsgi --ini uwsgi.ini`来启动uwsgi服务

*在修改工程文件后，需要手动重启uwsgi服务*


