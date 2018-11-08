# \(三\) 服务器规约

1.\*【推荐】\*高并发服务器建议调小TCP协议的time\_wait超时时间。

> 说明：操作系统默认240秒后，才会关闭处于time\_wait状态的连接，在高并发访问下，服务器端会因为处于time\_wait的连接数太多，可能无法建立新的连接，所以需要在服务器上调小此等待值。

```text
正例：在linux服务器上请通过变更/etc/sysctl.conf文件去修改该缺省值（秒）：
net.ipv4.tcp_fin_timeout = 30
```

2.\*【推荐】\*调大服务器所支持的最大文件句柄数（File Descriptor，简写为fd）。

> 说明：主流操作系统的设计是将TCP/UDP连接采用与文件一样的方式去管理，即一个连接对应于一个fd。主流的linux服务器默认所支持最大fd数量为1024，当并发连接数很大时很容易因为fd不足而出现“opentoomanyfiles”错误，导致新的连接无法建立。建议将linux服务器所支持的最大句柄数调高数倍（与服务器的内存数量相关）。

3.\*【推荐】\*给JVM设置-XX:+HeapDumpOnOutOfMemoryError参数，让JVM碰到OOM场景时输出dump信息。

> 说明：OOM的发生是有概率的，甚至有规律地相隔数月才出现一例，出现时的现场信息对查错非常有价值。

4.【参考】服务器内部重定向使用forward；外部重定向地址使用URL拼装工具类来生成，否则会带来URL维护不一致的问题和潜在的安全风险。
