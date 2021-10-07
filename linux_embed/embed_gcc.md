# gcc编译过程

<!-- vim-markdown-toc GFM -->

* [gcc预处理C文件](#gcc预处理c文件)
* [gcc编译C文件](#gcc编译c文件)
* [gcc编译汇编](#gcc编译汇编)
* [gcc链接可重定位文件](#gcc链接可重定位文件)

<!-- vim-markdown-toc -->

### 预处理

生成预编译文件(.i文件)

`gcc -E hello.c -o hello.i -v`

```
/usr/lib/gcc/x86_64-linux-gnu/9/cc1 -E -quiet -v -imultiarch x86_64-linux-gnu hello.c -o hello.i -mtune=generic -march=x86-64 -fasynchronous-unwind-tables -fstack-protector-strong -Wformat -Wformat-security -fstack-clash-protection -fcf-protection
```

### 编译

生成汇编代码(.s文件)

`gcc -S hello.i -o hello.s -v`

```
/usr/lib/gcc/x86_64-linux-gnu/9/cc1 -fpreprocessed hello.i -quiet -dumpbase hello.i -mtune=generic -march=x86-64 -auxbase-strip hello.s -version -o hello.s -fasynchronous-unwind-tables -fstack-protector-strong -Wformat -Wformat-security -fstack-clash-protection -fcf-protection
```

### 汇编

生成目标文件(.o文件)

`gcc -c hello.s -o hello.o -v`

```
as -v --64 -o hello.o hello.s
```

### 链接

生成可执行文件(二进制文件)

`gcc hello.o -o hello -v`

```
/usr/lib/gcc/x86_64-linux-gnu/9/collect2 -plugin /usr/lib/gcc/x86_64-linux-gnu/9/liblto_plugin.so -plugin-opt=/usr/lib/gcc/x86_64-linux-gnu/9/lto-wrapper -plugin-opt=-fresolution=/tmp/ccRRqwrE.res -plugin-opt=-pass-through=-lgcc -plugin-opt=-pass-through=-lgcc_s -plugin-opt=-pass-through=-lc -plugin-opt=-pass-through=-lgcc -plugin-opt=-pass-through=-lgcc_s --build-id --eh-frame-hdr -m elf_x86_64 --hash-style=gnu --as-needed -dynamic-linker /lib64/ld-linux-x86-64.so.2 -pie -z now -z relro -o hello /usr/lib/gcc/x86_64-linux-gnu/9/../../../x86_64-linux-gnu/Scrt1.o /usr/lib/gcc/x86_64-linux-gnu/9/../../../x86_64-linux-gnu/crti.o /usr/lib/gcc/x86_64-linux-gnu/9/crtbeginS.o -L/usr/lib/gcc/x86_64-linux-gnu/9 -L/usr/lib/gcc/x86_64-linux-gnu/9/../../../x86_64-linux-gnu -L/usr/lib/gcc/x86_64-linux-gnu/9/../../../../lib -L/lib/x86_64-linux-gnu -L/lib/../lib -L/usr/lib/x86_64-linux-gnu -L/usr/lib/../lib -L/usr/lib/gcc/x86_64-linux-gnu/9/../../.. hello.o -lgcc --push-state --as-needed -lgcc_s --pop-state -lc -lgcc --push-state --as-needed -lgcc_s --pop-state /usr/lib/gcc/x86_64-linux-gnu/9/crtendS.o /usr/lib/gcc/x86_64-linux-gnu/9/../../../x86_64-linux-gnu/crtn.o
```

