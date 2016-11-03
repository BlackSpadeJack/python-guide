命令行应用
=========================

命令行应用也叫 `控制台应用 <http://en.wikipedia.org/wiki/Console_application>`_ ，是为文本界面设计的电脑程序，
比如 `shell <http://en.wikipedia.org/wiki/Shell_(computing)>`_ 。命令行应用通常接收多个输入作为参数或者子命令，
同时还会接收一些选项来作为标识或开关。

一些流行的命令行应用包括：

* `Grep <http://en.wikipedia.org/wiki/Grep>`_ - 文本数据搜索工具
* `curl <http://curl.haxx.se/>`_ - 采用URL语法进行数据传输的工具
* `httpie <https://github.com/jakubroztocil/httpie>`_ - HTTP客户端命令行工具，是cURL更为友好的替代品
* `git <http://git-scm.com/>`_ - 一种分布式版本控制系统
* `mercurial <https://www.mercurial-scm.org/>`_ - 一种分布式版本控制系统，主要采用Python开发

Clint
-----

`clint <https://pypi.python.org/pypi/clint/>`_ 是一个用于开发命令行应用的Python模块，包含很多有用的工具，
支持的特性包括：命令行颜色/缩排、简单强大的列输出、基于迭代器的进度条以及隐式参数处理等。

Click
-----

`click <http://click.pocoo.org/>`_  (Command-line Interface Creation Kit，首字母缩写) 是一个使用尽可能少的代码来实现命令行接口的Python包，该包采用了组合方式来实现，目前开发中，很快就可以使用了(译者注：其实早就可以用了）。这个“命令行接口构造工具”具有开箱即用的默认设置，同时不失高可配置性。

docopt
------

`docopt <http://docopt.org/>`_ 是一个轻量且Pythonic的包。通过解析POSIX风格的指令来创建命令行接口，很直观易用。

Plac
------

`Plac <https://pypi.python.org/pypi/plac>`_ 是对Python标准库中的 `argparse <http://docs.python.org/2/library/argparse.html>`_ 的简单包装，
采用声明式接口（即通过推断而不是手写命令的方式来构建出参数解析器）来隐藏其复杂性。其目标用户包括：初级用户、
程序员、系统管理员、科学家以及那些编写用完即扔脚本的人，该工具可以帮助他们快速简单的创建命令行接口。

Cliff
------

`Cliff <http://docs.openstack.org/developer/cliff/>`_  是一个构建命令行程序的框架。它采用了setuptools的入口点
来提供子命令、格式化输出以及其他扩展。该框架目的是用于创建包含多层级的命令，比如subversion和git，这些程序会处理某个
基本参数的解析，然后再调用对应的子命令来进行具体的工作。
