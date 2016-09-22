================
Web应用
================

作为一种适用于快速原型以及大型项目的强大脚本语言，Python在Web应用开发中被广泛使用。


上下文环境
:::::::::::


WSGI
----

Web服务器网关接口（缩写为“WSGI”）是Python web应用框架与web服务器交互的标准接口。通过标准化Python web框架与web服务器之间的行为和交互，WSGI使得编写可部署于任何 :ref:`WSGI兼容服务器 <wsgi-servers-ref>` 上的可移植性Python代码变成了可能。WSGI的相关文档见 :pep:`3333` 。


框架
::::::::::

大体上来说，web框架包含了各种库的集合，以及用于定制代码实现web应用（比如一个交互式的web站点）的主处理器。大部分的web框架包含了各种模式以及工具来实现以下几点：

URL路由
  匹配到来的HTTP请求到特定的Python代码来执行相应逻辑

请求响应对象
  对接收自或发送给用户浏览器的信息进行包装

模板引擎
  用于分离实现应用逻辑的Python代码和产生的HTML（或其他形式）输出

开发时使用的web服务器
  在开发机上运行HTTP服务器可以进行快速开发；当文件更新时，通常会自动重载服务端代码。


Django
------

`Django <http://www.djangoproject.com>`_ 是一个“内置电池”的web应用框架，对于创建面向内容的站点来说是一个极好的选择。通过提供大量开箱即用的工具和模式，Django旨在鼓励以最佳实践方式编写代码的同时，可以快速构建复杂的、数据库驱动的web应用。

Django有着一个活跃的大型社区，有许多预先构建好的 `可复用模块 <http://djangopackages.com/>`_ 可以用来构建新的项目，抑或通过定制来达到你的要求。

在 `美国 <http://djangocon.us>`_ 和 `欧洲 <http://djangocon.eu>`_ 每年都有Django的会议。

当今大多数新的Python web应用都是使用Django来构建的。


Flask
-----

`Flask <http://flask.pocoo.org/>`_ 是Python中的一个 “微框架”，对于构建小型的应用、API或者web服务，这是一个极好的选择。

使用Flask构建应用在很大程度上就和编写标准Python模块差不多，除了要绑定路由到一些函数之上。这种方式棒极了。

Flask并没有向你提供可能会用到的所有功能，而是实现了web应用框架中大部分常用的核心组件，比如URL路由、请求响应对象和模板。

如果采用Flask，你可以根据自己爱好来为你的应用选择其他任何组件。比如，Flask并没有内建数据库访问或者表单的生成与验证。

这样做其实很好，因为很多web应用并不需要这些特性。对于那些需要这些特性的项目而言，有许多 `扩展 <http://flask.pocoo.org/extensions/>`_ 可以满足你的需求。又或者你可以使用任何你想用的库！

对于那些不太适用Django的Python web应用来说，Flask是默认的选择。


Tornado
--------

`Tornado <http://www.tornadoweb.org/>`_ 是Python中的一个异步web框架，有着自己的事件循环，这使得其本身可以支持WebSockets。优秀的tornado应用以性能卓越而著称。

我不太建议使用Tornado，除非你认为非用不可。

Pyramid
--------

`Pyramid <https://trypyramid.com/>`_ 是一个聚焦于模块化、极具伸缩性的框架。框架本身内建有少量的库（“电池”），并鼓励用户扩展这些基础功能。

不像Django和Flask，Pyramid用户基础并不大。本身是一个功能很强大的框架，但是对于如今新的Python web应用来说并不是一个流行的选择。


Web服务器
:::::::::::

.. _nginx-ref:

Nginx
-----

`Nginx <http://nginx.org/>`_ （发音 "engine-x"）是一个web服务器以及HTTP、SMTP和其他协议的反向代理。以高性能、相对简单及和许多应用服务器的（如WSGI服务器）兼容性著称。它包含有大把的特性，比如负载均衡、基本认证、流处理以及其他特性。Nginx设计用以服务于高负载的站点，正在逐渐变得越来越流行。


.. _wsgi-servers-ref:

WSGI服务器
::::::::::::

