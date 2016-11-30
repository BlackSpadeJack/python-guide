测试你的代码
=================

对自己的代码进行测试是非常重要的一步。

同时编写测试代码和实际运行的代码是一个非常好的习惯。合理利用这种方法可以帮助你更加精确的定位代码功能，并构建出一个更加解耦的架构。

测试中一些通用的准则：

- 一个测试单元应当聚焦于一个很小的功能并证明其实现的正确性。

- 每一个测试单元必须保持完全独立。保证既可以单独运行，又可以集成在测试套件中运行，而不必考虑其调用的顺序。这个规则暗含这样的意思：每个测试载入的数据集必须是全新的，并且完成测试后需要清理这些数据集。这通常通过方法 :meth:`setUp()` 和 :meth:`tearDown()` 来实现。

- 尽可能的使得测试集可以快速运行。如果单单一个测试就需要运行几毫秒的话，不仅会降低开发速度，也可能无法按照需要的那样尽可能频繁的运行测试。在某些情况下，测试集由于工作在复杂的数据结构上，且每次都要载入这些数据结构，所以测试无法快速运行。这时，可以把这种比较重量级的测试集放在单独的测试套件中，该测试套件通过计划任务来运行，而其他测试集则可以尽可能频繁的运行。

- 学习使用工具，并学习如何运行一个单独的测试或者测试用例。这样，当在模块中开发一个函数时，可以频繁的运行这个函数的测试，理想的方式是每次保存代码时自动运行对应的测试。

- 在每次进行编码任务前运行全套的测试套件，完成此次编码任务后再次运行。这会让你更确信自己的编码没有对代码的其他部分造成任何破坏。

- 通过实现钩子，把代码推送到共享仓库之前自动运行所有测试集是一个好的主意。

- 如果你正在进行开发中，并且由于其他原因不得不打断目前的开发工作，那么，对接下来要开发的部分编写一个损坏的单元测试是个不错的主意。当你回来继续工作时，你可以有个类似指针一样的东西告诉你目前工作在哪个地方，这样就可以快速回归开发状态。

- 调试代码的第一步：编写一个新的测试来精确的暴露出BUG。尽管不可能总这样做，但是，那些捕获BUG的测试集可以说是项目中最具有价值的一部分。

- 给测试函数命名一个长的具有描述性的名字。这里的代码风格与实际运行的代码略微有一些不同，对于实际运行的项目代码，我们更倾向于短命名。原因在于，测试函数从不会被显示的调用。在实际运行的代码中 ``square()`` 或者 ``sqr()`` 都是可以的，但是在测试代码中，你应该命名为 ``test_square_of_number_2()`` 、 ``test_square_negative_number()`` 。这些函数名会在测试失败时显示，所以应当尽可能的具有描述性。

- 当出现错误或者不得不进行改变时，如果有一个好的测试集，你和其他维护者就可以大量的依赖测试套件来修复问题所在，或者修改给定的行为。因此，相比于实际运行的代码，测试代码被阅读的次数至少会与其一样多，甚至更多。这种情况下，目的不清晰的单元测试用处并不大。

- 测试代码的另外一个用途是作为新开发人员的入门介绍。当有人不得不在代码基上进行工作时，运行并阅读相关的测试代码通常是他们开始的最好方式。他们可以发现热点所在、哪些地方是难点以及一些边边角角的情形。如果他们想添加某个功能，第一步要做的就是添加一个测试，通过这种方法，确保新功能不再是一个没有嵌入到接口中的工作路径。


基础知识
::::::::::


单元测试
---------

:mod:`unittest` 是Python标准库内置的测试模块。如果使用过JUnit/nUint/CppUnit系列工具中的任何一个，你会发现这个模块的API非常熟悉。

可以通过实现 :class:`unittest.TestCase` 的子类来完成创建测试用例。

.. code-block:: python

    import unittest

    def fun(x):
        return x + 1

    class MyTest(unittest.TestCase):
        def test(self):
            self.assertEqual(fun(3), 4)

Python 2.7 `标准库中的单元测试模块 <http://docs.python.org/library/unittest.html>`_ 包含自己的测试发现机制。 


文档测试
---------

:mod:`doctest` 模块会在文档字符串中搜索看起来像交互式Python会话的文本片段，然后执行这些会话，以确认是否可以如展示的那样工作。

文档测试与单元测试有着不同的使用情形：它们通常很少详细的描述，不会捕捉特殊的情况或者不明显的回归Bug。它们的主要用途是作为表述性文档来描述模块及其组成的主要部分。然而，每次完整运行测试套件时，文档测试也应当自动运行。

函数中简单的文档测试：

