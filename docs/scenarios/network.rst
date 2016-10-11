网络
==========

Twisted
-------

`Twisted <http://twistedmatrix.com/trac/>`_ 是一个事件驱动的网络引擎。可以用来构建基于多种不同网络协议的应用程序，包括http服务器/客户端、使用SMTP/POP3/IMAP或SSH协议的应用、即时通信应用以及 `更多 <http://twistedmatrix.com/trac/wiki/Documentation>`_ 。

PyZMQ
-----

`PyZMQ <http://zeromq.github.com/pyzmq/>`_ 是 `ZeroMQ <http://www.zeromq.org/>`_ 的Python绑定。ZeroMQ是一个高性能的异步消息库，其中一个最大的优点是采用了无代理的方式来处理消息队列。ZeroMQ的基本模式如下：

- 请求-应答: 把一组客户端关联到一组服务上。这属于一种远程过程调用及任务分发模式。
- 发布-订阅: 把一组发布者关联到一组订阅者上。这是一种数据分发模式。
- 推送-拉取（或管道）: 采用多阶段及循环输出/输入模式把一组节点关联起来。这是一种并行任务分发及收集模式。

快速上手参见 `ZeroMQ指南 <http://zguide.zeromq.org/page:all>`_ 。

gevent
------

`gevent <http://www.gevent.org/>`_ 是一个基于协程的Python网络库，在libev事件循环上利用greenlets封装了更加高层的同步API。
