HTML页面爬取
=============

网页爬取
---------

网站采用HTML编写，这意味着每个网页都是一个结构化的文档。有时候我们往往需要从这些网页中获取一些数据，与此同时还要保留其结构。网站一般不会以合适的格式来提供他们的数据，比如采用 ``csv`` 或者 ``json`` 。

这时，网页爬取就派上了用场。网页爬取是一种采用电脑程序在网页上筛选并收集数据的行为，这些数据以对你最为有用的格式来保存，同时还保留了其结构。

lxml与Requests
-----------------

`lxml <http://lxml.de/>`_ 是一个用来快速解析XML和HTML文档且具有良好扩展性的库，甚至可以处理各种杂乱的标签。我们还会使用 `Requests <http://docs.python-requests.org/en/latest/>`_ 模块来替代内置的urllib2模块，以便提高速度和可读性。你可以很容易的使用命令 ``pip install lxml`` 和 ``pip install requests`` 来安装。

首先，导入这两个库：

.. code-block:: python

    from lxml import html
    import requests

接下来我们将使用 ``requests.get`` 来获取包含我们所需数据的网页，采用 ``html`` 模块来解析，并把结果保存在 ``tree`` 中。

.. code-block:: python

    page = requests.get('http://econpy.pythonanywhere.com/ex/001.html')
    tree = html.fromstring(page.content)

我们应该使用 ``page.content`` 而不是 ``page.text`` ，因为 ``html.fromstring`` 默认使用 ``bytes`` 来作为输入。

``tree`` 现在以良好的树状结构包含整个HTML文件，我们可以采用两种方式来遍历：XPath和CSSSelect。在这个示例中，我们主要介绍前一种。

XPath是一种在HTML或XML等结构化文档中定位信息的方式。 `W3Schools <http://www.w3schools.com/xsl/xpath_intro.asp>`_ 上有对XPath很好的介绍。

此外还有各种各样的工具来获取元素的XPath，比如Firefox中的FireBug或者Chrome中的Inspector。如果你正在使用Chrome，你可以右击元素，选择“检查”，高亮对应的代码，再次右击然后选择 "Copy -> Copy XPath"。

快速分析下面代码后，可以发现在我们的页面中，数据包含在两个元素之中 - 一个是title为"buyer-name"的div块，另外一个是class为"item-price"的span。

.. code-block:: html

    <div title="buyer-name">Carson Busses</div>
    <span class="item-price">$29.95</span>

知道这些后，我们可以构造一个正确的XPath查询，并且按下列方式使用lxml中的 ``xpath`` 函数：

.. code-block:: python

    # 此处会构造一个购买者的列表:
    buyers = tree.xpath('//div[@title="buyer-name"]/text()')
    # 此处会构造一个价格的列表：
    prices = tree.xpath('//span[@class="item-price"]/text()')

我们来看看得到的确切数据是什么：

.. code-block:: python

    print 'Buyers: ', buyers
    print 'Prices: ', prices

::

    Buyers:  ['Carson Busses', 'Earl E. Byrd', 'Patty Cakes',
    'Derri Anne Connecticut', 'Moe Dess', 'Leda Doggslife', 'Dan Druff',
    'Al Fresco', 'Ido Hoe', 'Howie Kisses', 'Len Lease', 'Phil Meup',
    'Ira Pent', 'Ben D. Rules', 'Ave Sectomy', 'Gary Shattire',
    'Bobbi Soks', 'Sheila Takya', 'Rose Tattoo', 'Moe Tell']

    Prices:  ['$29.95', '$8.37', '$15.26', '$19.25', '$19.25',
    '$13.99', '$31.57', '$8.49', '$14.47', '$15.86', '$11.11',
    '$15.98', '$16.27', '$7.50', '$50.85', '$14.26', '$5.68',
    '$15.00', '$114.07', '$10.09']

恭喜恭喜！我们已经成功的使用lxml和Requests从网页中爬取到了所有我们想要的数据。目前这些数据以两个列表的形式保存在内存中。这时候就可以在这些数据上做各种很酷的操作了：我们可以使用Python来分析这些数据或者把这些数据保存在一个文件中，然后分享给其他人。

可以想一些更加酷的idea，比如修改这个脚本来迭代处理网页剩下的部分，或者使用线程重写该应用来提高速度。
