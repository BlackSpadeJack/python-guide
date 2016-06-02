阅读优秀代码
=============

Python设计背后的核心理念之一就是创建高可读性的代码。这种设计背后的动机很简单：Python程序员首要做的事就是阅读代码。

成为优秀Python开发者的秘诀之一就是读代码，了解代码，然后深入理解优秀的代码。

**译者注** ：下面是Youtube的视频，请自备梯子。

.. raw:: html

    <iframe width="650" 
            height="400" 
            src="https://www.youtube.com/embed/Jc8M9-LoEuo" 
            frameborder="0" allowfullscreen></iframe>


优秀的代码都会遵循 :ref:`代码风格` 中罗列的指导规范，并且会尽可能向其读者表达出清晰简洁的意图。

下面罗列一些推荐阅读的Python项目。这里的每一个项目都是Python编码的模范之作。

- `Howdoi <https://github.com/gleitz/howdoi>`_ 是一个搜索工具，采用Python开发。

- `Flask <https://github.com/mitsuhiko/flask>`_ 是基于Werkzeug和Jinja2的Python微框架。其目标：为实现构想而进行快速开发。

- `Diamond <https://github.com/python-diamond/Diamond>`_ 是一个Python守护程序，可以搜集监测数据并发送到 `Graphite <http://graphite.wikidot.com>`_ 或者其他后端。目前可以搜集包括CPU、内存、网络、IO设备、负载以及磁盘在内的相关数据。另外，它还提供了API来实现定制化的搜集器，可以从几乎任何来源搜集数据。

- `Werkzeug <https://github.com/mitsuhiko/werkzeug>`_ 开始只是供WSGI应用使用的一些简单的工具集合，后面逐渐发展成为高级WSGI工具模块中的一员。其中包括了强大的调试器、特性齐全的请求/响应对象、处理实体标签的HTTP工具、缓存控制头、HTTP日期、Cookie处理、文件上传、强大的URL路由系统以及一大堆社区贡献的其他模块。

- `Requests <https://github.com/kennethreitz/requests>`_ 是一个基于Apache2许可证的HTTP库，采用Python开发，非常人性化。

- `Tablib <https://github.com/kennethreitz/tablib>`_ 是一个与格式无关、实现数据集表格化输出的库，采用Python开发。


.. todo:: 增加上述每个项目里代码的典型示例。解释为什么这是优秀的代码。可以使用一些较为复杂的示例。

.. todo:: 讲述一些可以快速确定数据结构、算法并确定代码实现什么功能的技术。
