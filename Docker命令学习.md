####一.docker images

该命令将列出当前本地环境中的所有的镜像文件

~~~bash
[root@dev ~]# docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             VIRTUAL SIZE
hello-world         latest              19b3f968b60c        3 weeks ago         1.84 kB
~~~

#####1.a选项 

~~~bash
[root@dev ~]# docker images -a
REPOSITORY          TAG                 IMAGE ID            CREATED             VIRTUAL SIZE
hello-world         latest              19b3f968b60c        3 weeks ago         1.84 kB
<none>              <none>              74bc6c628a00        3 weeks ago         1.84 kB
~~~

列出所有的镜像文件，一个镜像中可能还会包含其他镜像，使用-a选项就可以列出所有的镜像。

#####2.q选项

~~~bash
[root@dev ~]# docker images -q
19b3f968b60c
~~~

只显示镜像的ID

#####3.--digests

~~~bash
[root@dev ~]# docker images --digests
REPOSITORY          TAG                 DIGEST              IMAGE ID            CREATED             VIRTUAL SIZE
hello-world         latest              <none>              19b3f968b60c        3 weeks ago         1.84 kB
~~~

显示摘要信息

#####4.--no-trunc

~~~bash
[root@dev ~]# docker images --no-trunc
REPOSITORY          TAG                 IMAGE ID                                                           CREATED             VIRTUAL SIZE
hello-world         latest              19b3f968b60c5d8ccd301a63ddcdf94ba8ecd7e4df5002cca0f12f136239f8e0   3 weeks ago         1.84 kB
~~~

显示完整的镜像ID

####二.docker search

~~~bash
[root@dev ~]# docker search tomcat
NAME                                  DESCRIPTION                                     STARS     OFFICIAL   AUTOMATED
tomcat                                Apache Tomcat is an open source implementa...   2058      [OK]       
tomee                                 Apache TomEE is an all-Apache Java EE cert...   56        [OK]       
dordoka/tomcat                        Ubuntu 14.04, Oracle JDK 8 and Tomcat 8 ba...   49                   [OK]
davidcaste/alpine-tomcat              Apache Tomcat 7/8 using Oracle Java 7/8 wi...   30                   [OK]
............................
~~~

docker search 镜像名称，会显示docker hub上的与这个镜像名称匹配的镜像信息。

##### 1.-s选项

~~~bash
[root@dev ~]# docker search -s 30 tomcat
NAME                       DESCRIPTION                                     STARS     OFFICIAL   AUTOMATED
tomcat                     Apache Tomcat is an open source implementa...   2061      [OK]       
tomee                      Apache TomEE is an all-Apache Java EE cert...   56        [OK]       
dordoka/tomcat             Ubuntu 14.04, Oracle JDK 8 and Tomcat 8 ba...   49                   [OK]
davidcaste/alpine-tomcat   Apache Tomcat 7/8 using Oracle Java 7/8 wi...   30                   [OK]
~~~

-s表示的是点赞数超过某个值得选项。

#### 三.docker pull

~~~bash
[root@dev ~]# docker pull tomcat
~~~

从DockerHub上下载指定的镜像。

#### 四.docker rmi

~~~bash
[root@dev ~]# docker rmi hello-world
Error response from daemon: Conflict, cannot delete 19b3f968b60c because the container f382bbc2f8d2 is using it, use -f to force
Error: failed to remove images: [hello-world]
[root@dev ~]# docker rmi -f hello-world
Untagged: hello-world:latest
Deleted: 19b3f968b60c5d8ccd301a63ddcdf94ba8ecd7e4df5002cca0f12f136239f8e0
Deleted: 74bc6c628a008492ac5b8ebf00c36fd72512e653606efb4f5209501747a9efb4
[root@dev ~]# docker rmi -f 19b3f968b60c
Untagged: hello-world:latest
Deleted: 19b3f968b60c5d8ccd301a63ddcdf94ba8ecd7e4df5002cca0f12f136239f8e0
Deleted: 74bc6c628a008492ac5b8ebf00c36fd72512e653606efb4f5209501747a9efb4
~~~

删除镜像，rmi后面既可以指定镜像名，也可以指定镜像ID。

~~~bash
[root@dev ~]# docker rmi -f $(docker images -qa)
~~~

这和命令用于删除所有的镜像。

####五.docker run

~~~bash
[root@dev ~]# docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             VIRTUAL SIZE
centos              latest              c5507be714a7        7 weeks ago         199.7 MB
[root@dev ~]# docker run -it --name test c5507be714a7
[root@db3b8045ab34 /]# 
~~~

docker run命令选项：

- -i：以交互模式运行容器，通常与-t同时使用。
- -t：为容器重新分配一个伪输入终端，通常与-i同时使用。
- --name：为生成的容器分配一个名字。

使用docker ps命令可以查看正在运行的容器

~~~bash
[root@dev ~]# docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
db3b8045ab34        c5507be714a7        "/bin/bash"         16 seconds ago      Up 15 seconds                           test 
~~~

通过命令的执行结果可以发现，run命令开启的伪终端root@db3b8045ab34后面的hash值，其实就是新生成的容器的id，images的值是c5507be714a7，就是centos的images id。

#### 六.docker ps

docker ps命令用于显示运行的容器的信息。

- -a选项：用于显示正在运行的或者以前运行的所有的docker容器。
- -l选项：用于显示上一个运行的容器。
- -n Num选项：用于显示指定数量的之前运行的容器。
- -q 静默模式，只显示容器的ID。

#### 七.退出Docker的两种方式

- exit：用于永久退出该容器，退出之后docker ps不会再显示该容器的信息。
- Crtl + p + q：临时性退出该容器，退出之后docker ps可以显示该容器的信息。

#### 八.重启容器

对于之前已经停止了的容器，可以使用docker start containerID来启动该容器。

docker restart containerID，当容器正在运行的时候，可以市容该命令重启某个容器。

#### 九.停止容器

docker stop ContainerID，类似于正常关机的形式停止容器。

docker kill ContainerID，类似于强制关机形式的停止容器。

#### 十.删除容器

停止或者退出的容器，会留在Docker缓存中。

docker rm ContainerID可以删除这些已经停止了的容器。

docker rm -f强制删除容器

批量删除容器的两种方式：

- docker rm -f $(docker ps -aq)
- docker ps -a -q | xargs docker rm -f