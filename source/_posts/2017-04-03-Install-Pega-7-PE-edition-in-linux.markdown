title:  在Linux下安装Pega7 PE版
date: 2017-04-03 20:21:29
updated: 2017-04-03 20:21:34
comments: true
tags: pega7
categories: pega
---

> Pega版本：Pega 7.1.9

## 前言
我们可以从Pega PDN上下载PE版本供日常练习使用，但是Pega7的PE版默认只提供了Windows的安装向导，若要在Linux下使用就要自己手动安装了。

## 安装步骤

### 下载Pega7 PE版

![pdn-download-pe-edition](pdn-download-pe-edition.png)

登录PDN后可以申请下载Pega7 PE版。

### 安装PostgreSQL数据库

这里以Ubuntu为例，安装PostgreSQL数据库
```SHELL
sudo apt-get install postgresql pgadmin3
```

安装好后打开pgadmin3，创建一个新role——pega，权限给满

![create-new-role](create-new-role.png)
![create-new-role-privilege](create-new-role-privilege.png)

分别运行这3条语句
```SQL
ALTER USER pega PASSWORD 'pega';

CREATE DATABASE pega WITH OWNER pega TEMPLATE template0 ENCODING 'UTF8';

ALTER USER pega SET SEARCH_PATH to "$user",personaledition,public;
```
![pgadmin3-script](pgadmin3-script.png)

### 导入Pega数据

找到第一步中下载到的Pega7 PE版，解压

![pega7-pe-edition](pega7-pe-edition.png)

找到data目录下的两个数据库dump文件

![database-dump-file](database-dump-file.png)

恢复Pega dump文件到数据库（用户名和密码都是pega），这一步的等待时间会很长
```SQL
pg_restore -U pega -h 127.0.0.1 -d pega sqlj.dump
pg_restore -U pega -h 127.0.0.1 -d pega pega.dump
```

### 配置Tomcat

在上一步的解压后，继续解压PRPC_PE.jar，再解压PersonalEdition.zip，这样我们就的到了tomcat，但现在的tomcat是不能用的，需要再配置一下

![tomcat-configuration](tomcat-configuration.png)

创建一个Pega目录，把刚才得到的tomcat复制过来，再创建一个temp目录

![create-pega-directory](create-pega-directory.png)

进入tomcat的bin目录，把所以shell脚本加上运行权限
```SHELL
chmod +x *.sh
```

再进入conf目录，修改配置文件

`context.xml`
搜索@PG_PORT，把其替换成你PostgreSQL数据库的端口，默认是5432
搜索@TEMP_DIR，把其替换成你刚才创建的temp目录

![context-configuration](context-configuration.png)

`server.xml`
搜索@TCHTTP，把其替换成8080（或你想使用的tomcat端口）

![server-configuration](server-configuration.png)

### 启动Pega7
切换到tomcat的bin目录启动tomcat

```SHELL
./startup.sh
```
![start-tomcat](start-tomcat.png)

然后等待Pega7启动好就可以使用了

![run-pega7](run-pega7.png)
