.. _install-osx:

在Mac OS X安装Python
=====================

.. note::
    查看 :ref:`如何在OS X中安装Python 3<install3-osx>`.

最新的Mac OS X，Sierra **带有开箱即用的Python 2.7** 。

虽然说使用Python前不需要额外的安装或者配置，但是我强烈建议你在开始构建Python应用程序前，按照下一节描述的步骤安装工具和库。特别的，任何时候你都该安装Setuptools和pip，这样会让你更方便的使用其他第三方Python库。

OS X自带的Python版本对于学习来说绰绰有余，但是却不太适合用来开发。与 `官方当前的版本 <https://www.python.org/downloads/mac-osx/>`_ 相比，自带的Python版本太旧了，没有达到生产环境稳定性的要求。

正确的方式
-----------

接下来我们安装一个真正的Python。

在安装Python前，需要先安装一个C编译器。通过运行 ``xcode-select --install`` 可以以最快方式安装Xcode命令行工具。你也可以从Mac应用商店下载完整版本的 `Xcode <http://developer.apple.com/xcode/>`_ ，或者是最小化的非官方版本 `OSX-GCC-Installer <https://github.com/kennethreitz/osx-gcc-installer#readme>`_ 。

.. note::
    如果你已经安装了Xcode或者计划使用Homebrew，那就不要安装OSX-GCC-Install。同时安装二者时，软件会出现问题，并且很难诊断出原因。

.. note::
    如果是全新安装的XCode，还需要通过在终端运行 ``xcode-select --install`` 来添加命令行工具。


尽管OS X自带了大量的UNIX工具集，但是熟悉Linux系统的开发人员会发现缺少一个关键的组件：一个像样的包管理工具。`Homebrew <http://brew.sh>`_ 填补了这块空白。

为了 `安装Homebrew <http://brew.sh/#install>`_ ，需要打开 :file:`Terminal` 或者你最喜欢的OSX终端模拟器，然后执行如下命令：

.. code-block:: console

    $ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

这个脚本会在你安装之前说明它会对系统做出什么改变。一旦安装Homebrew，可以通过把下面一行内容添加到 :file:`~/.profile` 中，来把Homebrew目录添加到环境变量 :envvar:`PATH` 。

.. code-block:: console

    export PATH=/usr/local/bin:/usr/local/sbin:$PATH

接下来，我们就可以安装Python 2.7：

.. code-block:: console

    $ brew install python

或者Python 3:

.. code-block:: console

    $ brew install python3


这会花费一两分钟。


Setuptools & Pip
----------------

Homebrew也会安装Setuptools和 ``pip``。

Setuptools可以让你通过一个命令 ``easy_install`` 在网上下载和安装任何兼容的Python软件包。同时也可以很方便的利用它们在自己开发的Python软件里添加网络安装功能。

``pip`` 是一个易于安装和管理Python包的工具，相比于 ``easy_install`` 更加推荐 ``pip`` 。它在 `几个方面 <https://python-packaging-user-guide.readthedocs.io/en/latest/pip_easy_install/#pip-vs-easy-install>`_ 要更加优于 ``easy_install`` ，并且维护良好。


虚拟环境
---------

虚拟环境主要是通过为各自创建虚拟的Python环境，把不同项目所依赖的包分隔在各自独立的空间内。这样就能解决“项目X依赖版本1.x，但是项目Y需要版本4.x”的窘境，同时保持全局site-packages目录的干净和可管理性。

例如，你可以在一个需要Django 1.10的项目上进行开发工作，同时维护一个依赖Django 1.8的项目。

请参考文档 :ref:`虚拟环境 <virtualenvironments-ref>` 来使用。也可以使用 :ref:`virtualenvwrapper <virtualenvwrapper-ref>` 来更简单的管理你的虚拟环境。

--------------------------------

本章是 `另外一篇文章 <http://www.stuartellis.eu/articles/python-development-windows/>`_ 的修改合成版本，与原文使用同样的许可证。