独立的WSGI服务器往往比传统的web服务器使用更少的资源，并且提供更高的性能 [3]_ 。

.. _gunicorn-ref:

Gunicorn
--------

`Gunicorn <http://gunicorn.org/>`_ （Green Unicorn）是一个用来驱动Python应用的WSGI服务器，纯Python实现。与其他Python web服务器不同，它有着非常体贴的接口，并且非常易用和配置。

Gunicorn有着很明智合理的默认配置。然而，一些其他服务器，例如uWSGI，虽然有着惊人的可定制性，但也因此变得更加难以高效使用。

对于如今新的Python web应用而言，Gunicorn是更加推荐的选择。


Waitress
--------

`Waitress <https://waitress.readthedocs.io>`_ 也是一个纯Python的WSGI服务器，声称有着“非常可接受的性能”。其文档并不太详细，但是确实提供了一些Gunicorn没有提供的优秀功能（如HTTP请求缓冲）。

Waitress在Python web开发社区正在变得越来越流行。

.. _uwsgi-ref:

uWSGI
-----

`uWSGI <https://uwsgi-docs.readthedocs.io>`_ 为构建托管服务提供了全栈的功能。除了进程管理、进程监控以及其他功能，uWSGI还可以作为多种编程语言和协议的应用服务器 - 当然包括Python和WSGI。uWSGI既可以作为独立的web路由器来运行，也可以运行在全功能的web服务器（比如Nginx和Apache）后端。后一种情况下，web服务器可以配置uWSGI与应用之间采用 `uwsgi协议 <https://uwsgi-docs.readthedocs.io/en/latest/Protocol.html>`_ 来通信。uWSGI的web服务器支持通过传递环境变量和进一步的调整来动态配置Python。更详细的信息，参见 `uWSGI魔法变量 <https://uwsgi-docs.readthedocs.io/en/latest/Vars.html>`_ 。

我不建议使用uWSGI，除非你知道为什么需要使用。

.. _server-best-practices-ref:


服务端最佳实践
:::::::::::::::::::::

当前主流部署Python应用的方式主要是采用如 :ref:`Gunicorn <gunicorn-ref>` 的WSGI服务器，然后直接或间接的放置在轻量级web服务器，如 :ref:`nginx <nginx-ref>` 后面。

WSGI服务器主要是用于Python应用的处理，与此同时，web服务器则处理更适合它的任务，比如静态文件服务、请求路由、DDoS保护以及基本认证。


托管部署
:::::::::

平台即服务（PaaS）是一种云计算基础设施的类型，会抽象并管理基础设施、路由以及web应用的扩展。使用PaaS时，应用开发者可以聚焦于编写应用代码而不用关心部署的细节。


Heroku
------

`Heroku <http://www.heroku.com/python>`_ 对Python 2.7-3.5 应用提供了第一流的支持。

Heroku支持所有类型的Python web应用、服务器以及框架。可以在Heroku上免费的开发应用。一旦应用可以用于生产，你可以升级到兴趣或专业应用。

Heroku维护了 `详细的文章 <https://devcenter.heroku.com/categories/python>`_ 来说明如何在Heroku上使用Python，同时也有一份 `手把手指南 <https://devcenter.heroku.com/articles/getting-started-with-python>`_ 来帮助设置你的第一个应用。

Heroku是当前比较推荐的用于部署Python web应用的PaaS。


Gondor
------

`Gondor <https://gondor.io/>`_ 是一个专用于Django和Pinax应用的PaaS。Gondor建议的Django版本是1.6，并且支持Python 2.7上的WSGI应用。如果使用 :file:`local_settings.py` 来存储站点特有配置信息，Gondor可以自动的配置你的Django站点。

Gondor有一份指南说明如何部署 `Django项目 <https://gondor.io/support/django/setup/>`_ 。

Gondor是由一家小型公司运营的，聚焦于帮助企业成功部署Python和Django。


模板
::::::::::

大多数WSGI应用会以HTML或其他标记语言作为HTTP请求的响应。关注点分离的概念建议我们采用模板，而不是直接从Python中产生文本内容。模板引擎管理着一系列的模板文件，采用层次系统和包含系统来避免不必要的重复，并负责渲染（生成）实际的内容，利用应用产生的动态内容来填充模板的静态内容。

