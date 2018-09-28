虚拟机中的Linux系统设置静态IP方法

1.打开下面这个文件

~~~bash
vim /etc/sysconfig/network-scripts/ifcfg-eth0
~~~



2.在文件中加入下面的内容并保存关闭文件

~~~bash
DEVICE="eth0"
BOOTPROTO="static"
HWADDR="00:1C:42:54:FF:21"
IPV6INIT="yes"
NM_CONTROLLED="no"
ONBOOT="yes"
TYPE="Ethernet"
IPADDR=192.168.0.200
NETMASK=255.255.255.0
GATEWAY=192.168.0.1
UUID="2a125218-1eb3-49cb-934f-fbf62c2cef84"
~~~



3.重启网络服务

~~~bash
service network restart
~~~

