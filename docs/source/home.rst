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

.. prompt:: bash $
    pip install djangorestframework
    pip install markdown       # Markdown support for the browsable API.
    pip install django-filter

将 ``rest_framework`` 添加到 ``INSTALLED_APPS`` 中

.. code-block:: python
    INSTALLED_APPS = [
        ...
        'rest_framework',
    ]

如果您打算使用可浏览 API，您可能还想添加 REST 框架的登录和注销视图。将以下内容添加到您的根 ``urls.py`` 文件中。（请注意，URL 路径可以是您想要的任何内容。）

.. code-block:: python
    urlpatterns = [
        ...
        path('api-auth/', include('rest_framework.urls'))
    ]


示例
++++++++++++

让我们看一下使用 REST 框架构建简单的模型支持 API 的快速示例。

我们将创建一个读写 API 来访问有关我们项目用户的信息。

``rest-framework api`` 的任何全局设置都保存在一个名为REST_FRAMEWORK. 首先将以下内容添加到您的 ``settings.py`` 模块中：

.. code-block:: python
    REST_FRAMEWORK = {
        # Use Django's standard `django.contrib.auth` permissions,
        # or allow read-only access for unauthenticated users.
        'DEFAULT_PERMISSION_CLASSES': [
            'rest_framework.permissions.DjangoModelPermissionsOrAnonReadOnly'
        ]
    }
不要忘记确保您还添加 ``rest_framework`` 到您的 ``INSTALLED_APPS`` 。

我们现在准备好创建我们的 ``API`` 。这是我们项目的根 ``urls.py`` 模块：

.. code-block:: python
    from django.urls import path, include
    from django.contrib.auth.models import User
    from rest_framework import routers, serializers, viewsets

    # Serializers define the API representation.
    class UserSerializer(serializers.HyperlinkedModelSerializer):
        class Meta:
            model = User
            fields = ['url', 'username', 'email', 'is_staff']

    # ViewSets define the view behavior.
    class UserViewSet(viewsets.ModelViewSet):
        queryset = User.objects.all()
        serializer_class = UserSerializer

    # Routers provide an easy way of automatically determining the URL conf.
    router = routers.DefaultRouter()
    router.register(r'users', UserViewSet)

    # Wire up our API using automatic URL routing.
    # Additionally, we include login URLs for the browsable API.
    urlpatterns = [
        path('', include(router.urls)),
        path('api-auth/', include('rest_framework.urls', namespace='rest_framework'))
    ]

您现在可以在浏览器中打开该 ``API`` ，网址为  `http://127.0.0.1:8000/ <http://127.0.0.1:8000/>`_ ，并查看您的新“用户” ``API`` 。如果您使用右上角的登录控件，您还可以在系统中添加、创建和删除用户。

快速开始
++++++++++++
等不及要开始了吗？该快速入门指南是启动和运行，并与REST框架构建的API的最快方式。

发展
++++++++++++
有关如何克隆存储库、运行测试套件并将更改贡献回 REST Framework 的信息，请参阅贡献指南。

支持
++++++++++++
如需支持，请参阅 ``rest-framework`` 讨论组，尝试 #restframework频道irc.libera.chat，或在 `Stack Overflow <https://stackoverflow.com/>`_ 上提出问题，确保包含 ``django-rest-framework`` 标签。

如需优先支持，请注册专业或高级赞助计划。

安全
++++++++++++
如果您认为自己在 ``Django REST framework`` 中发现了一些具有安全隐患的内容，请不要在公共论坛中提出该问题。
通过电子邮件将问题描述发送至 ``rest-framework-security@googlegroups.com`` 。然后，在任何公开披露之前，项目维护人员将与您合作解决任何需要的问题。

执照
++++++++++++
©2011至今，编码OSS有限公司。版权所有。
如果满足以下条件，则允许以源代码和二进制形式重新分发和使用，无论是否修改：
 * 源代码的重新分发必须保留上述版权声明、此条件列表和以下免责声明。
 * 以二进制形式重新分发必须在随分发提供的文档和/或其他材料中复制上述版权声明、此条件列表和以下免责声明。
 * 未经特别事先书面许可，不得使用版权所有者的姓名或其贡献者的姓名来认可或推广从该软件衍生的产品。

本软件由版权所有者和贡献者“按原样”提供，不提供任何明示或暗示的保证，包括但不限于适销性和特定用途适用性的暗示保证。 在任何情况下，版权所有者或贡献者均不对任何直接、间接、偶然、特殊、惩戒性或后果性损害（包括但不限于替代商品或服务的采购；使用、数据或利润的损失； 或业务中断），无论是因使用本软件而以任何方式引起的，并且根据任何责任理论，无论是合同、严格责任或侵权（包括疏忽或其他），即使已被告知可能发生此类损害。