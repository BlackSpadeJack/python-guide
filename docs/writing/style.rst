.. _代码风格:

代码风格
=========

如果询问一个Python开发者他最喜欢Python的哪一点，他们通常会说是其可读性。确实，高可读性是Python语言设计的核心准则之一，主要是基于这样一个事实：阅读代码要远多于编写代码。

Python代码之所以容易阅读和理解，原因之一就是它相对完整的编码风格指南以及“Pythonic”的惯用方式。

此外，当一个富有经验的Python开发者（一个Pythonista）指出一部分代码不够“Pythonic”的时，通常意味着这部分代码没有遵循通用的风格指南，并且没有按照最佳方式（即：最具有可读性）来进行缩进处理。

一些边际情况并没有统一的最佳实践方式来进行Python代码缩进，但是这种情况还是比较罕见的。

常规概念
---------

显式的代码
~~~~~~~~~~~~~

尽管在Python中可以使用任何的黑魔法，但是更提倡显式直白的方式。

**坏的代码风格**

.. code-block:: python

    def make_complex(*args):
        x, y = args
        return dict(**locals())


**好的代码风格**

.. code-block:: python

    def make_complex(x, y):
        return {'x': x, 'y': y}

在上述好风格的代码中，x和y可以从调用者那里显式的获取，然后返回一个显式的字典。使用这个函数的开发人员可以通过阅读代码的首行和尾行清楚的知道它是干什么的，而坏风格的代码则无法做到这点。

一行一语句
~~~~~~~~~~~

列表解析这种组合语句是被允许和鼓励的，这主要是由于其简洁和富有表现力，尽管如此，把两个不太关联的语句放在同一行却不是一种好的实践方式。

**坏的代码风格**

.. code-block:: python

    print 'one'; print 'two'

    if x == 1: print 'one'

    if <complex comparison> and <other complex comparison>:
        # do something


**好的代码风格**

.. code-block:: python

    print 'one'
    print 'two'

    if x == 1:
        print 'one'

    cond1 = <complex comparison>
    cond2 = <other complex comparison>
    if cond1 and cond2:
        # do something


函数的参数
~~~~~~~~~~~~

参数可以通过四种方式来传递给函数。


1. **位置参数** 是强制的且没有默认值。这是最简单的参数形式，这种方式可以被用在很少参数即可表达完整意义的函数中，并且这些参数顺序是很自然的。举个例子，在函数 ``send(message, recipient)`` 或者 ``point(x,y)`` 中，函数的使用者可以毫不费力的记住这两个函数需要两个参数，以及参数的顺序是什么。

  在这两个示例中，可以通过使用参数名来调用函数，如果采用这种方式，参数的顺序是可以交换的，调用方式为 ``send(recipient='World', message='Hello')`` 以及 ``point(y=2, x=1)`` ，但是与直接调用 ``send（'Hello', 'World')`` 和 ``point(1, 2)`` 相比，这会降低可读性，同时也造成了不必要的冗长。

2. **关键字参数** 不是强制的且可以有默认值。它们通常被用于发送给函数的可选参数。当函数有多于两个或三个位置参数时，函数签名会变得相对难记，这时，使用带有默认值的关键字参数会有帮助的多。例如，更加完整的 ``send`` 函数可能被定义为 ``send(message, to, cc=None, bcc=None)`` 。这里的 ``cc`` 和 ``bcc`` 是可选的，并且，在没有被传递其他值时，会被赋值为None。

  在Python中，调用带有关键字参数的函数有多种方式，比如，可以按照函数定义时参数的顺序来调用，这时不需要显式的命名参数，就像 ``send('Hello', 'World', 'Cthulhu', 'God')`` 中一样，发送秘密抄送给上帝。同样，也可以用命名参数的方式来按其他顺序调用，就像 ``send('Hello again', 'World', bcc='God', cc='Cthulhu')`` 。除非有很重要的原因，否则上述两种方式最好避免使用，而应该按照最接近函数定义的语法方式来调用: ``send('Hello', 'World', cc='Cthulhu', bcc='God')`` 。

  作为附注，参见 `YAGNI <http://en.wikipedia.org/wiki/You_ain't_gonna_need_it>`_ 准则，通常来说，移除那些似乎永远用不到但为了“以防万一”而添加的可选参数（以及它在函数内的逻辑部分），要比需要时再添加新的可选参数以及其逻辑要困难的多。（译者注：也就是说，如无必要，不必预留不太可能用到的可选参数）

