# 服务器相关

### 守护进程（Daemon Process）

* 守护进程（Daemon Process），也就是通常说的 Daemon 进程（精灵进程），是 Linux 中的后台服务进程。它是一个生存期较长的进程，通常独立于控制终端并且周期性地执行某种任务或等待处理某些发生的事件。

  守护进程是个特殊的孤儿进程，这种进程脱离终端，为什么要脱离终端呢？之所以脱离于终端是为了避免进程被任何终端所产生的信息所打断，其在执行过程中的信息也不在任何终端上显示。由于在 linux 中，每一个系统与用户进行交流的界面称为终端，每一个从此终端开始运行的进程都会依附于这个终端，这个终端就称为这些进程的控制终端，当控制终端被关闭时，相应的进程都会自动关闭。



* [服务器扩展](https://arcentry.com/blog/scaling-webapps-for-newbs-and-non-techies/)
* [ngrok](https://blog.csdn.net/zhangguo5/article/details/77848658)
* [服务器高可用](https://www.infoq.cn/article/weoXU*5PNc0XyRgO7k4j)

