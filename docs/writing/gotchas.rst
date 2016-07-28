常见的问题
==============

很大程度上来讲，Python作为一门简洁一致的语言，会尽量避免一些让人感到惊讶的特性。然而，还是有一些情况会让新手感到迷惑不解。

这些情形中的一些是故意为之，但却可能会令人感到惊讶。一些则已被证明是语言的缺陷。通常，对于一系列难以捉摸的行为，乍一看很奇怪，但是一旦你明白这种惊讶背后的底层原因，你就会觉得合乎情理。


.. _default_args:

可变的默认参数
-------------------------

对于Python初学者而言，最为常见、看起来令人惊讶的就是Python对于函数定义中可变默认参数的处理。

你所写的代码
~~~~~~~~~~~~~~

.. code-block:: python

    def append_to(element, to=[]):
        to.append(element)
        return to

你所期望发生的
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: python

    my_list = append_to(12)
    print my_list

    my_other_list = append_to(42)
    print my_other_list


每次调用函数时，如果第二个参数没有提供，那么应该创建一个新的列表，所以输出应该是::

    [12]
    [42]


事实上发生的
~~~~~~~~~~~~~~~~~~

.. testoutput::

    [12]
    [12, 42]


一旦函数被定义后，新的列表就会被创建，后续的每次函数调用都会使用同一个列表。

当函数被定义时，Python的默认参数就会被求值，而不是发生在每次函数调用时（这和Ruby是一样的）。这就意味着，如果你使用了可变的默认参数且改变该参数，你 *将会* 并且已经无意识的修改了之后所有调用该函数时的参数对象。

如何处理这种情况
~~~~~~~~~~~~~~~~~~

每次函数调用时，通过使用一个默认的参数值（:py:data:`None` 通常是一个好的选择）来提示该调用未提供参数，这时再创建一个新的对象。

.. code-block:: python

    def append_to(element, to=None):
        if to is None:
            to = []
        to.append(element)
        return to


当问题就不再是问题
~~~~~~~~~~~~~~~~~~~~

有时候你可以专门“利用”（注：按所预期的使用）这个行为来维护函数调用之间的状态。通常在编写缓存函数的时候会用到这个特性。


延迟绑定闭包
---------------------

另外一个迷惑源自Python在闭包中绑定变量的方式（或在周围全局作用域）。

你所写的代码
~~~~~~~~~~~~~~

.. testcode::

    def create_multipliers():
        return [lambda x : i * x for i in range(5)]
        

你所期望发生的
~~~~~~~~~~~~~~~~~~~~~

.. testcode::

    for multiplier in create_multipliers():
        print multiplier(2)


包含有5个函数的列表，每个函数拥有自己的封闭的 ``i`` 变量来与其参数进行乘运算，产生结果如下：

.. testoutput::

    0
    2
    4
    6
    8

事实上发生的
~~~~~~~~~~~~~~~~~~

.. testoutput::

    8
    8
    8
    8
    8

5个函数都已创建，然而这些函数却都把 ``x`` 乘以4。

Python的闭包采用 *延迟绑定* 。这意味着，闭包中使用到的变量，它的值是在内部函数被调用时才会进行查找。

这里例子中，无论何时，当所返回函数中的 *任何* 一个进行调用时， ``i`` 的值只有在调用时刻才在周边作用域中进行查找。而此刻，循环操作早已结束且 ``i`` 最后的值已变为4。 

对于这个问题，更糟糕的一点是对这个结果的广泛误解：人们以为这与Python中的 :ref:`lambdas <python:lambda>` 有关。其实，使用 ``lambda`` 表达式创建的函数没有任何特殊，事实上，使用常用的 ``def`` 创建的函数同样存在这个问题。

.. code-block:: python

    def create_multipliers():
        multipliers = []

        for i in range(5):
            def multiplier(x):
                return i * x
            multipliers.append(multiplier)

        return multipliers


如何处理这种情况
~~~~~~~~~~~~~~~~~~~~~~~~~~

最为常用的解决方案可能需要一点hack。多亏前面提及的关于函数参数默认值求值问题（参见 :ref:`default_args` ），你可以创建一个闭包，然后利用默认的参数值立刻绑定其参数，就像下面这样：

.. code-block:: python

    def create_multipliers():
        return [lambda x, i=i : i * x for i in range(5)]

另外一个方案，你可以使用函数 functools.partial：

.. code-block:: python

    from functools import partial
    from operator import mul

    def create_multipliers():
        return [partial(mul, i) for i in range(5)]


当问题就不再是问题
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

有时候，你是希望闭包可以按照这种延迟绑定的行为来执行的。在很多情形下，延迟绑定是非常有用的。当然，很不幸，通过循环来创建唯一函数成了一个反例的情形。


无处不在的字节码(.pyc)文件
---------------------------------

默认情况下，当从一个文件执行Python代码的时候，Python解释器会自动在磁盘上产生该文件的字节码文件，例如： ``module.pyc`` 。

这些 ``.pyc`` 文件不应该提交到源码的版本库中。

从理论上讲，由于性能的原因，这种行为默认是开启的。因为如果没有这些字节码文件，每次源码文件被载入执行时，都需要重新生成字节码。


禁用字节码(.pyc)文件
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

幸运的是，产生字节码的过程极其快速，所以在开发代码的时候并不需要担心这些。

当然，这些字节码文件相当的烦人，所以可以通过下面的方法来摆脱它们：

::

    $ export PYTHONDONTWRITEBYTECODE=1

一旦设置 ``$PYTHONDONTWRITEBYTECODE`` 环境变量，Python就不会再产生字节码文件，这样你的开发环境可以保持干净整洁。

我建议在你的 ``~/.profile`` 文件中设置这个环境变量。

移除字节码(.pyc)文件
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

如果已经存在字节码文件，下述命令可以移除这些文件::

    $ find . -name "*.pyc" -delete

在项目的跟目录下执行这行命令，所有的 ``.pyc`` 文件瞬间就会消失的无影无踪。6不6?
