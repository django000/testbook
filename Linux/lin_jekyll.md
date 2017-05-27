<header><h2 align="center">Linux中搭建Jekyll环境</h2></header>

### 安装RVM进行Ruby版本控制

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

### 安装Ruby 

1. 在终端中执行如下命令

	```
	rvm requirements
	rvm install ruby
	rvm install jruby
	```
2. 执行`ruby -v`和`gem -v`检查是否成功

3. 安装Bundler `gem install bundler`并使用`bundler -v`检查是否成功

*关于Ruby的使用手册详见[Ruby China](http://ruby-china.org/wiki/rvm-guide)*

### 安装Jekyll

在终端中执行如下命令`gem install jekyll`并使用`jekyll --version`检查是否成功

*关于Jekyll的使用手册详见[Basic Usage of Jekyll](https://jekyllrb.com/docs/usage/)*
