# docker容器中运行nginx测试代码

## 参考

涉及到的docker文章，见[这里](./docker-doc.md)

另附收集的一点nginx文章，见[这里](./nginx-doc.md)

## 安装&配置docker

### 下载&安装

[Mac下载](https://docs.docker.com/docker-for-mac/install/#what-to-know-before-you-install)

测试

```bash
> docker version
```

### 修改镜像

1. 点击屏幕上方docker小图标
2. 选择 Preferances -> Deamon -> Registry-mirrors
3. Registry-mirrors选项增加一条：`https://registry.docker-cn.com`

### 下载image（容器模板）

```bash
> docker pull tianyn1990/nginx
```

### 将配置映射到本地

启动容器

```bash
> docker container run -it --rm --name mynginx \
  -p 127.0.0.1:8080:80 \
  tianyn1990/nginx \
  /bin/bash
```

启动nginx

```bash
> nginx
```

先测试一下（本地8080端口映射到了docker容器的80端口），访问：

[http://localhost:8080/](http://localhost:8080/)

然后，本地创建一个测试用目录，将docker容器中的nginx配置和资源，导出到本地

```bash
> cd ~/Documents
> mkdir mine-nginx
> cd mine-nginx
```

赋值容器的nginx配置到本地

```bash
> docker cp mynginx:/usr/share/nginx/html/ ./html
> docker cp mynginx:/etc/nginx ./conf
```

关闭容器

```bash
> docker container stop mynginx
```

### 使用本地配置启动容器的nginx

启动容器

```bash
> cd ~/Documents/mine-nginx
> docker container run -it --rm --name mynginx \
  -p 127.0.0.1:8080:80 \
  -p 127.0.0.1:443:443 \
  -v "$PWD/conf":/etc/nginx \
  -v "$PWD/html":/usr/share/nginx/html \
  tianyn1990/nginx \
  /bin/bash
```

启动nginx

```bash
> nginx
```

### 访问测试url

配置host

```host
127.0.0.1 aaaa.com
127.0.0.1 www.aaaa.com
127.0.0.1 bbbb.com
127.0.0.1 www.bbbb.com
127.0.0.1 cccc.com
127.0.0.1 www.cccc.com
```

访问一下链接测试

[https://cccc.com/pages/index.html](https://cccc.com/pages/index.html)

[https://bbbb.com/push/index.html](https://bbbb.com/push/index.html)

[http://localhost:8080/](http://localhost:8080/)

**现在，你可以修改本地的nginx配置和资源文件，然后在docker容器内执行reload命令即可测试nginx。**

常用的nginx命令有

```bash
# 启动nginx
> nginx

# 重启nginx
> nginx -s reload

# 停止nginx
> nginx -s stop
```

退出容器

```bash
> exit
```

## 本地安装nginx

> forMac

```bash
> brew -v
> sodu brew install nginx
> nginx -V
```

如果报错，可能是it部门限制了`/usr/local`的权限，试一下：

```bash
> sudo chmod -R 777 /usr/local/Cellar
> sudo chmod -R 777 /usr/local/bin
> sudo chmod -R 777 /usr/local/lib
```

然后再安装

```bash
> brew install nginx
> nginx -V
```
