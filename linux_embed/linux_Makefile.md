# Makefile学习


<!-- vim-markdown-toc GFM -->

* [Makefile介绍](#makefile介绍)
* [Makefile变量](#makefile变量)
	* [系统变量](#系统变量)
	* [自定义变量](#自定义变量)
	* [自动化变量](#自动化变量)
* [Makefile模式规则](#makefile模式规则)
* [Makefile条件分支](#makefile条件分支)
* [Makefile常用函数](#makefile常用函数)
* [Makefile头文件依赖](#makefile头文件依赖)

<!-- vim-markdown-toc -->

### Makefile与Make介绍

`make`是一个在软件开发中所使用的工具程序（Utility software），经由读取`makefile`的文件以自动化建构软件。

它是一种转化文件形式的工具，转换的目标称为`target`；与此同时，它也检查文件的依赖关系，如果需要的话，它会调用一些外部软件来完成任务。

主要根据依赖文件的修改时间进行判断。大多数情况下，它被用来编译源代码，生成结果代码，然后把结果代码连接起来生成可执行文件或者库文件。

`make`使用`makefile`的文件来确定一个target文件的依赖关系，然后把生成这个target的相关命令传给shell去执行。
### Makefile变量

#### 系统变量

- `CC`: 指定编译器
- `AS`: 指定汇编器
- `MAKE`

#### 自定义变量

- 赋值符号
  * `=`: 延时赋值(只有当变量被引用时才赋值)
  * `:=`: 立即赋值
  * `?=`: 空赋值(当变量为空时才会赋值)
  * `+=`: 追加赋值(var1 var2)

#### 自动化变量

- `$<`: 第一个依赖项
- `$^`: 全部依赖项
- `$@`: 目标

### Makefile模式规则

- `%`: 匹配任意非空字符
- `*`: `shell`通配符

### Makefile条件分支

```
ifeq (var1,var2)
...
else
...
```
```
ifneq (var1,var2)
...
else ifeq
...
```

### Makefile常用函数

- `$(patsubst PATTERN,REPLACEMENT,TEXT)`: 匹配替换

**eg.**`$(patsubst %.c,%.o,x.c.c bar.c)`

**oucput:** `x.c.o bar.o`

- `$(notdir names...)`: 去除文件目录名

**eg.**`$(notdir src/foo.c hacks)`

**output:** `foo.c hacks`

- `$(wildcard pattern...)`: 获取匹配模式文件名

**eg.**`$(wildcard *.c)` 如果./有main.c abc.c

**output:** `main.c abc.c`

- `$(foreach var,list,text)`: 遍历列表 

**eg.**`$(foreach dir,$(dirs).$(wildcard $(dir)/*))`

**output:** `输出$(dirs)目录的所有文件`

### Makefile模板
```
ARCH ?= x86

#条件编译由ARCH值指定
ifeq ($(ARCH),x86)
	CC=gcc
else ifeq ($(ARCH),arm) 
	CC=arm-linux-gnueabihf-gcc
endif

TARGET=mp3 
BUILD_DIR=build
SRC_DIR=./module1 ./module2
INC_DIR=include      

CFLAGS=$(patsubst %,-I %,$(INC_DIR)) 
INCLUDES=$(foreach dir,$(INC_DIR),$(wildcard $(dir)/*.h))    

SOURCES=$(foreach dir,$(SRC_DIR),$(wildcard $(dir)/*.c))
OBJS=$(patsubst %.c,$(BUILD_DIR)/%.o,$(notdir $(SOURCES)))

VPATH=$(SRC_DIR)

$(BUILD_DIR)/$(TARGET):$(OBJS)
	$(CC) $^ -o $@

#music.o:music.c
#	$(CC) -c music.c -o music.o
#main.o:main.c
#	$(CC) -c main.c -o main.o

#将源文件编译成目标文件
$(BUILD_DIR)/%.o:%.c $(INCLUDES) | create_build
	$(CC) -c $< -o $@ $(CFLAGS)

.PHONY:clean create_build
clean:
	rm -r $(BUILD_DIR)
create_build:
	mkdir -p $(BUILD_DIR)

```
