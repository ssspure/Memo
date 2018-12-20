####1.install java on centos

直接通过curl普通方式下载的jdk安装文件，在用yum安装的时候回报错，查了一下可能是因为在oracle在下载的时候做了一些别的设置。可以通过下面的命令下载文件

~~~bash
wget --no-cookies --no-check-certificate --header "Cookie: gpw_e24=http%3A%2F%2Fwww.oracle.com%2F; oraclelicense=accept-securebackup-cookie" "http://download.oracle.com/otn-pub/java/jdk/8u112-b15/jdk-8u112-linux-x64.rpm"
~~~

然后通过yum命令就可以安装下载下来的jdk安装包

~~~bash
yum install -y jdk-8u112-linux-x64.rpm
~~~



#### 2.install docker on centos

※在CentOS上安装Docker，前提CentOS版本必须在6.5或者以上，64位操作系统，系统内核版本为2.6.32-432或者更高

直接从网上复制安装方法

1.Add the EPEL Repository

Docker is part of Extra Packages for Enterprise Linux (EPEL), which is a community repository of non-standard packages for the RHEL distribution. First, we’ll install the EPEL repository:

~~~bash
rpm -iUvh http://dl.fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm
~~~

2.Then, as a matter of best practice, we’ll update our packages:

~~~bash
yum update -y
~~~

3.Installation Now let’s install Docker by installing the docker-io package:

~~~bash
yum -y install docker-io
~~~

4.Once the installation completes, we’ll need to start the Docker daemon:

~~~bash
service docker start
~~~

5.And finally, and optionally, let’s configure Docker to start when the server boots:

~~~bash
chkconfig docker on
~~~



#### 3VIntualBox中的CentOS安装共享文件夹

The VirtualBox documentation[1] for how to install guest additions 

for Linux on a virtual host is somewhat messy. So here is what 

I did to make it work.

Install the packages required

yum update
yum install gcc kernel-devel make

reboot

Click: Devices/Install Guest Additions... 

Mount the ISO image with the guest additions

mkdir /cdrom
mount /dev/cdrom /cdrom

Install guest additions

/cdrom/VBoxLinuxAdditions.run

Share a folder from the VirtualBox control panel, giving it a share name.

ls  /media/sf_<share_name>

You could always mount the directory yourself as well

mkdir /a_folder_name 
mount -t vboxsf the_share_name /a_folder_name


[1] http://www.virtualbox.org/manual/ch04.html



