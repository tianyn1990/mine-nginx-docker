# 笔记：[Nginx开发从入门到精通](http://tengine.taobao.org/book/index.html#id2)

## 了解多进程、多线程

参考：[多线程和多进程的区别](http://blog.csdn.net/hairetz/article/details/4281931)

多线程：

1. 理论上来说，子进程应该完整地复制父进程的堆，栈以及数据空间，但是2者共享正文段。
2. 一般使用**写时复制**来提升性能

多进程：

1. 一个线程可以被切分为多个进程

多进程 vs 多线程

1. 前者开销大，后者开销较小
2. 线程安全：可重入（类似纯函数）

### 架构设计

![.](http://wiki.jikexueyuan.com/project/nginx/images/chapter-2-1.png)

1. Nginx 在启动后，会有一个 master 进程和多个 worker 进程。master 进程主要用来管理 worker 进程，包含：接收来自外界的信号，向各 worker 进程发送信号，监控 worker 进程的运行状态，当 worker 进程退出后(异常情况下)，会自动重新启动新的 worker 进程。而基本的网络事件，则是放在 worker 进程中来处理了（egg (๑•ᴗ•๑)）。
2. 一个请求，完全由 worker 进程来处理，而且只在一个 worker 进程中处理。
3. 每个 worker 里面只有一个主线程，多少个 worker 就能处理多少个并发，何来高并发呢？Nginx 采用了异步非阻塞的方式来处理请求。
4. 非阻塞就是，事件没有准备好，马上返回 EAGAIN，告诉你，事件还没准备好，过一会，再来检查一下事件，直到事件准备好了为止，在这期间，你就可以先去做其它事情。虽然不阻塞了，但你得不时地过来检查一下事件的状态，你可以做更多的事情了，但带来的开销也是不小的。
5. 异步非阻塞的事件处理机制，让你可以同时监控多个事件，同时可以设置超时时间，在超时时间之内，如果有事件准备好了，就返回。拿 epoll 为例，当事件没准备好时，放到 epoll 里面，事件准备好了，我们就去读写，当读写返回 EAGAIN 时，我们将它再次加入到 epoll 里面。
