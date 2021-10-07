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

### Makefile介绍

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
