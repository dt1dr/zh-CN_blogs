---
title: C++学习：分别编译与makefile
date: 2023-11-01 00:10:12
tags: C++
categories: 编程
cover: ./img/CppCover.png
---


## 前言


一句话解释什么是makefile: 自动编译程序的脚本

## make 之前

从很多坨源代码文件到一个可运行的软件项目的过程叫做**构建（Build）**。
对于C++程序，一个重要的过程便是编译（compile）。

### 单个源文件的编译
编译如下文件：

```cpp
// helloworld.cpp
# include<iostream>

void print()
{
    std::cout << "hello world" << std::endl;
}

int main()
{
    std::cout << "Print" << std::endl;
    print();
}
```

编译方式是在`bash`等终端里输入：
```bash
g++ -c helloworld.cpp
g++ -o main helloworld.o
```
这样会产生中间文件`helloworld.o`，因为这里只有单个`.o`文件没有要链接的其他文件，可以委托g++一步到位：
```bash
g++ -o main helloworld.cpp
```
然后编译器会生成可执行文件 `main`


### 分别编译 Separate compilation

但是对于体积比较大的程序，规范是将函数，类等组件的声明与实现分开，不同功能分别放在不同的头文件与源文件中：

```cpp
// file: main.cpp
# include <iostream>
# include "Apple.h"
# include "print.h"


int main()
{
    std::cout << "Print" << std::endl;
    print();
}

// file: Apple.h
#ifndef APPLE_H  
#define APPLE_H

class Apple{
public:
    void print_apple();
private:
    int number;
};

#endif  // APPLE_H

// file: Apple.cpp

# include <iostream>
# include "Apple.h"

void Apple::print_apple(){
    std::cout << "I am an apple!" << std::endl;
}


// file: print.h
#ifndef PRINT_H  
#define PRINT_H

void print();
#endif  // PRINT_H

// file: print.cpp
# include <iostream>
# include "Apple.h"
# include "print.h"

void print(){
    Apple a;
    std::cout << " Somebody says : " << std::endl;
    a.print_apple();
}
```

上述代码有5个文件，而且相互之间还有依赖关系，规范的编译命令如下：

```bash
g++ -c Apple.cpp
g++ -c print.cpp
g++ -c main.cpp
g++ -o main main.o Apple.o print.o
```
太复杂了！如果你正在开发 Linux 操作系统内核, 使命召唤, 虚幻5 这样的大型C/C++软件，你能敲编译命令敲到天亮！
不同的文件之间相互依赖，牵一发而动全身，如果你修改了其中一个文件，要怎么确保重新编译时**只重新编译那些受修改影响的部件**？
我们需要一个自动化脚本来减少脱发量。


## Make 和 Makefile

软件`make`是GNU提供的一款自动编译源代码的命令行工具。当你在命令行里使用`make`命令时，`make`会搜索当前目录下最近的makefile文件，并按照上面的指引执行一条条命令，免去手动输入一行行代码了

#### 安装
`make` 属于 `GNU` 生态的 **工具链**（Toolchain）。所以几乎所有Linux发行版都会自带，如果没有，在安装GCC, MinGW, 甚至 MacOS上的 CommandLineTools 时都会安装make。
在命令行中输入 `make` 命令还是没反应？自行处理环境变量！
时至今日，`make`基本上可以算作PC的基础设施了

#### 写一个简短的makefile

在源代码所在的目录下新建一个文件，命名为`GNUmakefile`，`makefile` 或 `Makefile` 一般是`makefile`。不需要扩展名，也就是说没有必要建一个`makefile.txt`

对于我们刚刚写的五个文件，现在我们在`makefile`里这样写：

```makefile
all : main 

main :main.o Apple.o print.o
    g++ -o main main.o Apple.o print.o    
main.o : main.cpp Apple.o print.o
    g++ -c main.cpp
Apple.o : Apple.cpp
    g++ -c Apple.cpp
print.o : print.cpp Apple.o
    g++ -c print.cpp
clean :
    rm main main.o Apple.o print.o
```
这样，一个简单的makefile就写好了，在命令行输入：
```bash
make all
```
搞定！

## 更多技巧

详情请见 [跟我一起写Makefile](https://seisman.github.io/how-to-write-makefile/)
