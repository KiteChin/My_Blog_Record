# Linux下与嵌入式Linux搭建NFS服务

<!-- vim-markdown-toc GFM -->

* [Linux通过shell链接wifi](#linux通过shell链接wifi)
	* [安装Network Manager](#安装network-manager)
	* [查看网络设备](#查看网络设备)
	* [打开WIFI](#打开wifi)
	* [扫描附近的WIFI](#扫描附近的wifi)
	* [连接WIFI](#连接wifi)
* [搭建NFS服务环境](#搭建nfs服务环境)
	* [Ubuntu安装NFS服务](#ubuntu安装nfs服务)
	* [配置NFS](#配置nfs)
	* [嵌入式Linux安装NFS客户端](#嵌入式linux安装nfs客户端)
	* [通过NFS查看共享目录](#通过nfs查看共享目录)
	* [通过NFS挂载共享目录](#通过nfs挂载共享目录)

<!-- vim-markdown-toc -->

## Linux通过shell链接wifi

### 安装Network Manager

`sudo apt install NetworkManager`  

### 查看网络设备

`sudo nmcli dev`  

### 打开WIFI

`sudo nmcli r wifi on`

### 扫描附近的WIFI

`sudo nmcli dev wifi`

### 连接WIFI

`sudo nmcli dev wifi connect "SSID" password "xxx"`

## 搭建NFS服务环境
### Ubuntu安装NFS服务

`sudo install nfs-kernel-server`

### 配置NFS

- 创建共享文件夹  

 `sudo mkdir /home/kitechin/share_work`

- 编辑配置文件  

 `sudo vim /etc/exports`  

- 添加配置信息：
 ```
 /home/kitechin/share_work *(rw,sync,no_root_squash)
 ```
 `/home/kitechin/share_work`: 共享目录  

 `*`: 所有地址都可以访问

 `rw`: 读写权限

 `sync`: 资料同步

 `no_root_squash`: 用户具有挂载目录到全部操作权限

### 嵌入式Linux安装NFS客户端

`sudo apt install nfs-common -y`

### 通过NFS查看共享目录

`showmount -e ip`

### 通过NFS挂载共享目录

`sudo mount -t nfs ip:/home/kitechin/share_work ~/share_work`

`-t nfs`: 指定挂载文件系统格式为NFS

`ip:/home/kitechin/share_work`: NFS服务器共享文件夹

`~/share_work`: 本地挂载目录






