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

```text
https://cccc.com/pages/index.html
https://bbbb.com/push/index.html
http://localhost:8080/
```

另外，安装和配置docker，见[这里](./docker&nginx.md)