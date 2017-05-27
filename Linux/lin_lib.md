<header><h2 align="center">Linux中调用动态链接库libtest.so</h2></header>

### 生成.so文件

在终端中执行`gcc -o libtest.so libtest.c -shared -fPIC`来生成.so文件

### 调用.so文件

.so文件有两种调用方式

#### 第一种方式

1. 将当前库文件目录添加到**/etc/ld.so.conf.d/libtest.conf** 或者使用命令 **sudo ldconfig \`pwd\`** 设置本次有效
2. 在"test.c"文件中直接调用库文件中的函数，并使用如下命令生成可执行文件

#### 第二种方式

1. 在"test.c"文件中调用该库，并使用**dlxxx**函数进行操作，示例如下

	```C
	#include <stdio.h>
	#include <dlfcn.h>
	#include <stdlib.h>

	void (*fn)();

	int main(int argc, char** argv){
	void *handle = dlopen("./libtest.so", RTLD_LAZY);
	const char *err = dlerror();
	if (err != NULL){
	perror("The program could not open the .so file!");
	}
	fn = dlsym(handle, "testhola"); /*the function of the .so file*/
	fn(argv[1]);
	dlclose(handle);
	return 0;
	}
	```
2. 在终端中执行`gcc -o test test.c -rdynamic -ldl`生成可执行文件

