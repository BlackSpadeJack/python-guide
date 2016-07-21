日志
=======

自Python 2.3之后，:mod:`logging` 模块已经成为标准库的一部分。:pep:`282` 里进对此行了简单的介绍。 但该文档是出了名的难读，唯有 `Python基础日志教程`_ 相对容易学习。

日志主要有两个目的：

- **诊断性日志** 记录应用操作的相关事件。如果用户引入日志模块用来报告错误，那么就可以通过在日志中搜索上下文来获取相关错误信息。
- **审计性日志** 记录用于商业分析的事件。用户进行的事务可以被提取出来，然后与另外的用户详细信息组合形成报告，或者用来进行优化，以达到更好的业务目标。


日志还是Print输出?
-------------------

只有在一种情况下 ``print`` 相比于日志是一个更好的选择：在命令行应用下展示帮助信息时。其他情况下，日志毫无疑问是更好的选择，原因如下：

- 每一个日志事件创建的 `日志记录`_ 包含有可读的诊断信息，例如文件名、完整路径、函数以及日志事件发生的行号。
- 除非你过滤掉所引用模块中的日志事件，否则它会被根logger自动访问，进而输出到应用程序本身的日志流中。
- 日志可以通过使用 :meth:`logging.Logger.setLevel` 或者通过设置属性 :attr:`logging.Logger.disabled` 为 ``True`` 选择性不显示。


函数库中的日志
------------------

`库开发中的日志配置`_ 是 `Python日志教程`_ 中的一部分。由于是 **用户** 而不是库本身来说明当日志事件出现时究竟发生了什么，所以脑子里要不断重复下警告：

.. note::
    强烈建议除NullHandler外不要添加任何其他handler到所写库的日志logger中。


当在一个库中初始化loggers时，最佳实践方法是仅使用全局变量 ``__name__`` 来创建这些loggers：:mod:`logging` 模块使用点号来创建层次性的loggers，所以，使用 ``__name__`` 可以确保不会有名字冲突。 

如下是来自 `requests源码`_ 的最佳实践示例 -- 可以把这段代码放到你的 ``__init__.py`` 文件中：

.. code-block:: python

    # 设置默认的日志处理模块，避免产生 "No handler found" 警告。
    import logging
    try:  # Python 2.7+
        from logging import NullHandler
    except ImportError:
        class NullHandler(logging.Handler):
            def emit(self, record):
                pass

    logging.getLogger(__name__).addHandler(NullHandler())



应用程序中的日志
-------------------------

`The Twelve-Factor App <http://12factor.net>`_ 是一份应用开发最佳实践的权威性参考，其中包含了一节 `日志最佳实践 <http://12factor.net/logs>`_ 。它重点提倡把日志事件当作事件流来对待，然后把事件流发送到标准输出，以便被应用环境进行处理。


至少有三种方式来配置logger：

- 使用INI格式的文件：
    - **优点**: 通过使用函数 :func:`logging.config.listen` 监听socket可以在程序运行时更新配置。
    - **缺点**: 相比在代码中配置logger，可控性较弱（*比如* 利用子类定制filters或者loggers）
- 使用字典或者JSON格式的文件：
    - **优点**: 除了能在程序运行时更新外，还可以通过 :mod:`json` 模块载入文件来更新，该模块自Python 2.6进入标准库。
    - **缺点**: 相比在代码中配置logger，可控性较弱。
- 使用代码：
    - **优点**: 对配置可进行完全控制。
    - **缺点**: 修改配置需要改动源代码。


使用INI文件配置的例子
~~~~~~~~~~~~~~~~~~~~~~~

这里我们把配置文件叫做 ``logging_config.ini`` 。该文件格式的更多细节可参考 `Python日志教程`_ 中的 `配置日志`_ 一节。

.. code-block:: ini

    [loggers]
    keys=root
    
    [handlers]
    keys=stream_handler
    
    [formatters]
    keys=formatter
    
    [logger_root]
    level=DEBUG
    handlers=stream_handler
    
    [handler_stream_handler]
    class=StreamHandler
    level=DEBUG
    formatter=formatter
    args=(sys.stderr,)
    
    [formatter_formatter]
    format=%(asctime)s %(name)-12s %(levelname)-8s %(message)s


然后，在代码中调用 :meth:`logging.config.fileConfig`：

.. code-block:: python

    import logging
    from logging.config import fileConfig

    fileConfig('logging_config.ini')
    logger = logging.getLogger()
    logger.debug('often makes a very good meal of %s', 'visiting tourists')
    

使用字典配置的例子
~~~~~~~~~~~~~~~~~~~~

在Python 2.7中，可以使用包含有详细配置的字典。:pep:`391` 中列出了在配置字典中哪些元素是必备的，以及哪些元素是可选的。

.. code-block:: python

    import logging
    from logging.config import dictConfig

    logging_config = dict(
        version = 1,
        formatters = {
            'f': {'format':
                  '%(asctime)s %(name)-12s %(levelname)-8s %(message)s'}
            },
        handlers = {
            'h': {'class': 'logging.StreamHandler',
                  'formatter': 'f',
                  'level': logging.DEBUG}
            },
        root = {
            'handlers': ['h'],
            'level': logging.DEBUG,
            },
    )

    dictConfig(logging_config)

    logger = logging.getLogger()
    logger.debug('often makes a very good meal of %s', 'visiting tourists')


直接在代码中配置的例子
~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: python

    import logging

    logger = logging.getLogger()
    handler = logging.StreamHandler()
    formatter = logging.Formatter(
            '%(asctime)s %(name)-12s %(levelname)-8s %(message)s')
    handler.setFormatter(formatter)
    logger.addHandler(handler)
    logger.setLevel(logging.DEBUG)

    logger.debug('often makes a very good meal of %s', 'visiting tourists')


.. _Python基础日志教程: http://docs.python.org/howto/logging.html#logging-basic-tutorial
.. _配置日志: https://docs.python.org/howto/logging.html#configuring-logging
.. _Python日志教程: http://docs.python.org/howto/logging.html
.. _库开发中的日志配置: https://docs.python.org/howto/logging.html#configuring-logging-for-a-library
.. _日志记录: https://docs.python.org/library/logging.html#logrecord-attributes
.. _requests源码: https://github.com/kennethreitz/requests
