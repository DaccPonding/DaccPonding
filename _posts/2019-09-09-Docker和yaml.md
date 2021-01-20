---
title: Docker和yaml
layout: post
tags:
  - Docker
---

# **9月9**

#### **Docker**

###### **Docker架构**

使用C/S架构。通过远程API管理和创建Docker容器。

Docker容器通过Docker镜像创建。

两者关系相当于对象与类。

| Docker 镜像(Images)    | Docker 镜像是用于创建 Docker 容器的模板。                    |
| ---------------------- | ------------------------------------------------------------ |
| Docker 容器(Container) | 容器是独立运行的一个或一组应用。                             |
| Docker 客户端(Client)  | Docker 客户端通过命令行或者其他工具使用 Docker API (https://docs.docker.com/reference/api/docker_remote_api) 与 Docker 的守护进程通信。 |
| Docker 主机(Host)      | 一个物理或者虚拟的机器用于执行 Docker 守护进程和容器。       |
| Docker 仓库(Registry)  | Docker 仓库用来保存镜像，可以理解为代码控制中的代码仓库。Docker Hub([https://hub.docker.com](https://hub.docker.com/)) 提供了庞大的镜像集合供使用。 |
| Docker Machine         | Docker Machine是一个简化Docker安装的命令行工具，通过一个简单的命令行即可在相应的平台上安装Docker，比如VirtualBox、 Digital Ocean、Microsoft Azure。 |

Docker是 Docker.Inc 公司开源的一个基于 LXC技术之上构建的**Container容器引擎**，基于Go语言并遵从Apache2.0协议开源。

**LXC**全拼是linux containners，linux容器，是一种虚拟化技术。Docker就是linux容器的一种封装提供简单易用的容器使用接口。

###### **Docker能干嘛**

开发者可以搭建他们的应用仅仅一次，就能保证让这个应用保持一致的跑在任何地方。运营人员可以将他们的服务器配置一遍，就能跑任何应用。

- 提供一次性环境。本地测试他人软件，持续集成的时候提供单元测试和构建的环境。
- 提供弹性的云服务。docker容器可以随开随关，很适合动态扩容和缩容。
- 组件微服务架构。通过多个容器，一台机器跑多个服务。

###### **Docker常用命令**

- `docker images` 显示本地已有镜像；
- `docker info` 显示docker系统信息；
- `docker commit -m -a` 提交更新后的镜像；
- `docker build` 通过Dockerfile来构建镜像；
- `docker import` 本地导入镜像；
- `docker search` 查找仓库中镜像；
- `docker push` 将镜像推送到仓库；
  - ``docker push 账号名/镜像名:tag`` 
- `docker pull` 将仓库中镜像下载到本地；
- `docker save -o mysql_5.6.tar mysql:5.6` 导出镜像到本地；
- `docker load &lt; mysql_5.6.tar` 载入镜像；
- `docker rmi` 移除镜像；
  - ``docker rmi imageID`` 移除该镜像
- `docker attach` 运行中容器的stdin，进行命令执行的动作；
- `docker history Images` 显示镜像的历史；
- ``docker rm`` 删除结束了的container
  - ``dokcer rm containerID``
- ``docker cp`` 在host和container之间拷贝文件
- ``docker ps`` 列出正在执行containner
  - ``docker ps -a `` 列出所有执行过的containner
  - ``docker ps -l`` 列出最近一次的container
- ``docker run`` 运行container
- ``docker tag`` 给镜像打tag(标签)
  - docker tag 镜像名:tag(不填默认为latest) 镜像名:tag



###### **docker-compose安装卸载**

```
sudo curl -L https://github.com/docker/compose/releases/download/1.17.1/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```

卸载

```
sudo rm /usr/local/bin/docker-compose
```



###### **YAML语言**

通用的数据串行化格式。专门用于写配置的语言，**非常简洁强大**，远比**JSON方便**。

语法规则：

- 大小写敏感
- 缩进表示层级关系
- 缩进不允许使用tab，只允许空格
- 缩进的空格数目不重要，只要相同层级元素左侧对齐即可。

#表示注释，该字符一直到行尾，都会被解析器忽略。

YAML支持的数据结构：

- 对象，键值对的集合，又称映射，哈希，字典
- 数组,按次序排列的一组值，又称为序列，列表
- 纯量，单个的不可再分的值。

###### **对象**

对象的一组键值对，使用冒号结构表示。

> ```javascript
> animal: pets
> ```

转为 JavaScript 如下。

> ```javascript
> { animal: 'pets' }
> ```

Yaml 也允许另一种写法，将所有键值对写成一个行内对象。

> ```javascript
> hash: { name: Steve, foo: bar } 
> ```

转为 JavaScript 如下。

> ```javascript
> { hash: { name: 'Steve', foo: 'bar' } }
> ```

###### **数组**

一组连词线开头的行，构成一个数组。

```
 - Cat
 - Dog
 - Goldfish
```

转成js为

```
['Cat','Dog','Goldfish']
```

子成员是一个数组，可以在该项下面缩进一个空格。

```
- 
  - Cat
  - Dog
  - Goldfish
```

```
[['Cat','Dog','Goldfish']]
```

数组也可以用行内表示法

```
animal:[Cat,Dog]
{animal:['Cat','Dog']}
```

###### **复合结构**

对象与数组结合使用构成混合结构

```
languages:
 - Ruby
 - Perl
 - Python 
websites:
 YAML: yaml.org 
 Ruby: ruby-lang.org 
 Python: python.org 
 Perl: use.perl.org 
 
 //js
 {
 	languages:['Ruby','Perl','Python'],
 	websites:{
 		 YAML: 'yaml.org',
 		 Ruby: 'ruby-lang.org',
 		 Python: 'python.org',
 		 Perl: 'use.perl.org',
 	}
 }
```