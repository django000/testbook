<header><h2 align="center">Python利用Flask搭建网站</h2></header>

### 安装Nginx

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

### 安装uwsgi

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
