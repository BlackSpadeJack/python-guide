.. _install-linux:

在Linux上安装Python
====================

在最新版的CentOS、Fedora、Redhat Enterprise（RHEL）以及Ubuntu上已经 **搭载了开箱即用的Python 2.7**。

如果想查看自己安装的Python是什么版本，打开命令行运行如下命令：

.. code-block:: console

    $ python --version

一些老版本的RHEL和CentOS自带的Python 2.4对于现在的Python开发来说是无法接受的。幸运的是，存在 `Extra Packages for Enterprise Linux`_ ，这些包都基于Fedora的高质量包，而Fedora可以说是RHEL的试验场。这个仓库包含的Python 2.6包是定制的，可以与系统自带Python 2.4的包一一对应的安装。

.. _Extra Packages for Enterprise Linux: http://fedoraproject.org/wiki/EPEL

虽然说使用Python前不需要额外的安装或者配置，但是我强烈建议你在开始构建Python应用程序前，按照下一节描述的步骤安装工具和库。特别的，任何时候你都该安装Setuptools和pip，这样会让你更方便的使用其他第三方Python库。

Setuptools & Pip
----------------

最至关重要的两个第三方Python包是 `setuptools <https://pypi.python.org/pypi/setuptools>`_ 和 `pip <https://pip.pypa.io/en/stable/>`_。一旦安装好它们，你就可以使用一个简单的命令来下载、安装、卸载任何兼容的Python软件包。同时也可以很方便的利用它们在自己开发的Python软件里添加网络安装功能。

默认情况下，Python 2.7.9及之后（Python2系列）以及Python 3.4及之后的版本都已经包含了pip。

如果想知道pip是否已经安装，只需要打开命令行输入以下命令：

.. code-block:: console

    $ command -v pip

如果想自己安装pip，`参考官方pip的安装教程 <https://pip.pypa.io/en/latest/installing/>`_ - 这样会自动安装setuptools的最新版本。

虚拟环境
---------

虚拟环境主要是通过为各自创建虚拟的Python环境，把不同项目所依赖的包分隔在各自独立的空间内。这样就能解决“项目X依赖版本1.x，但是项目Y需要版本4.x”的窘境，同时保持全局site-packages目录的干净和可管理性。

例如，你可以在一个需要Django 1.10的项目上进行开发，同时维护一个依赖Django 1.8的项目。

请参考文档 :ref:`虚拟环境 <virtualenvironments-ref>` 来使用。也可以使用 :ref:`virtualenvwrapper <virtualenvwrapper-ref>` 来更简单的管理你的虚拟环境。

--------------------------------

本章是 `另外一篇文章 <http://www.stuartellis.eu/articles/python-development-windows/>`_ 的修改合成版本，与原文使用同样的许可证。