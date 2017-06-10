<header><h2 align="center">Linux终端技巧</h2></header>

### alias别名设置

alias中文译为别名，用于给某些命令设定简单的别名，适用于任何Linux系统环境。aliaa的合理利用可以大大提升日常命令的执行效率，因此，笔者在此总结目前常用的一些alias设置。

无论是user用户还是root用户，都可以在其主目录下的".bashrc"文件中编辑alias设置。

1. 在终端中执行`vim ~/.bashrc`打开".bashrc"文件
2. 在文件末尾添加如下命令
	
	```bash
	alias ex="exit"
	alias vbs="vim ~/.bashrc"
	alias sbs="source ~/.bashrc"
	alias ch="cd /home"
	alias ghp="git add . && git commit -m $1"
	alias al1="ssh root@120.25.79.195"
	alias te1="ssh root@118.89.227.144 -i ~/.ssh/ten01"
	alias az1="ssh ec2-user@54.250.174.123 -i ~/.ssh/amazonjp01.pem"
	```
3. 在终端中执行`source ~/.bashrc`使更改生效
4. 如果按照上述描述，之后可以执行`vbs`和`sbs`来进行更改

### 修改环境变量

修改环境变量一般有三种方式，第一种通过在终端中执行`$PATH="$PATH":/NEW_PATH`实现，只对本次的终端会话有效。下面分别介绍其余两种
- 修改用户主目录下的".profile"或".bash_profile"文件，这种方式只修改了用户的环境变量，对于root或user均适用
- 修改/etc/profile文件，这种方式修改了系统的环境变量，对于系统中任何用户都有效

至于修改方式，在文件末尾追加`$PATH="$PATH":NEW_PATH`即可，其中"NEW_PATH"最好为绝对路径。这条命令相当于对于原来的"$PATH"追加新的路径。
