# Linux上使用clash作为代理

最近一直在折腾这个clash如何在linux上跑起来，最开始看到网上的教程直接使用`clash for windows`这个客户端根据订阅地址生成的配置文件，把它复制到linux下clash并覆盖。由于这种方法比较麻烦就到网上找到了另一种方法，不过还是折腾了为好久。。

Clash是基于Go语言开发的，跨平台代理工具，支持Shadowsocks/v2ray，支持规则分流等。

* ## 0x01 安装

下载对应的二进制文件（Linux下载对应的`linux-adm64`），切换到文件目录。

```shell
gunzip clash-linux-amd64-v1.6.5.gz
sudo mv clash-linux-amd64-v1.6.5 clash
sudo chmod u+x ./clash
./clash
```

clash启动后会在`~/.config/clash/`目录生成配置文件`config.yaml`和`Country.mmdb`

* ## 0x02 修改配置

clash启动会根据`config.yaml`这个配置文件里的内容来选择节点。这时我们需要用代理提供商的订阅地址来更新这个配置文件。

先切换到你的配置文件目录中去`cd ~/.config/clash`

```linux
#使用wget获取
wget -O config.yaml 你的订阅地址加上\&flag=clash
#或者使用curl获取
curl 你的订阅地址加上\&flag=clash >> config.yaml
```

然后重新执行clash。

* ## 0x03 配置开机启动

在配置开机启动之前，将配置文件移动到`/etc`目录：
`
sudo mv ~/.config/clash /etc
`

使用vim对systemd进行配置
`sudo vi /systemd/system/clash.service`：

```shell
[Unit]
Description=Clash Daemon

[Service]
ExecStart=/usr/local/bin/clash -d /etc/clash/
Restart=on-failure

[Install]
WantedBy=multi-user.target
```
启用clash service:
`sudo systemctl enable clash.service`

手动启动clash.service:
`sudo systemctl start clash.service`

查看clash service的日志：
`journalctl -e -u clash.service`

