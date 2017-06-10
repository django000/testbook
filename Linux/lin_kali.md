<header><h2 align="center">Linux中Kali系统的安装与配置</h2></header>

### 安装Kali操作系统

Kali系统支持虚拟机安装和硬盘安装，两者的安装过程是不同的。一般来讲，虚拟机的安装方式更为简单安全，因此这里指的是在虚拟机管理软件上安装Kali系统。

1. 从官网[下载](https://www.offensive-security.com/kali-linux-vmware-virtualbox-image-download/)对应的虚拟系统镜像。
	注意：官网提供了适用于VMware、VirtualBox、Hyper-V各个虚拟机软件的镜像文件，可以自行选择
2. 将镜像文件解压至某目录，并双击其中的启动文件(VMware中为".vmx"文件)，选择在VMware Station Pro中打开，就可以在虚拟机列表里看到相应Kali系统了。
3. 更改相应参数设置(主要是内存、处理器、硬盘设置)，就可以启动系统了。
	注意：系统默认用户为`root`，密码为`toor`
4. 终端打开"/etc/apt/sources.list"文件添加国内的APT源，在文件头添加如下内容
	```bash
	# zhongkeda apt
	deb http://mirrors.ustc.edu.cn/kali kali-rolling main non-free contrib
	deb-src http://mirrors.ustc.edu.cn/kali kali-rolling main non-free contrib
	deb http://mirrors.ustc.edu.cn/kali-security kali-current/updates main contrib non-free
	deb-src http://mirrors.ustc.edu.cn/kali-security kali-current/updates main contrib non-free

	# aliyun apt
	deb http://mirrors.aliyun.com/kali kali-rolling main non-free contrib
	deb-src http://mirrors.aliyun.com/kali kali-rolling main non-free contrib
	deb http://mirrors.aliyun.com/kali-security kali-rolling/updates main contrib non-free
	deb-src http://mirrors.aliyun.com/kali-security kali-rolling/updates main contrib non-free
	```
5. 在终端中执行如下命令来完成更新
	```bash
	apt-get update & apt-get upgrade --fix-missing
	apt-get dist-upgrade 
	apt-get clean
	```
6. 在终端中执行`apt-get install open-vm-tools-desktop fuse`来安装vmware tools与物理机交互

### 安装Wing IDE及破解

Wing IDE是一款在调试功能上十分强大的Python IDE，一直深受Python开发者尤其是Hacker喜爱。目前Wing IDE虽然有三个版本类型，但这里安装Wing IDE Pro版，并给出破解步骤。

1. 从官网[下载](https://wingware.com/downloads/wing-pro)安装包
	注意：笔者无法在64位的Kali系统上安装64位的Wing IDE，转而尝试了"x86 64-bit"的版本，才得以安装成功
2. 在下载目录下执行`tar jxf package`解压压缩包，并执行`python wing-install.py`安装软件，在安装时设置相应目录，可以顺利安装完毕
3. 在终端中执行`wing6.0`检查是否安装成功
4. 启动Wing IDE后选择"输入LicenseID"来破解。
	注意：这里的破解文件为"wingide6.py"，内容如下：
	```python
	#!/usr/bin/env python
	import hashlib
	LicenseID='CN123-12345-12345-67899'
	RequestCode='RL61P-XWGDH-8973V-6WTY5'

	B16 = '0123456789ABCDEF'
	B30 = '123456789ABCDEFGHJKLMNPQRTVWXY'
	def B(n,f,t):
		xx = 0
		for d in str(n):
			xx = xx * len(f) + f.index(d)
		res = ''
		while xx > 0:
			res=t[int(xx%len(t))]+res
			xx//=len(t)
		return res
	def S(D):
		r = B(''.join([c for i,c in enumerate(D) if i//2*2==i]),B16,B30)
		while len(r) < 17:
			r = '1' + r
		return r
	def A(c):
		return c[:5]+'-'+c[5:10]+'-'+c[10:15]+'-'+c[15:]
	h = hashlib.sha1()
	h.update(RequestCode.encode('utf-8')+LicenseID.encode('utf-8'))
	lichash=A(RequestCode[:3]+S(h.hexdigest().upper()) )
	data=[23,161,47,9]
	tmp=0
	realcode=''
	for i in data:
		for j in lichash:
			tmp=(tmp*i+ord(j))&0xFFFFF
		realcode+=format(tmp,'=05X')
		tmp=0
	D=B(realcode,B16,B30)
	while len(D) < 17:
		D = '1' + D
	print "The Activation Code is: "+A('AXX'+D)
	```
	任意更改py文件中的License ID，并输入到Wing IDE中，然后执行`python wingide6.py`来获得RequestCode，并填入Wing IDE的下一个页面，完成激活。