.. code-block:: python

    def square(x):
        """Return the square of x.

        >>> square(2)
        4
        >>> square(-2)
        4
        """

        return x * x

    if __name__ == '__main__':
        import doctest
        doctest.testmod()

当以 ``python module.py`` 方式在命令行中运行这个模块时，文档测试就会运行，并且，如果没有按照文档字符串中描述的行为执行，会发出提示。

工具
:::::


`py.test <http://pytest.org/latest/>`_
---------------------------------------

py.test是Python标准库中unittest模块的可选替代。

.. code-block:: console

    $ pip install pytest

尽管是一个特性齐全、可扩展的测试工具，但是它具有简单的语法。创建一个测试套件如同编写一个只包含有几个函数的模块一样简单：

.. code-block:: python

    # test_sample.py的内容
    def func(x):
        return x + 1

    def test_answer():
        assert func(3) == 5

然后运行 `py.test` 命令

.. code-block:: console

    $ py.test
    =========================== test session starts ============================
    platform darwin -- Python 2.7.1 -- pytest-2.2.1
    collecting ... collected 1 items

    test_sample.py F

    ================================= FAILURES =================================
    _______________________________ test_answer ________________________________

        def test_answer():
    >       assert func(3) == 5
    E       assert 4 == 5
    E        +  where 4 = func(3)

    test_sample.py:5: AssertionError
    ========================= 1 failed in 0.02 seconds =========================

与unittest模块相比，同样的功能，py.test需要更少的工作。


`Nose <http://readthedocs.org/docs/nose/en/latest/>`_
------------------------------------------------------

nose扩展了unittest来使得测试更加容易。


.. code-block:: console

    $ pip install nose

nose提供了自动发现测试集的功能，避免了人工创建测试套件的麻烦。同时也提供了大量的插件来支持兼容xUnit的测试输出、覆盖率报告以及测验选择等特性。

    `nose <https://nose.readthedocs.io/en/latest/>`_


`tox <http://testrun.org/tox/latest/>`_
-----------------------------------------

tox是一个管理自动测试所需环境以及配置多解释器测试的工具。

.. code-block:: console

    $ pip install tox

tox使用简单的ini格式配置文件，以便允许你配置复杂的多参数测试模型。 

    `tox <https://tox.readthedocs.io/en/latest/>`_


`Unittest2 <http://pypi.python.org/pypi/unittest2>`_
-----------------------------------------------------

unittest2是Python 2.7中unittest模块的移植，该模块拥有增强的API以及更好的断言，超越了之前Python中对应的模块。

如果你使用Python 2.6或者更低的版本，可以通过pip来安装：

.. code-block:: console

    $ pip install unittest2

可以采用unittest名自来引入该模块，这样，将来移植代码到模块的新版本时会更加容易。

.. code-block:: python

    import unittest2 as unittest

    class MyTest(unittest.TestCase):
        ...

采用这种方式，如果需要转换到新版本的Python，并且不再需要unittest2模块时，可以简单的在测试模块中修改引入部分，而不需要修改其他的代码。



`mock <http://www.voidspace.org.uk/python/mock/>`_
----------------------------------------------------

:mod:`unittest.mock` 是Python中用于测试的一个库。在Python 3.3中已经成为了 `标准库 <https://docs.python.org/dev/library/unittest.mock>`_ 的一部分。

对于旧版本的Python：

.. code-block:: console

    $ pip install mock

该库可以用模拟对象来替换待测试系统的一部分，你会从中知晓它们是如何被使用的。

例如，你可以给一个方法打猴子补丁：

.. code-block:: python

    from mock import MagicMock
    thing = ProductionClass()
    thing.method = MagicMock(return_value=3)
    thing.method(3, 4, 5, key='value')

    thing.method.assert_called_with(3, 4, 5, key='value')

使用 ``patch`` 装饰器在待测试的模块中模拟类或者对象。在下述示例中，采用总是返回相同结果（仅限于该测试期间）的模拟对象来替代外部搜索系统。

.. code-block:: python

    def mock_search(self):
        class MockSearchQuerySet(SearchQuerySet):
            def __iter__(self):
                return iter(["foo", "bar", "baz"])
        return MockSearchQuerySet()

    # 这里的SearchForm指的是myapp中导入的类引用，并不是SearchFrom本身被引入前的所在
    @mock.patch('myapp.SearchForm.search', mock_search)
    def test_new_watchlist_activities(self):
        # get_search_results进行搜索操作并对结果进行迭代
        self.assertEqual(len(myapp.get_search_results(q="fish")), 3)

Mock还有许多其他的配置方式来控制其行为。
