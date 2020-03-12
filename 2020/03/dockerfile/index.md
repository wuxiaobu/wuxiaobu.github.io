# Dockerfile


Dockerfile是一个文本格式的配置文件，用户可以使用Dockerfile来快速创建自定义的镜像。

一般而言，Dockerfile主体内容分为四部分：基础镜像信息、维护者信息、镜像操作指令和容器启动时执行指令。

下面给出一个Redis  Dockerfile示例：

```dockerfile
FROM redis:4.0.14

# 解释信息
LABEL maintainer="Wu Xiaobu <woshilieqie@163.com>"

ENV TZ=Asia/Shanghai \
    DATA_DIR=/home/work/app/redis/data \
    CONF_DIR=/home/work/app/redis/conf

# 设置系统时区
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN groupadd -r work && useradd -r -g work work; \
    mkdir -p $DATA_DIR && mkdir -p $CONF_DIR; \
    chown -R work:work /home

# 拷贝配置文件
COPY conf/redis.conf $CONF_DIR/redis.conf

VOLUME [$DATA_DIR]

# 导出端口
EXPOSE 6379
# 启动redis
CMD ["redis-server", "/home/work/app/redis/conf/redis.conf"]
```



1. **FROM**

    用来指定基础镜像，也就是你要在什么镜像上进行定制。

    格式为FROM <image> [AS <name>]或FROM <image>:<tag> [AS <name>]或FROM<image>@<digest> [AS <name>]。

2. **LABEL**

    可以为生成的镜像添加元数据标签信息，可以理解成添加一些说明、描述信息。这些信息可以用来辅助过滤出特定镜像，我这里仅添加了联系方式。

    格式为LABEL <key>=<value> <key>=<value> <key>=<value> …。

3. **ENV**

    用来设置环境变量，例如：定义一些系统版本、路径的环境变量，在后续RUN中可以使用（当然不仅仅是RUN中可用），也可以用改写原有的环境变量，例如：PATH，在镜像启动的容器中也会存在。

    格式为ENV <key> <value>或ENV <key>=<value> ...。

4. **RUN**

    运行指定命令。格式为RUN <command>或`RUN ["executable", "param1", "param2"]`。注意后者指令会被解析为JSON数组，因此必须用双引号。前者默认将在shell终端中运行命令，即/bin/sh -c；后者则使用exec执行，不会启动shell环境。指定使用其他终端类型可以通过第二种方式实现，例如`RUN ["/bin/bash", "-c","echo hello"]`。每条RUN指令将在当前镜像基础上执行指定命令，并提交为新的镜像层。当命令较长时可以使用\来换行。例如：

    ```dockerfile
    RUN apt-get update \
        && apt-get install -y \
        libjpeg-dev \
        libpng-dev \
        libfreetype6-dev \
        && docker-php-ext-configure gd \
        --enable-gd-native-ttf \
        --with-jpeg-dir=/usr/include \
        --with-freetype-dir=/usr/include/freetype2 \
        --with-png-dir=/usr/include \
    ```

5. **COPY**

    将宿主机的内容复制到容器中指定的路径。格式为COPY <src> <dest>。复制本地主机的<src>（为Dockerfile所在目录的相对路径，文件或目录）下内容到镜像中的<dest>。目标路径不存在时，会自动创建。路径同样支持正则格式。COPY与ADD指令功能类似，当使用本地目录为源目录时，推荐使用COPY。

6. **EXPOSE**
    声明镜像内服务监听的端口。一般设置为应用程序使用常见的端口，例如Redis设置为：6379

    格式为EXPOSE <port> [<port>/<protocol>...]。

    **注意该指令只是起到声明作用，并不会自动完成端口映射。*

    如果要映射端口出来，在启动容器时可以使用-P参数（Docker主机会自动分配一个宿主机的临时端口）或-p HOST_PORT:CONTAINER_PORT参数（具体指定所映射的本地端口）

7. **VOLUME**

    创建一个数据卷挂载点。格式为VOLUME ["/data"]。

    过docker run命令的-v标识创建的挂载点只能对创建的容器有效。

    通过Dockerfile的 VOLUME 指令可以在镜像中创建挂载点，这样只要通过该镜像创建的容器都有了挂载点。

    还有一个区别是，通过 VOLUME 指令创建的挂载点，无法指定主机上对应的目录，是自动生成的。

    我们通过docker inspect 查看通过该dockerfile创建的镜像生成的容器，可以看到如下信息

    ![image-20200312192015951](/images/image-20200312192015951.png)

   

Dockerfile 已经写好了，通过下面的命令即可创建镜像。

`docker build -t xiaobu_redis:4.0.14 .`

编译完成后可用通过`docker images`查看当前的镜像列表数据

然后通过 `docker run --name redis -it -p 6379:6379 -d xiaobu_redis:4.0.14` 启动容器。



网络上有非常多关于 Dockerfile 该如何写的最佳实践，有几点特别重要： 

- 一个容器只运行一个进程； 
- 镜像层数尽可能少，当然还需要考虑可读性等方面的因素； 
- RUN指令应该用 \ 分成多行方便阅读； 
- 容器镜像要尽可能的小。



(未完…)
























































