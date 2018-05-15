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
  tianyn1990/nginx
  /bin/bash
```

本地创建一个测试用目录

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
> docker container run -it --rm --name mynginx \
  -v "$PWD/conf":/etc/nginx \
  -v "$PWD/html":/usr/share/nginx/html \
  tianyn1990/nginx \
  /bin/bash
```

启动nginx

```bash
> nginx
```

现在，你可以自由修改本地的nginx配置和资源文件，然后执行nginx reload命令即可。

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

## 访问测试url

配置host

```host
127.0.0.1 aaaa.com
127.0.0.1 www.aaaa.com
127.0.0.1 bbbb.com
127.0.0.1 www.bbbb.com
127.0.0.1 cccc.com
127.0.0.1 www.cccc.com
```

访问

```text
https://cccc.com/pages/index.html
https://bbbb.com/push/index.html
http://localhost:8080/
```

## 本地安装nginx

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
