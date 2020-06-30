---
title: "Hyperledger Fabric 运行环境"
tags: ""
---

## hyperledger fabric 2.0 运行环境安装说明

-   安装 GO 语言环境

    `Linux: centos 7.X`
    `go version: 1.14`

        # 下载 go 语言安装包
        $ wget https://dl.google.com/go/go1.14.linux-amd64.tar.gz

        # 解压缩
        $ tar -zxvf go1.14.linux-amd64.tar.gz

        # 查看 go 解压缩目录，默认为当前目录下的 go 文件夹
        $ cd go
        $ pwd
        /usr/local/pid/go

        # 设置环境变量
        $ vim /etc/profile

        # 在文件末尾添加后保存退出
        export GOROOT=/usr/local/pid/go
        export PATH=$PATH:$GOROOT/bin

        # 加载配置
        $ source /etc/profile

        # 查看版本
        $ go version
        go version go1.14 linux/amd64
         

-   安装 Docker

    ```
    # 查看 linux 内核版本
    $ uname -r

    # 更新 yum 源 ...可省略
    $ yum update

    # 安装依赖包
    $ yum install -y yum-utils device-mapper-persistent-data lvm2

    # 设置阿里云的镜像
    $ yum-config-manager --add-repo https://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo

    # 安装 docker-ce 会自动选择最新稳定版
    $ yum install docker-ce

    # 设置开机自动启动
    $ systemctl enable docker

    # 启动 docker
    $ systemctl start docker

    # 查看版本
    $ docker version
    Client: Docker Engine - Community
    Version:           19.03.8
    API version:       1.40
    Go version:        go1.12.17
    Git commit:        afacb8b
    Built:             Wed Mar 11 01:27:04 2020
    OS/Arch:           linux/amd64
    Experimental:      false

    Server: Docker Engine - Community
    Engine:
     Version:          19.03.8
     API version:      1.40 (minimum version 1.12)
     Go version:       go1.12.17
     Git commit:       afacb8b
     Built:            Wed Mar 11 01:25:42 2020
     OS/Arch:          linux/amd64
     Experimental:     false
    containerd:
     Version:          1.2.13
     GitCommit:        7ad184331fa3e55e52b890ea95e65ba581ae3429
    runc:
     Version:          1.0.0-rc10
     GitCommit:        dc9208a3303feef5b3839f4323d9beb36df0a9dd
    docker-init:
     Version:          0.18.0
     GitCommit:        fec3683


    ```

-   卸载 Docker

        $ yum list installed | grep docker
        $ yum -y remove docker-ce-cli.x86_64

        # 查询安装特定版本
        $ yum list docker-ce --showduplicates | sort -r
        $ yum install docker-ce-18.03.1.ce-1.el7.centos

-   安装 Docker Compose

        # 官网地址 https://docs.docker.com/compose/install/
        # 下载最新的安装包
        $ curl -L "https://github.com/docker/compose/releases/download/1.25.4/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/pid/docker-compose

        # wget下载 （如果curl无法下载）
        $ wget https://github.com/docker/compose/releases/download/1.25.4/docker-compose-Linux-x86_64

        # 设置权限
        $ chmod +x docker-compose-Linux-x86_64

        # 修改文件名
        $ mv docker-compose-Linux-x86_64 docker-compose

        # 建立软连接
        $ ln -s /usr/local/pid/docker-compose /usr/bin/docker-compose

        # 查看版本
        $ docker-compose version
        docker-compose version 1.25.4, build 8d51620a
        docker-py version: 4.1.0
        CPython version: 3.7.5
        OpenSSL version: OpenSSL 1.1.0l  10 Sep 2019
         

-   安装 git

        $ yum install git

        # 查看版本
        $ git --version
        git version 1.8.3.1

-   安装NodeJS

        $ wget https://nodejs.org/dist/v12.16.1/node-v12.16.1-linux-x64.tar.xz
        $ wget https://nodejs.org/dist/latest-v8.x/node-v8.17.0-linux-arm64.tar.xz
        $ tar -vxf node-v12.16.1-linux-x64.tar.xz
        $ ln -s /usr/local/nodejs/bin/npm /usr/local/bin/
        $ ln -s /usr/local/nodejs/bin/node /usr/local/bin/

-   安装 PostgreSQL

    ```
    $ yum install https://download.postgresql.org/pub/repos/yum/11/redhat/rhel-7-ppc64le/pgdg-centos11-11-2.noarch.rpm
    $ yum install postgresql11-server postgresql11-client postgresql11-libs postgresql11-contrib postgresql11-devel
    $ /usr/pgsql-11/bin/postgresql-11-setup initdb
    $ systemctl enable postgresql-11
    $ systemctl start postgresql-11

    $ vim /var/lib/pgsql/11/data/postgresql.conf
    $ vim /var/lib/pgsql/11/data/pg_hba.conf

    ```

-   安装jq

        $ wget https://github.com/stedolan/jq/releases/download/jq-1.6/jq-linux64
