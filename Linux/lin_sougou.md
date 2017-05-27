<header><h2 align="center">Linux中配置搜狗输入法</h2></header>

1. 菜单->首选项->语言，在语言界面安装或更改相应的语言支持，在输入法页面安装简体中文输入法(可能需要拖动中文至最顶行)，并在输入法下拉框中选择Fcitx
2. 在终端中执行`sudo im-config`，连续选择确定，在输入法配置界面选择Fcitx
3. 从搜狗输入法[官网](http://pinyin.sogou.com/linux/)下载64位的.deb安装包，双击安装(可能需要重启生效)
4. 菜单->首选项->Fcitx配置，在输入法中对于目前已有的进行排序，将搜狗输入法置于最前位置
5. 如果仍旧不成功参考如下教程
	- [Ubuntu14.04.2中文语言支持与输入法设置](http://blog.csdn.net/q1302182594/article/details/47065309)
	- [Ubuntu14.04.2安装搜狗输入法](http://blog.csdn.net/q1302182594/article/details/47068641)