3. **任意参数列表** 是传递给函数参数的第三种方式。如果函数的意图可以通过一个包含有数目可扩展的位置参数的函数签名表达出来，那么，可以定义一个使用了 ``*args`` 参数的函数。在函数体内， ``args`` 会是一个剩余位置参数组成的元组。例如， 可以使用每个接收者作为参数来调用 ``send(message, *args)`` ： ``send('Hello', 'God', 'Mom', 'Cthulhu')`` ，在函数体内 ``args`` 等同于 ``('God', 'Mom', 'Cthulhu')`` 。

  然而，这种构造有一些缺点，使用时应当谨慎。如果一个函数接收一组具有相同属性的参数，那么把函数定义成接收列表形式或者任意序列形式参数的方式会更加清晰。此例而言，如果 ``send`` 有多个接收者，最好显式的把它定义为： ``send(message, recipients)`` ，并且以 ``send('Hello', ['God', 'Mom', 'Cthulhu'])`` 方式调用。这样，函数使用者可以以预先定义好的列表形式来操作一组接收者，同时也打开了传递任何序列的可能性，包括无法解包为其他序列的迭代器。

4. **关键字参数字典** 是最后一种函数传递参数的方式。如果函数需要一系列未确定的命名参数，可以使用 ``**kwargs`` 构造。在函数体内， ``kwargs`` 是一个由所有尚未被函数签名中关键字参数捕获的其他命名参数的字典。

  与 *任意数目参数列表* 中一样，也必须谨慎使用这种方式，原因也是相似的：这种强力的技术应该在必要的时候才使用，如果存在更简单更清晰的方式即可满足函数的意图，那么应该避免使用 *关键字参数字典* 这种方式。

哪些参数作为位置参数，哪些参数作为可选的关键字参数，是否使用传递任意数目参数的高级技术，这都是由编写函数的开发者来决定的。如果明智的采用上述建议，完全有可能愉快的写出符合下列条件的函数：

* 易于阅读（函数名和参数无需过多解释）

* 易于修改（添加新的关键字参数不会破坏代码的其他部分）


避免魔法方法
~~~~~~~~~~~~~

作为黑客的强力的工具，Python自带了非常丰富的钩子和工具，允许你完成几乎任何奇技淫巧的事情。例如，它可以完成以下任何一件事：

* 改变对象的创建和初始化方式

* 改变Python解释器导入模块的方式

* 在Python中嵌入C代码（如果需要的话，建议这么做）

然而，所有这些选择都有许多缺点，所以使用最为直接的方式来达到你的目的总会更好。最为主要的缺点是使用这些构造方式严重影响了可读性。许多代码分析工具，例如pylint或者pyflakes将无法解析这些“魔幻的”代码。

我们认为Python开发者应该了解这些几乎无限的可能性，因为这会给你灌输自信，让你觉得没有不可逾越的难题。然而，知道怎么使用以及明确何时 **不** 去使用它们却非常重要。

就像功夫大师一样，一个Pythonista知道如何用一根指头杀人，然而却永远不会这么做。


我们都是负责的用户
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

如上所见，Python允许很多技巧，但是其中一些具有潜在的危险性。一个比较好的例子是客户端代码可以重写对象的属性和方法：在Python中，没有“private”关键字。这是Python的哲学，与像Java这样具有高度防御性的语言不同，高防御性语言会提供许多机制来阻止任何的误用，而Python会通过表明：我们都是负责的用户来达到这点。

这并不意味着，属性不能被认为是私有的，抑或Python无法进行合适的封装。相反，Python并不依赖于开发者在自身代码和其他人的代码之间竖立坚固的墙来达到隔离，Python社区更倾向于依赖一系列的惯例来表明这些元素不应当被直接访问。

对于私有属性，主要的惯例和实现细节是对所有“内部的元素”使用下划线前缀。如果客户端代码破坏这个规则，并且访问这些标记的元素，遇到的任何不正确行为或者问题都应当由客户端代码负责。

我们鼓励慷慨的使用这些惯例：任何不计划被客户端代码使用的方法或者属性应当使用下划线作为前缀。这样可以确保更好的责任分离以及对已有代码更容易的修改；把私有属性公有化总是可行的，反之，把公有属性私有化则困难的多。


返回值
~~~~~~~~

随着函数复杂性的增长，在函数体内使用多个返回语句变得很常见。然而，为了保持函数意图明确以及维持足以接受的可读性，更倾向于避免从函数体的多个出口点返回有意义的值。

在一个函数中返回值主要有两种情况：一种是函数正常处理完毕返回结果，另一种是返回错误情况，以便说明由于错误的输入参数或者其他原因，进而导致函数无法完成计算或任务。

