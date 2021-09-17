# 代理介绍
当我们需要访问外国的一些资源时，可能速度会非常慢或者访问不了。这时你就需要代理，通过代理来加速访问这些网站。  

关于代理，比较常见的有socks和http(s)代理，它们主要区别在于http代理工作在应用层（ftp代理也属于这个），而socks代理工作在会话层。socks代理只是简单地传递数据包，而不必关心是何种应用协议（比如FTP、HTTP请求）。所以socks代理比其他应用层代理要快的多。

[toc]

## 系统代理
Linux下的代理设置在网络设置里面,下图为ubuntu 20.04 LTS的设置界面

![pic-1](https://github.com/KiteChin/Photo-cloud/raw/master/linux_proxy/pic_proxy_sys.png)

PS：不过很多情况，软件都不会走系统代理，一般软件都能设置独立的代理。  

## 命令行终端
刚刚提到许多软件是不走系统代理的，同样地命令行也是默认不走系统代理。所以你必须单独设置，比如你可以通过在命令行输入：  

`export http_proxy=127.0.0.1:7890`  
`export https_proxy=127.0.0.1:7890`  
`export socks_proxy=127.0.0.1:7890`  

当然这样输入的话`http_proxy`这个环境变量只会在当前环境有效，重启电脑后就没有效果了。  

你可以通过修改`/etc/profile`或`~/.profile`增加上述语句来使其在每次重启电脑后都能生效。

设置这些代理后，一般的命令，比如curl，wget都会走这个环境变量。

## 应用代理
比如git,它需用单独设置代理：  

`git config --global http.proxy 127.0.0.1:7890`

类似的还有很多，他们默认情况下不会使用系统代理和命令行代理，需要自己额外设置。

## profile介绍
profile主要是用来设置系统的环境变量。profile通常有两类，一类是系统级的profile即`/etc/profile`，另一类则是用户级`~/.profile`。  

在系统启动的时,先读取`/etc/profile`内的内容设置环境变量，然登陆用户后将读取`~/.profile`。  

登陆用户后会先继承系统当前的环境变量，然后再配置用户的环境变量,如果变量重复的话将会覆盖变量。

比如我在`/etc/profile`内配置`export https_proxy=127.0.0.1:7890`然后又在`~/.profile`内配置`export https_proxy=127.0.0.1:7899`的话。登陆相应的用户后`https_proxy`的值为`127.0.0.1:7899`。    








