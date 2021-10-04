欢迎来到 Django-rest-framework 中文翻译
===================================

本项目是 `Django-rest-framework <https://www.django-rest-framework.org/>`_ 中文翻译版本.

Django REST framework 是一个强大且灵活的工具包，用于构建 Web API。

您可能想要使用 REST 框架的一些原因：

    1. 该 `网站可浏览API <https://restframework.herokuapp.com/>`_ 是你的开发人员一个巨大的可用性胜利。
    2. 身份验证策略，包括OAuth1a和OAuth2 的包 :doc:`/api/authentication` 。
    3. 支持ORM和非ORM数据源的序列化。
    4. 可自定义，如果您不需要更强大的功能，只需使用常规的基于功能的视图。
    5. 广泛的文档和强大的社区支持。
    6. 得到国际知名公司的使用和信任，包括Mozilla、Red Hat、Heroku和Eventbrite。


依赖环境
++++++++++++
    * Python（3.5、3.6、3.7、3.8、3.9）
    * Django (2.2, 3.0, 3.1, 3.2)

我们强烈推荐并且只正式支持每个 Python 和 Django 系列的最新补丁版本。

以下软件包是可选的：

    * PyYAML , uritemplate (5.1+, 3.0.0+) - 模式生成支持。
    * Markdown (3.0.0+) - 对可浏览 API 的 Markdown 支持。
    * Pygments (2.4.0+) - 为 Markdown 处理添加语法高亮。
    * django-filter (1.0.1+) - 过滤支持。
    * django-guardian (1.1.1+) - 对象级权限支持。

.. note::

   还有一些，译者平时工作中常用的第三方包：``django-redis`` （redis支持；在 ``Django4.0`` 之后，会提供内置的Redis的支持）、 ``django-cors-headers`` （跨域支持）等


安装
++++++++++++
使用 ``pip`` 安装

    pip install djangorestframework
    pip install markdown       # Markdown support for the browsable API.
    pip install django-filter

将 ``rest_framework`` 添加到 ``INSTALLED_APPS`` 中

    INSTALLED_APPS = [
        ...
        'rest_framework',
    ]

如果您打算使用可浏览 API，您可能还想添加 REST 框架的登录和注销视图。将以下内容添加到您的根 ``urls.py`` 文件中。（请注意，URL 路径可以是您想要的任何内容。）

    urlpatterns = [
        ...
        path('api-auth/', include('rest_framework.urls'))
    ]