如果在第二种情况下你不希望抛出异常，那么应当返回一个None或者False值来表明函数无法正常处理。这种情况下，最好在检测到不正确的上下文时尽早返回。这样有助于函数结构的扁平：返回语句（由于错误而返回）之后的代码可以认为是满足后续计算函数结果的情形。函数中往往会有多个这样的返回语句（由于错误而返回）。

然而，当一个函数在正常路径上有多个主要的退出点时，会导致难以调试返回结果，所以如果可能，应当保留单个退出点。这将有助于提取一些公共的代码路径，并且如果有多个退出点也说明函数很有可能需要重构。

.. code-block:: python

   def complex_function(a, b, c):
       if not a:
           return None  # 抛出异常可能会更好
       if not b:
           return None  # 抛出异常可能会更好
       # 尝试从a, b和c中计算x的复杂代码
       # 如果成功，暂时先不返回x
       if not x:
           # 计算x的其他方式
       return x  # 返回值x有单一的退出点有助于代码的维护


惯用语法
------------

编程习惯，简而言之就是写代码的 *方式* 。在 `c2 <http://c2.com/cgi/wiki?ProgrammingIdiom>`_ 和 `Stack Overflow <http://stackoverflow.com/questions/302459/what-is-a-programming-idiom>`_ 上有着对编程习惯广泛的讨论。

惯用的Python代码通常可以称为 *Pythonic* 的代码。

尽管通常有一种（当然，最好也只有一种）显而易见的方式来写惯用代码，但是对于Python初学者来说，如何写出符合语言习惯的Python代码却并不那么明显。所以，好的编程习惯必须主动学习才能获得。

一些通用的Python惯用语法如下：

.. _unpacking-ref:

解包
~~~~~

如果你知道列表或者元组的长度，你可以通过解包来给其中的元素分配名字。例如， ``enumerate()`` 会为列表中的元素生成一个二元组：

.. code-block:: python

    for index, item in enumerate(some_list):
        # do something with index and item

你也可以使用这种方式来交换变量：

.. code-block:: python

    a, b = b, a

嵌套的部分也可以解包：

.. code-block:: python

   a, (b, c) = 1, (2, 3)

在Python 3中，通过 :pep:`3132` 引入了一种新方法来扩展解包方式:

.. code-block:: python

   a, *rest = [1, 2, 3]
   # a = 1, rest = [2, 3]
   a, *middle, c = [1, 2, 3, 4]
   # a = 1, middle = [2, 3], c = 4

创建可忽略的变量
~~~~~~~~~~~~~~~~~

如果你需要把某值赋给变量（例如，在 :ref:`unpacking-ref` 中），但是又不会真正用到这个变量，那么可以使用 ``__`` ：

.. code-block:: python

    filename = 'foobar.txt'
    basename, __, ext = filename.rpartition('.')

.. note::
   许多Python风格指南建议使用单个下滑线 “``_``” 来处理那些用不到的变量，而不是这里建议的双下划线 “``__``” 。这种方式的问题在于 “``_``” 通常会被用作 :func:`~gettext.gettext` 函数的别名，同时，在交互式环境中，单下划线往往保存着最后一次操作的结果值。而双下划线与单下划线一样清晰方便，且消除了这两种情形下意外干扰的风险。


创建长度为N的且由相同元素组成的列表
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

使用Python列表的 ``*`` 操作符：

.. code-block:: python

    four_nones = [None] * 4

创建长度为N且元素为列表的列表
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

由于列表是可变的， ``*`` 操作符（如上）会创建一个包含有N个指向 `同一` 列表引用的列表，这种方式并不是我们想要的。这种情况下，我们使用列表解析：

.. code-block:: python

    four_lists = [[] for __ in xrange(4)]

注意：在Python 3中要使用range()代替xrange()

从列表创建字符串
~~~~~~~~~~~~~~~~

创建字符串的通用惯例是在空字符串上调用方法 :py:meth:`str.join` 。

.. code-block:: python

    letters = ['s', 'p', 'a', 'm']
    word = ''.join(letters)

这种方式会给变量 *word* 赋值为“spam”。这种惯用方式适用于列表和元组。

在聚合集中搜索元素
~~~~~~~~~~~~~~~~~~~~

有时候我们需要在聚合集中进行查找。这里我们来看看两种结构的查找方式：列表和集合。

代码示例：

.. code-block:: python

    s = set(['s', 'p', 'a', 'm'])
    l = ['s', 'p', 'a', 'm']

    def lookup_set(s):
        return 's' in s

    def lookup_list(l):
        return 's' in l

