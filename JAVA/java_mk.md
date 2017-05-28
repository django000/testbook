<header><h2 align="center">JAVA环境搭建</h2></header>

### 安装JDK和JRE

1. 根据操作系统及位数从[官网](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)下载对应的Java SE安装包
2. 双击安装，等待完成。

*P.S. 将jdk和jre安装在同一级目录下*

### 配置Java的环境变量

1. 添加环境变量JAVA_HOME
	```
	JAVA_HOME
	C:\Program Files\Java\jdk1.8.0_131
	```
2. 添加环境变量CLASSPATH
	```
	CLASSPATH
	.;%JAVA_HOME%\lib\dt.jar;%JAVA_HOME%\lib\tools.jar;
	```
3. 向环境变量Path追加`JAVA_HOME%\bin`
4. 在终端中执行`java`, `java -version`, `javac`检查是否安装成功

### Sublime Text 3 配置Java开发环境

1. Sublime Text 3->Preference->Browse Packages，在打开的打开的窗口中双击User文件夹，新建文件*JavaC.sublime-build*，用Sublime 打开并粘贴如下内容

	```
	{
		"cmd": ["javac", "-encoding", "UTF-8", "-d", ".", "$file"],
		"file_regex": "^(...*?):([0-9]*):?([0-9]*)",
		"selector": "source.java",
		"encoding": "GBK",
		//执行完上面的命令就结束

		// 下面的命令需要按Ctrl+Shift+b来运行
		"variants": [{
			"name": "Run",
			"shell": true,
			"cmd": ["start", "cmd", "/c", "java ${file_base_name} &echo. & pause"],
			// /c是执行完命令后关闭cmd窗口,
			// /k是执行完命令后不关闭cmd窗口。
			// echo. 相当于输入一个回车
			// pause命令使cmd窗口按任意键后才关闭
			"working_dir": "${file_path}",
			"encoding": "GBK"
		}]
	}
	```

2. 新建测试文件*Hello.java*，并输入如下内容

```java
import java.util.Scanner;


public class Hello {
	public static void main(String args[]) {
		Scanner s = new Scanner(System.in);
		System.out.println("输入字符串，exit终止====>");
		while (s.hasNextLine()) {
			String line = s.nextLine();
			if (line.equals("exit"))
				break;
			System.out.println("out==>"+line);
		}
	}
}
```

3. 快捷键"Ctrl+Shift+B"选择"JavaC"编译
4. 快捷键"Ctrl+Shift+B"选择"JavaC - Run"运行，并检查是否成功
