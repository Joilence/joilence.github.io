---
title: makefile 学习指南
date: 2016-08-19 20:24:15
tags:
---

# makefile 简介

make 是一个程序，识别一系列如文件名为 Makefile，makefile 等的文件，根据其中的依赖关系，自动化编译项目。

# 为什么需要 makefile

对于一个有一定规模的项目，makefile 可以自动化编译，比一个一个手打 gcc/g++ 命令的效率高出许多，并且明确了依赖关系。另一个巨大优势是：使用 makefile 重新编译程序，make 会自动忽略没有修改的文件，只编译被修改过的文件，使得编译效率大大提高。

# 基本语法

``` makefile
Target: Dependence1 Dependence2 ...
        command ... 
```

`Target` 即是要编译的目标文件，`Dependence` 是制作这个目标文件需要的依赖文件，如果这些文件都存在，即条件都满足，就会执行下面 `command` 中命令。

如：

``` makefile
main: main.o
    g++ main.o -o main
main.o: main.cpp
    g++ main.cpp -o main.o
```

# 进阶

### 多目录

一般来说，自己程序的文件夹中会有 bin, build, src, include 这些目录，分别存放可执行程序，目标文件，源文件，头文件。makefile 一般放在根目录下。你只需在前面加上目录名字即可。如:

``` makefile
bin/main: build/main.o
    g++ build/main.o -o bin/main
build/main.o: src/main.cpp
    g++ -c src/main.cpp -o build/main.o
```

### 变量

在很多教程中，会给出声明变量的不同写法。

``` makefile
var := value
var = value
```

实际上，前者为简单扩展变量（recursively expanded variable），后者为递归扩展变量（simply expanded variable）。

简单变量会在 **被引用时立即赋值** ，比如你这样写：

``` makefile
a := a
abc := $(a) b c
a := d
abc2 := $(a) b c

test:
	echo $(abc)
	echo $(abc2)
```

然后 `make test` 会发现输出如下：

``` shell
echo a b c
a b c
echo d b c
d b c
```

而递归变量 **只有在被引用的变量在执行时被赋值** ，比如你这样写：

``` makefile
a = a
abc = $(a) b c
a = d
abc2 = $(a) b c
test:
	echo $(abc)
	echo $(abc2)
```

会发现输出如下，即便 `abc` 在 `a = d` 之后就被赋值，都只有在 `test` 执行 `abc` 的时候，a 才会被替换为它最后的值 `d`。

``` shell
echo d b c
d b c
echo d b c
d b c
```

### 自动化变量

makefile 可以使用一些自动化减少劳动量，同样拿之前的例子：

``` makefile
bin/main: build/main.o
    g++ build/main.o -o bin/main
build/main.o: src/main.cpp
    g++ -c src/main.cpp -o build/main.o
```

可以简化成

``` makefile
bin/main: build/main.o
    g++ $^ -o $@
build/main.o: src/main.cpp
    g++ -c $< -o $@
```

`$^` 可以直接替换成当前目标文件的所有依赖文件；`$@` 可以直接替换成当前目标文件的路径名称，而不需要反复输入；`$<` 会直接替换成当前目标文件的首个依赖文件。

# 最后

以上只提到了自己比较常用的东西，并未介绍完所有关于 makefile 的知识，比如另外更多的自动化变量等。这些可以自行 google。

推荐一份更加详细深入的教程（只是没有自动化变量）：

[跟我一起写Makefile](http://wiki.ubuntu.org.cn/跟我一起写Makefile)