尽管两个函数看起来完全一样，但是由于 *look_set* 利用了Python集合属于哈希表的特性，二者之间的性能差异极大。为了确定一个元素是否在列表中，Python不得不遍历每一个元素，直到找到匹配的元素为止。这是很耗时的操作，尤其是列表很长的时候。另一方面，在集合中，元素的哈希值会直接告诉Python去哪里查找匹配的元素。所以即使集合再大，也可以很快的完成查找。字典中的查找方式也类似集合。更多信息请参见 `StackOverflow <http://stackoverflow.com/questions/513882/python-list-vs-dict-for-look-up-table>`_ 。如果想知道各种常用操作在这些数据结构上耗费时间的详细信息，请参见 `此页 <https://wiki.python.org/moin/TimeComplexity?>`_ 。

由于性能上的差异，以下情形使用集合或者字典来代替列表是个不错的主意：

* 聚合集包含有大量的元素

* 需要不断重复的在聚合集中搜索元素

* 没有重复的元素

对于一些小的聚合集，或者是不需要进行频繁搜索的聚合集，创建哈希表所花费的时间和内存，往往会比由于搜索速度提升而节省出的时间更多。


Python之禅
-------------

因 :pep:`20` 为人熟知，这是Python设计的指导准则。翻译 `在此 <https://wiki.python.org/moin/PythonZenChineseTranslate>`_ 。

.. code-block:: pycon

    >>> import this
    Python之禅, by Tim Peters

    优美胜于丑陋，明晰胜于隐晦。
    简单胜于复杂，复杂胜于繁芜。
    扁平胜于嵌套，稀疏胜于密集。
    可读性很重要。
    虽然实用性比纯粹性更重要，
    但特例并不足以把规则破坏掉。

    错误状态永远不要忽略，
    除非你明确地保持沉默，
    直面多义，永不臆断。

    最佳的途径只有一条，然而他并非显而易见————谁叫你不是荷兰人？

    置之不理或许会比慌忙应对要好，
    然而现在动手远比束手无策更好。

    难以解读的实现不会是个好主意，
    容易解读的或许才是。

    名字空间就是个顶呱呱好的主意。

    让我们想出更多的好主意！



这里有一些符合Python风格的例子，参见 `这些幻灯片来自Python用户组 <http://artifex.org/~hblanks/talks/2011/pep20_by_example.pdf>`_ 。

PEP 8
-----

:pep:`8` 是Python事实上的代码风格指南。`pep8.org <http://pep8.org/>`_ 上有一份高质量且易读的PEP 8版本。

强烈建议阅读这份指南。整个Python社区都尽最大努力遵守这份文档中提及的指导。一些项目可能会随着时间推移逐渐偏离其指导，而另外一些则会 `改善其中的建议 <http://docs.python-requests.org/en/master/dev/contributing/#kenneth-reitz-s-code-style>`_ 。 总之，确保你的代码遵循PEP 8通常来说是个不错的主意，并且与其他开发者合作时，这也有助于代码风格的统一。有一个命令行工具 `pep8 <https://github.com/jcrocholl/pep8>`_ ，可以帮助你检查代码是否符合规范。在终端执行下面的命令来安装：

.. code-block:: console

    $ pip install pep8

然后在需要检查的文件上运行这个命令，就可以得到检测报告：

.. code-block:: console

    $ pep8 optparse.py
    optparse.py:69:11: E401 multiple imports on one line
    optparse.py:77:1: E302 expected 2 blank lines, found 1
    optparse.py:88:5: E301 expected 1 blank line, found 0
    optparse.py:222:34: W602 deprecated form of raising exception
    optparse.py:347:31: E211 whitespace before '('
    optparse.py:357:17: E201 whitespace after '{'
    optparse.py:472:29: E221 multiple spaces before operator
    optparse.py:544:21: W601 .has_key() is deprecated, use 'in'

工具 `autopep8 <https://pypi.python.org/pypi/autopep8/>`_ 可以自动把代码重新格式化到符合PEP 8风格。安装方式如下：

.. code-block:: console

    $ pip install autopep8

可以用这个工具来直接格式化并修改文件：

.. code-block:: console

    $ autopep8 --in-place optparse.py

如果除去 ``--in-place`` 标志，它会把格式化后的代码直接输出到终端，以便查看。 ``--aggressive`` 标志会进行更大的修改，可以通过多次使用这个标志来达到更好的格式化效果。

约定
------

你应当按照本节的约定，以便你的代码更容易阅读。

检查变量是否等于常量
~~~~~~~~~~~~~~~~~~~~

对于一个值，你并不需要显示地把它与True、None或者0进行比较 - 只需要把它放到if语句中即可。参见 `Truth Value Testing <http://docs.python.org/library/stdtypes.html#truth-value-testing>`_ 了解哪些值可以认为是false。

