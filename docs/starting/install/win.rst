.. _install-windows:

在Windows上安装Python
======================

首先，到官网下载Python 2.7的 `最新版本 <https://www.python.org/ftp/python/2.7.12/python-2.7.12.msi>`_ 。如果你想确保安装的是最新版本，在 `官网主页 <http://python.org>`_ 上点击Downloads > Windows链接。

Windows的Python以MSI的格式提供，双击即可安装。MSI格式的文件允许Windows管理员使用标准工具来自动化安装。

按照设计，Python会安装到带有版本号的目录中，例如，Python 2.7会安装到 :file:`C:\\Python27\\` ，这样可以在系统上安装多个版本而不引起冲突。当然，对于Python文件，只能有一个默认解释器。这种安装方式也不会自动修改环境变量 :envvar:`PATH` ，这样你就可以控制运行哪个Python版本。

如果使用时，每次都要输入Python解释器的完整路径，显得太麻烦，所以最好把默认版本的Python目录添加到环境变量 :envvar:`PATH` 。假设你的Python安装位置是 :file:`C:\\Python27\\` ，把下述内容添加到 :envvar:`PATH` ：

.. code-block:: console

    C:\Python27\;C:\Python27\Scripts\

在 ``powershell`` 中运行下列命令可以很容易做到这点：

.. code-block:: console

    [Environment]::SetEnvironmentVariable("Path", "$env:Path;C:\Python27\;C:\Python27\Scripts\", "User")

当安装Python包时，一些新的命令会放置在上面的第二个目录（ :file:`Scripts` ）中，所以把这个目录添加到环境变量中是很有用的。

虽然说使用Python前不需要额外的安装或者配置，但是我强烈建议你在开始构建Python应用程序前，按照下一节描述的步骤安装工具和库。特别的，任何时候你都该安装Setuptools和pip，这样会让你更方便的使用其他第三方Python库。

Setuptools + Pip
----------------

最至关重要的的第三方Python软件是Setuptools，该工具扩展了标准库中disutils的安装和打包功能。一旦安装好它们，你就可以使用一个简单的命令来下载、安装、卸载任何兼容的Python软件包。同时也可以很方便的利用它们在自己开发的Python软件里添加网络安装功能。

通过运行 `ez_setup.py <https://bitbucket.org/pypa/setuptools/raw/bootstrap/ez_setup.py>`_ 这个脚本可以获得Windows上最新的Setuptools。

这时候就会新出现一个可以使用的命令：**easy_install**。不过这个命令已经被很多人认为废弃了，所以我们需要安装它的替代：**pip**。不像easy_install，Pip允许卸载安装好的包，并且维护也很活跃。

运行脚本 `get-pip.py <https://raw.github.com/pypa/pip/master/contrib/get-pip.py>`_ 可以安装pip。


虚拟环境
---------

虚拟环境主要是通过为各自创建虚拟的Python环境，把不同项目所依赖的包分隔在各自独立的空间内。这样就能解决“项目X依赖版本1.x，但是项目Y需要版本4.x”的窘境，同时保持全局site-packages目录的干净和可管理性。

例如，你在一个需要Django 1.10的项目上进行开发，同时维护一个依赖Django 1.8的项目。

请参考文档 :ref:`Virtual Environments <virtualenvironments-ref>` 来使用。也可以使用 :ref:`virtualenvwrapper <virtualenvwrapper-ref>` 来更简单的管理你的虚拟环境。

--------------------------------

本章是 `另外一篇文章 <http://www.stuartellis.eu/articles/python-development-windows/>`_ 的修改合成版本，与原文使用同样的许可证。
