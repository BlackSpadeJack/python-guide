文档
=====

无论是项目文档还是代码文档，可读性都是Python开发人员重点关注的一方面。遵守一些简单的最佳实践可以为你和他人节省出一大堆时间来。

项目文档
---------


:file:`README` 文件在项目根目录下，主要给出项目维护者以及用户的常规信息。此文件最好是使用纯文本或者一些容易阅读的标记文本来编写，例如使用 :ref:`reStructuredText-ref` 或者Markdown。文件中应当包含几行内容来说明本项目或者本库主要用来干什么（要假设用户对此项目一无所知）、软件源代码的URL以及一些基本的信用信息。这个文件可以说是代码阅读人员的主要入口。

:file:`INSTALL` 文件在Python项目中不是那么的必要。安装指导通常只是一个命令，比如 ``pip install module`` 或者 ``python setup.py install`` ，可以直接添加到 :file:`README` 文件中。

:file:`LICENSE` 文件应该 *总是* 存在，并且需要指明软件在什么许可证下对公众可用。

:file:`TODO` 文件或者是 :file:`README` 中的 ``TODO`` 章节应当列出代码的开发计划。

:file:`CHANGELOG` 文件或者 :file:`README` 中的 ``CHNANGELOG`` 章节应当为最新版本的代码基变更作出一个简短的说明。

项目发布
---------

依项目不同，通常你的文档可能会由以下全部或者部分的内容构成：

- *简介* 主要是对该项目产品可以干什么作出一个非常简短的说明，可以使用一个或者两个极其简单的例子。这可以说是对你项目进行一个30秒的推销。

- *指南* 应当更加详细地展示一些初级的案例。读者可以一步一步根据案例来搭建一个可工作的原型。

- *API参考* 通常直接由代码来生成（参见 :ref:`docstrings <docstring-ref>` ）。其中会列出所有公开可用的接口、参数以及返回值。

- *开发文档* 主要是为潜在的贡献者人员提供。其中会包括代码约定以及项目的常规设计策略等。

.. _sphinx-ref:

Sphinx
~~~~~~

Sphinx_ 无疑是最为流行的Python文档工具。 **赶紧去使用吧。** 它会把 :ref:`restructuredtext-ref` 标记语言转换为各种格式的输出，包括HTML、LaTeX（用于可打印的PDF）、man手册以及普通文本。

网上还有一个 **非常好用** 且 **免费** 的 Sphinx_ 文档托管网站: `Read The Docs`_ 。赶紧去使用吧。通过配置它的提交钩子到你的源码仓库，可以实现自动化构建你的文档。

运行 Sphinx_ 时，会自动导入你的代码，并利用Python的内省机制提取出代码中的函数、方法以及类签名。同时还会提取出相应的文档字符串，并编译成结构良好又易于阅读的项目文档。

.. note::

    Sphinx以由API生成文档而闻名，但是对于常规项目文档的生成也可以完成的很好。本文档就是使用 Sphinx_ 构建并托管于 `Read The Docs`_ 上。

.. _Sphinx: http://sphinx.pocoo.org
.. _Read The Docs: http://readthedocs.org

.. _restructuredtext-ref:

reStructuredText
~~~~~~~~~~~~~~~~

大部分的Python文档使用 reStructuredText_ 来编写。这种标记语言就像是内建了各种可选扩展的Markdown。

`reStructuredText Primer`_ 和 `reStructuredText Quick Reference`_ 可以帮助你熟悉其语法。

**译者注:** 网上有中文教程，请自行搜索。

.. _reStructuredText: http://docutils.sourceforge.net/rst.html
.. _reStructuredText Primer: http://sphinx.pocoo.org/rest.html
.. _reStructuredText Quick Reference: http://docutils.sourceforge.net/docs/user/rst/quickref.html


代码文档建议
-------------

注释可以阐明代码，它们主要用来让代码更加容易理解。在Python中，注释以 ``#`` 开头。

.. _docstring-ref:

在Python中， *文档字符串(docstrings)* 描述了模块、类以及函数：

.. code-block:: python

    def square_and_rooter(x):
        """返回自身乘以自身后的平方根"""
        ...

通常可以参照 :pep:`8#comments` （Python风格指南）中的注释那一节。关于文档字符串的更多信息可以在 :pep:`0257#specification` （文档字符串约定指南）中找到。

注释代码片段
~~~~~~~~~~~~~~~

*不要使用三引号字符串来注释代码* 。这种方式并不是一个好的实践，因为类似grep这种面向行操作的命令行工具，是无法知晓那部分代码已失效的。更好的方式是确保正确的缩进，并在每个注释行前添加 ``#`` 。你使用的编辑器说不定可以很容易的完成这种功能，所以学习下如何注释/取消注释是很值得的。

文档字符串与魔法
~~~~~~~~~~~~~~~~~