由于模板文件有时会由设计人员或者前端开发者来编写，因此处理起不断增长的复杂性会很困难。

对于如何把应用中的动态内容传递给模板引擎和模板本身，有一些通用且好的实践可供参考：

- 应当只把渲染时必要的动态内容传递给模板文件。避免传递额外的内容“以防万一”：添加缺失的变量远比移除一个不用的变量要容易。

- 许多模板引擎允许在模板中使用复杂的语句或赋值，并且还允许在模板中调用Python代码。这种便捷会导致复杂性的不可控，进而使得很难找到bug。

- 通常情况下需要把Javascript模板与HTML模板混合。对于这种设计来说，一个明智的方式是把需要由HTML模板传递变量内容到JavaScript代码的部分隔离。。



Jinja2
------
`Jinja2 <http://jinja.pocoo.org/>`_ 是一个得到普遍好评的模板引擎。

它采用基于文本的模板语言，这样就可以用于生成任何类型的标记语言，不仅仅是HTML。Jinja2允许定制过滤器、标签、测试以及全局内容。相比于Django的模板系统，Jinja2有许多的改进。

这里是Jinja2中一些重要的HTML标签：

.. code-block:: html

    {# 这是注释 #}

    {# 下一个标签是变量输出 #}
    {{title}}

    {# 块标签，通过继承可以被其他html代码替换 #}
    {% block head %}
    <h1>This is the head!</h1>
    {% endblock %}

    {# 迭代输出数组 #}
    {% for item in list %}
    <li>{{ item }}</li>
    {% endfor %}


接下来的代码清单是一个与Tornado服务器结合的web站点示例。Tornado使用起来并不复杂。


.. code-block:: python

    # 导入Jinja2
    from jinja2 import Environment, FileSystemLoader

    # 导入Tornado
    import tornado.ioloop
    import tornado.web

    # 载入模板文件 templates/site.html
    TEMPLATE_FILE = "site.html"
    templateLoader = FileSystemLoader( searchpath="templates/" )
    templateEnv = Environment( loader=templateLoader )
    template = templateEnv.get_template(TEMPLATE_FILE)

    # 用于渲染的著名电影列表
    movie_list = [[1,"The Hitchhiker's Guide to the Galaxy"],[2,"Back to future"],[3,"Matrix"]]

    # template.render() 返回包含有渲染后html的字符串
    html_output = template.render(list=movie_list,
                            title="Here is my favorite movie list")

    # 主页的处理器
    class MainHandler(tornado.web.RequestHandler):
        def get(self):
            # 返回渲染后的模板字符串到浏览器
            self.write(html_output)

    # 设定路由  (127.0.0.1:PORT/)
    application = tornado.web.Application([
        (r"/", MainHandler),
    ])
    PORT=8884
    if __name__ == "__main__":
        # 设置服务器
        application.listen(PORT)
        tornado.ioloop.IOLoop.instance().start()

:file:`base.html` 文件可以作为所有站点页面的基础，这些站点页面实现其中的内容块即可。

.. code-block:: html

    <!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN">
    <html lang="en">
    <html xmlns="http://www.w3.org/1999/xhtml">
    <head>
        <link rel="stylesheet" href="style.css" />
        <title>{{title}} - My Webpage</title>
    </head>
    <body>
    <div id="content">
        {# 下一行会由site.html模板中的内容填充 #}
        {% block content %}{% endblock %}
    </div>
    <div id="footer">
        {% block footer %}
        &copy; Copyright 2013 by <a href="http://domain.invalid/">you</a>.
        {% endblock %}
    </div>
    </body>


下一代码清单是我们Python应用载入的的站点页面（ :file:`site.html` ），该页面扩展了 :file:`base.html` 。内容块会自动嵌入到 :file:`base.html` 页面对应的块中。

.. code-block:: html

    <!{% extends "base.html" %}
    {% block content %}
        <p class="important">
        <div id="content">
            <h2>{{title}}</h2>
            <p>{{ list_title }}</p>
            <ul>
                 {% for item in list %}
                 <li>{{ item[0]}} :  {{ item[1]}}</li>
                 {% endfor %}
            </ul>
        </div>
        </p>
    {% endblock %}


对于新的Python web应用，Jinja2是比较推荐的模板库。


Chameleon
---------

`Chameleon <https://chameleon.readthedocs.io/>`_ 页面模板是一个HTML/XML模板引擎，该引擎实现了 `模板属性语言 (TAL) <http://en.wikipedia.org/wiki/Template_Attribute_Language>`_ 、 `TAL表达式语法 (TALES) <https://chameleon.readthedocs.io/en/latest/reference.html#expressions-tales>`_ 和 `宏扩展TAL (Metal) <https://chameleon.readthedocs.io/en/latest/reference.html#macros-metal>`_ 语法。

Chameleon可用于Python 2.5及以上版本（包括3.x和pypy），常用于 `Pyramid框架 <http://trypyramid.com>`_ 。

页面模板会在你的文档结构中添加特殊的元素属性和文本标记。通过使用一组简单的语言构造，你可以控制文档流、元素的重复、文本的替换和转化。由于是基于属性的语法，未渲染的页面模板是合法的HTML，所以可以在浏览器中查看，也可以在WYSIWYG的编辑器中编辑。这使得与设计师来回的协作，以及在浏览器中使用静态文件构建原型变得更加容易。

基本的TAL语言可以很容易的从下面的例子中了解：

.. code-block:: html

  <html>
    <body>
    <h1>Hello, <span tal:replace="context.name">World</span>!</h1>
      <table>
        <tr tal:repeat="row 'apple', 'banana', 'pineapple'">
          <td tal:repeat="col 'juice', 'muffin', 'pie'">
             <span tal:replace="row.capitalize()" /> <span tal:replace="col" />
          </td>
        </tr>
      </table>
    </body>
  </html>


`<span tal:replace="expression" />` 是插入文本的模式，它是如此常见，以至于当你不需要保证未渲染的模板严格合法时，你可以使用更加简短可读的语法来替换，即 `${expression}` ，具体如下：

.. code-block:: html

  <html>
    <body>
      <h1>Hello, ${world}!</h1>
      <table>
        <tr tal:repeat="row 'apple', 'banana', 'pineapple'">
          <td tal:repeat="col 'juice', 'muffin', 'pie'">
             ${row.capitalize()} ${col}
          </td>
        </tr>
      </table>
    </body>
  </html>


但是请记住完整的 `<span tal:replace="expression">Default Text</span>` 语法还允许在未渲染的模板中包含默认内容。

由于Chameleon来自Pyramid世界，所以并未广泛使用。

Mako
----

`Mako <http://www.makotemplates.org/>`_ 是一种会编译为Python的模板语言，以达到性能最大化。它的语法和API借鉴于其他模板语言（比如Django和Jinja2）最好的部分，它是 `Pylons and Pyramid <http://www.pylonsproject.org/>`_ web框架包含的默认模板语言。

Mako模板示例如下：

.. code-block:: html

    <%inherit file="base.html"/>
    <%
        rows = [[v for v in range(0,10)] for row in range(0,10)]
    %>
    <table>
        % for row in rows:
            ${makerow(row)}
        % endfor
    </table>

    <%def name="makerow(row)">
        <tr>
        % for name in row:
            <td>${name}</td>\
        % endfor
        </tr>
    </%def>


要想渲染一个最基本的模板，你可以这样做：

.. code-block:: python

    from mako.template import Template
    print(Template("hello ${data}!").render(data="world"))

在Python web社区，Mako备受推崇。

.. rubric:: 参考

.. [1] `mod_python项目已死 <http://blog.dscpl.com.au/2010/06/modpython-project-is-now-officially.html>`_
.. [2] `mod_wsgi vs mod_python <http://www.modpython.org/pipermail/mod_python/2007-July/024080.html>`_
.. [3] `Python WSGI服务器基准测试 <http://nichol.as/benchmark-of-python-web-servers>`_
