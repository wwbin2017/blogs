---
title: c++编译
date: 2018-07-14 17:36:26
tags: c++编译
---

### g++
程序运行步骤
```shell
预处理 　　.i .ii文件　　　　     gcc -E helloworld.cpp -o helloworld.i
编译 　　　.s文件　　　　         gcc -S helloworld.cpp -o helloworld.s
汇编 　　　.o .obj文件　　　　 　　gcc -c helloworld.cpp -o helloworld.o
链接 　　　.lib .a文件
```
```shell
g++ helloworld.cc # a.out
g++ helloworld.cc -o helloworld #编译输出文件 helloworld
g++ helloworld.cc world.cc hello.h-o helloworld # 多文件编译
```
### 静态库与动态库

* 静态库 .a (linux) .lib (windows)
* 动态库 .so (linux) .dll (windows)
* gcc时，用-I和-L分别制定库名和库路径
#### 静态库
1 创建print.c和print.h,其中helloworld中用到了print这个函数，如果直接运行会报错说找不到print这个函数。
2 先print.c编译成二进制文件print.o
g++ -c print.c -o print.o
3 再用ar这个工具将add.o做成静态库
ar -r libprint.a print.o
4 这样就可以调用了，即在编译的时候加上库的名字，路径并申明为静态库-static等参数即可。
g++ helloworld.c -l libprint -L ./ -static -o helloworld
5 注意要其他地方也要用的话要把print.h也拷贝过去才能用

#### 动态库
1.首先创建libmyprint.so，即利用print.c这个函数生成动态库
g++ -shared -fPIC -o libmyprint.so print.c
-share指为共享的，-fPIC表示position independent code位置无关，这是动态库特性
2.指定动态库生成可执行文件，-L.表示当前文件夹，-l myprint表示去找libmyprint.so这个动态库文件。
g++ helloworld.c -L ./ -l myprint
3.直接使用会抱错，找不到动态库，要指定动态库的路径
./a.out会报错 
LD_LIBRARY_PATH=. ./a.out指定当前库的路径后在运行就可以了
4.如果要一直用，可以将.so文件的目录添加到/etc/ld.so.conf里面，然后再执行ldconfig就行了，具体如下面：
