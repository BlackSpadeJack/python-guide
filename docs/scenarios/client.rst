网络应用
====================


HTTP
::::

超文本传输协议是一种用于分布式、协作化、超媒体信息系统的应用协议。HTTP是万维网中数据交互的基础。

Requests
--------

Python标准库中的urllib2模块提供了你可能会用到的绝大部分HTTP功能，然而，该模块的API却十分难用。该模块是为不同时间段、不同web构建的。所以，即使要完成一个很简单的任务也需要大量的工作（甚至需要重写一些方法）。


Requests做了Python HTTP的所有工作 — 可以无缝的集成web服务。通过使用Requests，不再需要人工添加查询字符串到URL中，又或者编码POST数据。Keep-alive以及HTTP连接池都是100%的自动完成，这是通过内嵌在Requests中的urllib3来完成的，

- `参考文档 <http://docs.python-requests.org/en/latest/index.html>`_
- `PyPi <http://pypi.python.org/pypi/requests>`_
- `GitHub <https://github.com/kennethreitz/requests>`_


分布式系统
::::::::::::::::::::


ZeroMQ
------

ØMQ（也写作ZeroMQ、0MQ或ZMQ）是一个高性能的异步消息库，旨在用于高扩展性的分布式或并发应用中。它提供了一个消息队列，但与面向消息的中间件有所不同，
ØMQ系统不需要特定的消息协商器就可以运行。库本身的设计与socket API有着相似的接口。

RabbitMQ
--------

RabbitMQ是一个实现了高级消息队列协议（AMQP）的开源消息协商器软件。RabbitMQ服务器采用Erlang编程语言实现，并且构建在开放电信平台（OTP）上来达到集群化和容错。所有主流的编程语言都实现了与协商器交互的客户端。

- `主页 <http://www.rabbitmq.com/>`_
- `GitHub组织 <https://github.com/rabbitmq?page=1>`_
