# 进程

### fork函数

`fork`函数会复制一份当前进程,并返回`pid_t`类型的参数。

```
#include <unistd.h>
pid_t fork()
```

`pid_t` :
- fork执行失败,返回-1
- 当前为父进程，返回子进程的PID
- 当前为子进程，返回0

```
#include <unistd.h>
#include <stdio.h>
#include <stdlib.h>

int main()
{
    pid_t PID;
    printf("before fork!!\r\n");

    PID = fork();
    switch(PID)
    {
	case -1:
	    perror("fork()");
	    exit(-1);
	//当前为子进程，返回0
	case 0:
	    printf("Child process PID:%d \r\n",getpid());
	    printf("Child process pid_t:%d \r\n",PID);
	    sleep(3);
	    break;
	//当前为父进程，返回子进程的PID
	default:
	    printf("Parent process PID:%d \r\n",getpid());
	    printf("Parent process pid_t:%d \r\n",PID);
    }


    return 0;
}
```
执行结果 :  
```
before fork!!
Parent process PID:17037
Parent process pid_t:17038
Child process PID:17038
Child process pid_t:0
```



### exec函数

```
l: 代表以列表形式传参
v: 代表以矢量数组形式传参
p: 代表使用环境变量来寻找指定文件
e: 代表用户提供自定义的环境变量
```

```
int execl(const char *path, const char *arg, ...);
int execlp(const char *file, const char *arg, ...);
int execv(const char *path, const char *argv[]);
int execve(const char *path, const char *argv[], const char *envp[]);
```

### exit
`exit`函数用来结束当前进程，

```
#include <stdlib.h>
void exit(int status);

#include <unistd.h>
void _exit(int status);
```

`exit`: exit函数会对输入输出流进行判断，释放所占用的资源以及清空缓冲区。

`_exit`: 立刻结束进程不检查缓冲区。
