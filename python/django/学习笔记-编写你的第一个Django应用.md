
[官方教程](https://docs.djangoproject.com/zh-hans/2.2/intro)

## 第 1 部分  创建项目

通过这个教程，我们将带着你创建一个基本的投票应用程序。

它将由两部分组成：

- 一个让人们查看和投票的公共站点。
- 一个让你能添加、修改和删除投票的管理站点。(网站后台)

创建项目命令
```
...\> django-admin startproject mysite
```

开启服务器
```
...\> py manage.py runserver
```

创建投票应用
```
...\> py manage.py startapp polls
```

项目目录结构
```
mysite/
    manage.py
    mysite/
        __init__.py
        settings.py
        urls.py
        wsgi.py
    polls/
        __init__.py
        admin.py
        apps.py
        migrations/
            __init__.py
        models.py
        tests.py
        urls.py
        views.py
```

## 第 2 部分 开始使用数据库

一般是先写model，然后去创建迁徙数据库，步骤如下：

- 编辑 `models.py` 文件，改变模型。
- 运行 `python manage.py makemigrations` 为模型的改变生成迁移文件。
- 运行 `python manage.py migrate` 来应用数据库迁移。

django自带数据库API和后台管理系统。

## 第 3 部分 为投票应用添加更多视图

## 第 4 部分 了解简单的表单处理和通用视图。

## 第 5 部分 解如何测试我们的投票应用

真正不同的地方在于，自动化 测试是由某个系统帮你自动完成的。当你创建好了一系列测试，每次修改应用代码后，就可以自动检查出修改后的代码是否还像你曾经预期的那样正常工作。你不需要花费大量时间来进行手动测试。

`测试驱动`一般是先写测试后写代码。当然你可以根据自己的喜好是选择在写代码前还是写代码后进行编写测试。

当需要测试的时候，测试用例越多越好。

如果你对测试有个整体规划，那么它们就几乎不会变得混乱。下面有几条好的建议：

- 对于每个模型和视图都建立单独的 TestClass
- 每个测试方法只测试一个功能
- 给每个测试方法起个能描述其功能的名字

## 第 6 部分 学习静态文件管理的相关知识

## 第 7 部分 如何自定义 Django 自动生成后台网页的过程

## 接下来要做什么？
初学者教程到这就结束了。随后，你可能想阅读 [下一步看什么](https://docs.djangoproject.com/zh-hans/2.2/intro/whatsnext/)，看看下一步能做什么。

如果你很熟悉 Python 打包，且对学习如何把投票应用改成“可复用应用”感兴趣，查看 [进阶教程：如何创建可复用应用](https://docs.djangoproject.com/zh-hans/2.2/intro/reusable-apps/)。