**坏的代码风格**:

.. code-block:: python

    if attr == True:
        print 'True!'

    if attr == None:
        print 'attr is None!'

**好的代码风格**:

.. code-block:: python

    # 只需检查值即可
    if attr:
        print 'attr is truthy!'

    # 或者检查值的相反情况
    if not attr:
        print 'attr is falsey!'

    # 又或者，由于None可以被认为是false，可以显示的检查一下
    if attr is None:
        print 'attr is None!'

访问字典元素
~~~~~~~~~~~~~

不要使用 :py:meth:`dict.has_key` 方法。取而代之，使用 ``x in d`` 的语法形式或者给 :py:meth:`dict.get` 传递一个默认值。

**坏的代码风格**:

.. code-block:: python

    d = {'hello': 'world'}
    if d.has_key('hello'):
        print d['hello']    # 输出 'world'
    else:
        print 'default_value'

**好的代码风格**:

.. code-block:: python

    d = {'hello': 'world'}

    print d.get('hello', 'default_value') # 输出 'world'
    print d.get('thingy', 'default_value') # 输出 'default_value'

    # 或者:
    if 'hello' in d:
        print d['hello']

操作列表的简便方式
~~~~~~~~~~~~~~~~~~~

`列表解析 <http://docs.python.org/tutorial/datastructures.html#list-comprehensions>`_ 提供了一种强大简洁的方式来操作列表。此外，:py:func:`map` 和 :py:func:`filter` 函数使用了不同却更加简洁的语法。

**坏的代码风格**:

.. code-block:: python

    # 过滤大于4的元素
    a = [3, 4, 5]
    b = []
    for i in a:
        if i > 4:
            b.append(i)

**好的代码风格**:

.. code-block:: python

    a = [3, 4, 5]
    b = [i for i in a if i > 4]
    # 或者:
    b = filter(lambda x: x > 4, a)

**坏的代码风格**:

.. code-block:: python

    # 对每个列表元素加3
    a = [3, 4, 5]
    for i in range(len(a)):
        a[i] += 3

**好的代码风格**:

.. code-block:: python

    a = [3, 4, 5]
    a = [i + 3 for i in a]
    # 或者:
    a = map(lambda i: i + 3, a)

使用 :py:func:`enumerate` 来获取元素在列表中的位置。

.. code-block:: python

    a = [3, 4, 5]
    for i, item in enumerate(a):
        print i, item
    # 输出
    # 0 3
    # 1 4
    # 2 5

:py:func:`enumerate` 函数相对于手动计数有着更好的可读性，而且有助于迭代器的优化。

读取文件
~~~~~~~~~

使用 ``with open`` 语法来读取文件，这种方式会自动关闭文件。

**坏的代码风格**:

.. code-block:: python

    f = open('file.txt')
    a = f.read()
    print a
    f.close()

**好的代码风格**:

.. code-block:: python

    with open('file.txt') as f:
        for line in f:
            print line

``with`` 语句是一种更好的选择，因为这种方式会确保文件的关闭，即使在 ``with`` 代码块中抛出异常也能正确处理。


延续代码行
~~~~~~~~~~~

当代码的逻辑行长度超过限制时，需要把代码分割成逻辑上关联的几行。如果一行代码的最后一个字符是反斜杠，那么Python解释器会自动把后续的行连接起来。在一些情况下，这种做法很有用，但是通常应当避免这种方式，因为这种处理方式比较脆弱：行末尾反斜杠之后的空白会破坏代码并且导致一些无法预期的结果。

更好的解决方案是使用括号。如果一行开头有左括号，但是行末却没有相应的右括号，Python解释器会把下一行连接起来，直到遇到关闭的右括号。对于大括号和方括号也有类似的行为。

**坏的代码风格**:

.. code-block:: python

    my_very_big_string = """For a long time I used to go to bed early. Sometimes, \
        when I had put out my candle, my eyes would close so quickly that I had not even \
        time to say “I’m going to sleep.”"""

    from some.deep.module.inside.a.module import a_nice_function, another_nice_function, \
        yet_another_nice_function

**好的代码风格**:

.. code-block:: python

    my_very_big_string = (
        "For a long time I used to go to bed early. Sometimes, "
        "when I had put out my candle, my eyes would close so quickly "
        "that I had not even time to say “I’m going to sleep.”"
    )

    from some.deep.module.inside.a.module import (
        a_nice_function, another_nice_function, yet_another_nice_function)

然而，多半情况下，当不得不分割一行很长的代码时，往往预示着你同时尝试完成的功能太多，这有可能会妨碍可读性。
