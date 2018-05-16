# mine-nginx-docker
docker x nginx for tests

### 提交更新

```bash
> npm run build
> npm run publish
```

### 运行

```bash
> npm run build
> npm run run
```

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

[https://cccc.com/pages/index.html](https://cccc.com/pages/index.html)

[https://bbbb.com/push/index.html](https://bbbb.com/push/index.html)

[http://localhost:8080/](http://localhost:8080/)

**安装和配置docker，在docker容器中运行nginx测试代码，见[这里](./docker&nginx.md)**

涉及到的docker文章，见[这里](./docker-doc.md)

另附收集的一点nginx文章，见[这里](./nginx-doc.md)

nginx分享大纲，见[这里](./nginx-share.md)
