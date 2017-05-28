<header><h2 align="center">Linux利用亚马逊AWS搭建Shadowsocks服务器</h2></header>

### 注册亚马逊AWS账号

访问[AWS官网](https://aws.amazon.com/cn/)，注册AWS服务。如果之前有亚马逊账号，可以直接用亚马逊账号登录，填写相关资料。过程中有两点需要注意
1. 注册服务需要绑定信用卡缴付预授权的费用，因此需要提前准备双币信用卡
2. 之后的AWS服务一年内享受免费优惠，一年之后需要继续付费试用，因此如果不想用到期记得自动终止服务

### 创建EC2实例

1. 账号登录进入AWS控制台，右上角选择"亚太地区(东京)"，在页面中启动实例
2. 选择镜像系统、硬件配置，设置服务器标签和名称
3. 命名生成新的密钥文件，并下载".pem"文件到本地，最好将其移入"~/.ssh/"目录

### SSH连接实例

记录EC2实例的公网IP，在终端中执行如下命令连接实例，如果遇到选择输入"yes"
	```bash
	ssh ec2-user@ec2-ip -i ~/ssh/amazonjp.pem
	```

### 安装并配置Shadowsocks

1. 在终端中安装必要依赖库以及Shadowsocks

	```bash
	sudo yum(apt-get) install -y python-setuptools
	sudo easy_install pip
	sudo pip install shadowsocks
	```
2. 在终端中执行`which ssserver`获取将ssserver执行文件目录，并将其添加到环境变量中
3. 生成Shadowsocks的配置文件，一个常见的实例如下
	```json
	{
		"server":"0.0.0.0",
		"server_port":4000,
		"local_address":"127.0.0.1",
		"local_port":1080,
		"password":"amazonjp",
		"timeout":300,
		"method":"aes-256-cfb",
		"fast_open":true,
		"workers": 1
	}
	```
4. 设置alias别名，一个常见的实例如下
	```bash
	alias sst="ssserver -c /home/ec2-user/shadow/ssconfig.json -d start"
	alias ssp="ssserver -c /home/ec2-user/shadow/ssconfig.json -d start"
	alias ssr="ssserver -c /home/ec2-user/shadow/ssconfig.json -d start"
	```
5. 设置ssserver的开机自启
	以sudo权限编辑文件"/etc/rc.local"，在其末尾追加`ssserver -c /home/ec2-user/shadow/ssconfig.json -d start`

6. 从[shadowsocks](https://github.com/shadowsocks/shadowsocks/tree/master)的github主页下载相应的客户端，并根据EC2实例中的配置文件填写客户端的账号设置
7. 享受畅通

*在一年优惠之后可以终止该实例，也可以继续使用*
