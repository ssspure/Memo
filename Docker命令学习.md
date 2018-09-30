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