一些工具会使用文档字符串来实现一些不仅限于文档的行为，比如单元测试的逻辑。这看上去很不错，但是你不会因为“这里就是这么做的”而永远不出错。

Sphinx_ 会把你的文档字符串解析为reStructuredText，然后渲染成HTML，这就可以很方便的把示例代码嵌入到文档项目中。

另外, Doctest_ 会读取所有格式为Python命令行输出样式（以">>>"为前缀）的文档字符串，然后执行这部分文档内容，检测命令的结果是否匹配紧接着的下一行内容。开发人员可以利用示例代码和函数使用说明一起来注释源码，顺便还可以确保代码被测试通过。

::
    
    def my_function(a, b):
        """
        >>> my_function(2, 3)
        6
        >>> my_function('a', 3)
        'aaa'
        """
        return a * b

.. _Doctest: https://docs.python.org/3/library/doctest.html


文档字符串与块注释
~~~~~~~~~~~~~~~~~~

二者并非不可交换。对于一个函数或者类，开头的注释块是开发人员的笔记说明。文档字符串则描述了函数或者类进行的 *操作* 。

.. code-block:: python

    # 这个函数会由于某些原因降低程序的运行速度
    def square_and_rooter(x):
        """返回自身乘以自身后的平方根"""
	...

.. see also:: 进一步阅读关于文档字符串的内容： :pep:`257`

与块注释不同，文档字符串内建于Python语言自身。这意味着在运行时你可以使用Python强大的内省能力来访问文档字符串，相比而言，注释则会被优化掉。几乎每一个Python对象都可以从 `__doc__` 属性或者内建的 `help()` 函数来访问文档字符串。

块注释通常用于解释一段代码是做什么的，或者阐述一个算法，而文档字符串更倾向于向别人解释你的代码中的某个函数如何使用以及一个函数、类或模块的主要目的是什么。


编写文档字符串
~~~~~~~~~~~~~~~~~~

根据所写函数、方法或类的复杂性，有时候单行文档字符串非常适用。以下是一个非常鲜明的例子::

    def add(a, b):
        """把两个数字相加，返回结果"""
        return a + b

文档字符串应该以一种非常易懂的方式来描述函数。对于一些不重要的函数或者类，简单的把函数签名（比如： `add(a, b) -> result` ）嵌入到文档字符串完全没必要。因为如果需要的话，使用Python的 `inspect` 模块可以很容易找到这些信息，而且通过阅读代码也可以很容易明白。

然而，在更大更复杂的项目中，最好还是对一个函数给出足够多的信息：它做了什么、有可能抛出什么异常、返回什么或者一些参数的相关细节。

Numpy项目使用了一种流行的文档风格来给出代码更详细的信息，称为 `Numpy风格`_ 的文档字符串。尽管这种注释风格会比之前的示例占用更多行，但是也让开发人员可以为一个方法、函数或类提供更多的信息::

    def random_number_generator(arg1, arg2):
        """
        Summary line.

        Extended description of function.

        Parameters
        ----------
        arg1 : int
            Description of arg1
        arg2 : str
            Description of arg2

        Returns
        -------
        int
            Description of return value

        """
        return 42

插件 `sphinx.ext.napoleon`_ 可以让Sphinx解析这种风格的文档字符串，方便你把Numpy风格的文档字符串包含到项目中。

最后，采用什么风格编写文档字符串并不重要，它们的目的都是为那些需要阅读或者修改你代码的人而服务的。只要这些文档是正确的、可以理解的并且你得到了想要知道的，那么赋予它的使命就算完成了。


如果还想对文档字符进一步的了解，参考 :pep:`257`

.. _thomas-cokelaer.info: http://thomas-cokelaer.info/tutorials/sphinx/docstring_python.html
.. _sphinx.ext.napoleon: https://sphinxcontrib-napoleon.readthedocs.io/
.. _`NumPy风格`: http://sphinxcontrib-napoleon.readthedocs.io/en/latest/example_numpy.html


其他工具
----------

你可能会在其他地方看到这些工具。参见 :ref:`sphinx-ref` 。

Pycco_
    Pycco是一个“文学编程风格的文档生成器”，是node.js里 Docco_ 的移植。它可以把代码转化成代码与文档并排展现的HTML格式。

.. _Pycco: https://pycco-docs.github.io/pycco/
.. _Docco: http://jashkenas.github.com/docco

Ronn_
    Ronn可以构建Unix的man手册。它可以把人类可读的文本转换为用于终端显示的roff格式以及用于Web的HTML格式。

.. _Ronn: https://github.com/rtomayko/ronn

Epydoc_
    Epydoc已经停止开发。使用 :ref:`sphinx-ref` 替代吧。

.. _Epydoc: http://epydoc.sourceforge.net

MkDocs_
    MkDocs是一个快速简单的静态网站生成器，致力于使用Markdown来构建项目文档。

.. _MkDocs: http://www.mkdocs.org/
