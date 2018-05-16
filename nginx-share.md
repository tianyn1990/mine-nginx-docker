# 大纲

### 安装

见[这里](https://github.com/tianyn1990/mine-nginx-docker/blob/master/docker&nginx.md#%E6%9C%AC%E5%9C%B0%E5%AE%89%E8%A3%85nginx)

### 运行

见[这里](https://github.com/tianyn1990/mine-nginx-docker/blob/master/docker&nginx.md#%E5%AE%89%E8%A3%85%E9%85%8D%E7%BD%AEdocker)

### 基本配置

见：nginx.conf

1. 一般配置
2. gzip
3. include

### server 配置

见：conf.d/default.conf

1. server
2. location
3. https
4. http2
   - 查看是否生效 [chrome://net-internals/#http2](chrome://net-internals/#http2)
5. server : server_name
6. if + $host + rewrite
7. location : root alias
8. location : http2_push
9. default_server

### proxy_pass & upstream

见：xx

### 测试环境的nginx

使用 `~/.ssh/config` 管理，参考：[这里](https://www.barretlee.com/blog/2016/03/09/config-in-ssh-after-troubling-git-connection/)

例如：

```text
# 主机名：classb-haitao6.server.163.org
# 机房ip：10.165.139.201 （不是外网ip或内网ip） # http://doc.hz.netease.com/pages/viewpage.action?pageId=64392560
# 环境：test1
# 链接方法：
# > ssh test1-6
# > sudo -iu appops
Host test1-6
HostName  10.165.139.201
User hztianyanan
IdentityFile ~/.ssh/gitlab_rsa
Port  1046

# netease gitlab
Host g.hz.netease.com
HostName  g.hz.netease.com
IdentityFile ~/.ssh/gitlab_rsa
Port  22222

```
