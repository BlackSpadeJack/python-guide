选择一个解释器
==============

.. _which-python:

Python的现状 (2 vs 3)
~~~~~~~~~~~~~~~~~~~~~~~

当选择Python解释器的时候，总会面临一个问题：“我该使用Python 2还是Python 3呢？” 答案并不会像我们想的那么明确。


目前Python现状的基本情形如下：

1. Python 2.7 已经作为标配存在了 **很长** 一段时间。
2. Python 3 在语言层面引入了重要的改变（不兼容），这使得很多开发者不愿意尝试。
3. Python 2.7 将会继续发布必要的安全更新，直到2020 [#pep373_eol]_。
4. Python 3 仍然在继续进化，就像过去几年Python 2所发生的那样。

瞧，你也可以看到，这就是为什么不是一个容易的决定。


建议
~~~~~

我就直接说了：


**如果是下列情形，使用Python 3**

- 版本无所谓。
- 你对Python 3有深沉的爱。
- 你毫不关心对于2 vs 3的问题。
- 你不知道该用哪个版本。
- 想拥抱变化.

**如果是下列情形，使用Python 2**

- 你爱Python 2，并且被Python 3的一些特性搞的黯然神伤。
- 语言和运行时不再有变更时，可以提升软件的稳定性。
- 你依赖的软件需要用到Python 2.


那么，用Python 3咯？
~~~~~~~~~~~~~~~~~~~~

如果你要选择Python解释器，并且不那么固执己见，那么我推荐使用最新的Python 3.x, 因为每个新版本都会在标准库、安全性以及BUG修复上有所提升。发展就是进步。

考虑到这样，如果你有很重要的原因只能使用Python 2，例如用到了Python 2独有的库，该库Python 3中也没有备选方案，或者像我一样，极度喜欢Python 2，那么就使用Python 2。

通过 `Can I Use Python 3? <https://caniusepython3.com/>`_ 检查你依赖的软件是否会妨碍你采用Python 3。

`进一步阅读 <http://wiki.python.org/moin/Python2orPython3>`_

`编写同时支持Python 2.6、2.7和Python 3 <https://docs.python.org/3/howto/pyporting.html>`_ 的代码是完全有可能的。至于难易程度，取决于你所编写软件的类型。如果你是新手，可能还有更重要的方面需要考虑。

实现
~~~~~

当人们讨论 *Python* 的时候，通常不仅仅意味着这门编程语言，同时也指CPython实现。*Python* 实际上是一个规范，该规范有多种实现方式。

CPython
-------

`CPython <http://www.python.org>`_ 是用C语言编写的一种参考实现，它会把Python代码编译成中间字节码供虚拟机来解释执行。CPython对Python的包和C扩展模块提供了最高程度的兼容。

如果你正在编写基于Python的开源代码，并且想让尽可能多的人受益，CPython可以说是最好的选择。如果使用的包依赖于C扩展，那么唯一的可选实现也只有CPython。

所有版本的Python语言都是C实现的，因为CPython是其参考实现。

PyPy
----

`PyPy <http://pypy.org/>`_ 是RPython实现的解释器，RPython是Python的子集，具有静态类型。这个解释器的特点是带有JIT编译器并且支持多种后端（C，CLI，JVM）。

PyPy的目标是在提高性能的同时，最大限度的保持与CPython参考实现的兼容性。

如果你想提高自己Python代码的性能，PyPy值得一试。在一套测试基准下，目前会`比CPython <http://speed.pypy.org/>快5倍以上`_。

PyPy支持Python 2.7。PyPy3 [#pypy_ver]_, 目前处于beta阶段，目前是支持Python 3。

Jython
------

`Jython <http://www.jython.org/>`_ 是Python的另一种实现，它会把Python代码编译为Java的字节码，然后被JVM（Java虚拟机）执行。另外，该实现也可以像使用Python模块一样来使用Java的类。

如果你需要与现有的Java代码进行交互，或者有其他原因需要在JVM上使用Python，Jython是最好的选择。

Jython目前支持到Python 2.7。 [#jython_ver]_

IronPython
----------

`IronPython <http://ironpython.net/>`_  是.NET框架上的实现。可以同时使用Python和.NET的库，并且可以让.NET上的其他语言来调用所写的Python代码。

`Python Tools for Visual Studio <http://ironpython.net/tools/>`_ 把IronPython直接集成到了Visual Studio开发环境中，给Windows上的开发者提供了一个不错的选择。

IronPython支持Python 2.7。 [#iron_ver]_

PythonNet
---------

`Python for .NET <http://pythonnet.github.io/>`_ 作为一个包，为本地已安装的Python和.NET公共语言运行时(CLR)提供了无缝的集成。它采取与IronPython （见上文）相反的方法，与其说是竞争，不如说是互补。

通过结合Mono, PythonNet可以让安装在非Windows操作系统（比如OS X和Linux）上的Python与.NET框架进行互操作。除了IronPython外，它也是可以毫无冲突运行的。

PythonNet支持范围从Python 2.3到Python 2.7。 [#pythonnet_ver]_

.. [#pypy_ver] http://pypy.org/compat.html

.. [#jython_ver] https://hg.python.org/jython/file/412a8f9445f7/NEWS

.. [#iron_ver] http://ironpython.codeplex.com/releases/view/81726

.. [#pythonnet_ver] http://pythonnet.github.io/readme.html

.. [#pep373_eol] https://www.python.org/dev/peps/pep-0373/#id2
