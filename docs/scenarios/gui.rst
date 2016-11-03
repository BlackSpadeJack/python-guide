GUI应用
================

按字母排序的GUI应用列表。

Camelot
-------
`Camelot <http://www.python-camelot.com>`_ 受Django管理界面的启发，在Python、SQLAlchemy和Qt的基础上提供了各种组件来构建应用。

可用的参考资源主要是其网站：http://www.python-camelot.com 和邮件列表: https://groups.google.com/forum/#!forum/project-camelot

Cocoa
-----
.. note:: Cocoa框架仅用于OS X，如果要编写跨平台的应用就不要考虑了。

GTK
---
PyGTK提供了对GTK+工具集的Python绑定。与GTK+库本身一样，也采用了GNU LGPL许可证。需要注意的是PyGTK目前只支持GTK-2.X的API（不支持GTK-3.0）。
对于新项目来说目前已不推荐使用PyGTK，现有的PyGTK应用也推荐迁移到PyGObject上。

PyGObject 又叫(PyGi)
--------------------
`PyGObject <https://wiki.gnome.org/Projects/PyGObject>`_ 提供了整个GNOME软件平台的Python绑定，且与GTK+ 3完全兼容。
这里有一份入门资料 `Python GTK+ 3指南 <https://python-gtk-3-tutorial.readthedocs.io/en/latest/>`_ 。

`API参考 <http://lazka.github.io/pgi-docs/>`_

Kivy
----
`Kivy <http://kivy.org>`_ 是一个Python库，可用于开发多点触屏的富媒体应用。其目标是为了能够进行快速轻松的交互设计及快速原型，
同时保证代码的可重用性和可部署性。

Kivy采用Python编写，基于OpenGL，支持多种输入设备，例如：鼠标、双向鼠标、TUIO触摸协议、Wii控制器、
Windows的WM_TOUCH消息、HID触摸以及苹果公司的产品等等。

Kivy由一个社区进行开发，非常活跃且免费使用，可在所有主流平台（Linux, OSX, Windows, Android）上使用。

主要资源可以在其网站上找到：http://kivy.org

PyObjC
------
.. note:: Cocoa框架仅用于OS X，如果要编写跨平台的应用就不要考虑了。

PySide
------
PySide是对跨平台GUI工具Qt的Python绑定。

  pip install pyside

https://wiki.qt.io/Category:LanguageBindings::PySide::Downloads

PyQt
----
.. note:: 如果你的软件没有完全遵从GPL，那么你需要购买商业许可证！

PyQt提供了Qt框架的Python绑定（见后面）。

http://www.riverbankcomputing.co.uk/software/pyqt/download

PyjamasDesktop (pyjs Desktop)
-----------------------------
PyjamasDesktop是Pyjamas的移植。PyjamasDesktop是一组用于桌面及跨平台框架的组件集，v0.6版本之后，PyjamasDesktop成了Pyjamas(Pyjs)的一部分。
简单来说，就是可以采用与Python Web应用完全相同的代码但是作为独立桌面应用来执行。

`PyjamasDesktop的Python Wiki <http://wiki.python.org/moin/PyjamasDesktop>`_ 。

主页： `pyjs Desktop <http://pyjs.org/>`_ 。

Qt
--
`Qt <http://qt-project.org/>`_ 是一个广泛使用的跨平台应用框架，可用于开发GUI以及非GUI应用。

Tk
--
Tkinter是Tcl/Tk之上很薄的面向对象包装层。 **可以使用Python标准库的优势使得它成为最方便且兼容性良好编程工具集** 。

Tk和Tkinter二者都可以在大多数的Unix平台使用，当然Windows及Macintosh系统也同样支持。从8.0版本开始，Tk在所有平台提供了原生界面的支持。


`TkDocs <http://www.tkdocs.com/tutorial/index.html>`_ 上有一份非常不错的多语言Tk教程，包含了Python的示例。更多信息见 `Python Wiki <http://wiki.python.org/moin/TkInter>`_ 。

wxPython
--------
wxPython是一个Python语言的GUI工具集。可以让Python程序员很简便的创建出健壮、功能丰富的图形用户界面。
它是一个Python的扩展模块（原生代码），通过包装著名的跨平台C++ GUI库wxWidgets来实现。

**安装wxPython：**
*到 http://www.wxpython.org/download.php#stable 下载适合你所使用操作系统的包。*
