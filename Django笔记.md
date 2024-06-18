# Django基本原理

Django项目本质上是各种应用程序的集合,每一个都提供一定的功能

### 1. Django简介
- Django是一个基于Python的开发框架，用于构建Web应用程序。
- 由MTV模式（模型，模板，视图）驱动。

### 2. 安装Django
```bash
pip install django
```

### 3. 创建Django项目和应用
- 创建项目：`django-admin startproject projectname`
- 创建应用：`python manage.py startapp appname`

### 4. MVC vs MTV
- MTV：模型（Model），模板（Template），视图（View）
- 模型：定义数据模型
- 模板：定义用户界面
- 视图：处理业务逻辑

### 5. 数据模型
- 使用模型类定义数据结构
- 迁移数据库：`python manage.py makemigrations` 和 `python manage.py migrate`

### 6. 视图
- 处理用户请求和业务逻辑
- 类型：函数视图和类视图

### 7. 路由
- 定义URL模式，将URL映射到视图
- 在应用中的`urls.py`中配置路由

### 8. 模板
- 使用HTML和Django模板语言构建用户界面
- 模板继承和包含

### 9. 表单
- 使用Django表单处理用户输入
- 内置表单和自定义表单

### 10. 静态文件
- 存储CSS，JavaScript等静态文件
- 在模板中使用 `{% static %}` 标签引用静态文件

### 11. 用户认证
- 使用Django内置的用户认证系统
- 注册、登录、注销功能

### 12. 中间件
- Django中的中间件处理请求和响应
- 内置和自定义中间件

### 13. Django管理后台
- 使用Django自动生成的管理后台进行数据管理
- 自定义管理后台界面和功能

### 14. 测试
- 编写和运行单元测试
- 使用Django的测试工具

### 15. 部署
- 部署Django应用到生产环境
- 使用WSGI服务器（如Gunicorn）、数据库（如PostgreSQL）、静态文件服务等

这些笔记覆盖了Django的基础概念和常见任务。在学习的过程中，你可能还会遇到其他特定的需求和概念，根据需要进行深入学习。祝你学习愉快！

## 创建Django项目

创建Django项目时，生成的文件和目录通常包括：

1. **`manage.py`:**
   - **作用：** Django 项目的命令行工具。
   - **解释：** 通过 `manage.py` 可以执行多种 Django 管理命令，如启动开发服务器、创建数据库迁移、创建超级用户等。

2. **项目目录：**
   - **作用：** 包含整个 Django 项目的主要文件和配置。
   - **解释：** 项目目录的名称是你在创建项目时指定的，其中包含了一系列配置文件、应用程序目录和其他项目级别的文件。

3. **`settings.py`:**
   - **作用：** 配置 Django 项目的设置。
   - **解释：** 包含了项目的各种配置选项，如数据库设置、静态文件路径、应用程序列表等。

4. **`urls.py`:**
   - **作用：** 定义 Django 项目的 **URL 映射**。**在Django中，URL映射（URL mapping）是指将特定的URL请求映射到相应的视图函数或处理程序的过程。当用户在浏览器中输入一个URL时，Django需要知道如何处理该请求，这就是通过URL映射来实现的。**
   - **解释：** 通过 `urls.py` 文件，你可以配置项目中 URL 路由，将不同的 URL 映射到对应的视图函数。

5. **`wsgi.py`:**
   - **作用：** 提供项目的 WSGI 入口。
   - **解释：** WSGI（Web Server Gateway Interface）是一种协议，用于将 web 服务器和 Django 项目连接起来。`wsgi.py` 提供了一个 WSGI 入口点。 

6. **`asgi.py`:**
   - **作用：** 提供项目的 ASGI 入口。
   - **解释：** ASGI（Asynchronous Server Gateway Interface）是一种异步 web 服务器连接协议，用于支持异步请求处理。`asgi.py` 提供了一个 ASGI 入口点。

7. **`__init__.py`:**
   - **作用：** 将项目目录标识为 Python 包。
   - **解释：** 这个文件的存在告诉 Python 解释器将该目录视为一个包，可以在其中导入模块。

8. **`migrations/` 目录:**
   - **作用：** 存储数据库迁移文件。
   - **解释：** Django 的迁移系统用于跟踪和应用数据库模型的更改。`migrations/` 目录包含由 `makemigrations` 命令生成的迁移文件。

9. **`static/` 目录:**
   - **作用：** 存储项目中使用的静态文件。
   - **解释：** 静态文件，如样式表、JavaScript 文件和图像等，可以存储在 `static/` 目录中。

10. **`templates/` 目录:**
    - **作用：** 存储项目中使用的 HTML 模板文件。
    - **解释：** Django 使用模板引擎来生成 HTML 页面，`templates/` 目录用于存储这些模板文件。

这些文件和目录组成了一个基本的Django项目结构，每个都有特定的作用，用于组织和管理项目的不同方面。在实际项目中，你还可能会创建和使用其他目录和文件，具体取决于项目的需求和架构。

## 创建Django应用程序

当你在 Django 项目中创建一个应用程序时，Django 自动生成的应用程序文件夹包含一些主要文件和目录，每个都有特定的作用。以下是这些文件和目录的解释：

1. **`migrations` 文	件夹:**
   - **作用：** 存储数据库迁移文件。
   - **解释：** Django 中的迁移系统用于跟踪数据库模型的更改，并将这些更改应用到数据库。`migrations` 文件夹包含由 `makemigrations` 命令生成的迁移文件。

2. **`__init__.py`:**
   - **作用：** 表示该目录是一个 Python 包。
   - **解释：** 这个文件的存在告诉 Python 解释器将该目录视为一个包，允许你在这个目录中导入模块。

3. **`admin.py`:**
   - **作用：** 用于配置 Django 的后台管理系统。
   - **解释：** 在这个文件中，你可以注册模型以便在 Django 的后台管理界面中进行管理。你可以定义显示在后台的模型字段、过滤器和搜索字段等。

4. **`apps.py`:**
   - **作用：** 用于配置应用程序的元数据。
   - **解释：** 这个文件包含有关应用程序的元数据，如应用程序的名称、标签和其他配置。通常情况下，你不需要经常修改这个文件。

5. **`models.py`:**
   - **作用：** 用于定义应用程序的数据模型。
   - **解释：** 在这个文件中，你可以定义数据库中的表结构，以及与这些表相关的操作。Django 的模型是一种用于定义数据结构的强大工具。

6. **`tests.py`:**
   - **作用：** 存储应用程序的测试代码。
   - **解释：** 在这个文件中，你可以编写用于测试应用程序的单元测试和集成测试。Django 提供了强大的测试框架，用于确保应用程序的正确性。

7. **`views.py`:**
   - **作用：** 存储应用程序的视图函数。
   - **解释：** 在这个文件中，你可以定义处理 HTTP 请求并生成 HTTP 响应的视图函数。视图负责处理用户请求，执行逻辑，然后返回相应的响应。

这些文件和目录组成了一个典型的 Django 应用程序的结构，帮助你组织和管理应用程序的不同部分。

### 视图函数

在Django中，视图函数（View Function）是处理Web应用程序中HTTP请求的Python函数。视图函数负责接收HTTP请求并返回HTTP响应，决定了在用户访问特定URL时应该显示什么内容。

一个简单的Django视图函数通常接收一个HTTP请求作为输入参数，执行一些处理逻辑（可能涉及数据库查询、业务逻辑等），然后返回一个HTTP响应。Django的视图函数是MVC（Model-View-Controller）架构中的"视图"部分，负责呈现用户界面。

下面是一个简单的Django视图函数的示例：

```python
from django.http import HttpResponse

def hello_world(request):
    # 处理逻辑，可以进行数据库查询等操作
    response_text = "Hello, World!"
    
    # 返回HTTP响应
    return HttpResponse(response_text)
```

在这个例子中，`hello_world` 是一个简单的视图函数。当用户访问与该函数关联的URL时，Django将调用该函数并返回其返回的HTTP响应。

Django的URL配置（通常在`urls.py`文件中定义）将URL与视图函数进行关联，告诉Django在用户访问特定URL时应该调用哪个视图函数。例如：

```python
from django.urls import path
from .views import hello_world

urlpatterns = [
    path('hello/', hello_world, name='hello_world'),
]
```

在这个 Django 项目中，`urlpatterns` 是一个列表，其中包含了定义项目URL模式的规则。每个规则都由 `path` 函数定义，指定了一个URL模式与相应的视图函数的关联关系。

1. **`path('hello/', hello_world, name='hello_world')`:**
   - **作用：** 定义一个URL模式，将URL路径 '/hello/' 映射到 `hello_world` 视图函数。
   - 解释：
     - `'hello/'`: 是URL路径模式，表示当用户访问以'/hello/'结尾的URL时，该规则将匹配。
     - `hello_world`: 是与该URL模式匹配时要调用的视图函数。
     - `name='hello_world'`: 是为该URL模式指定的名称，可以在Django模板中使用，也可以在代码中用于生成URL。
2. **`urlpatterns = [...]`:**
   - **作用：** 定义了项目中所有URL模式的列表。
   - **解释：** `urlpatterns` 是一个列表，其中包含了项目中所有的URL规则。每个规则由 `path` 函数定义，并指定了URL路径、与之关联的视图函数以及可选的规则名称。

这样，当用户访问项目中的URL `/hello/` 时，Django将调用 `hello_world` 视图函数来处理请求。这个 URL 模式的定义是一种将特定路径映射到相应处理逻辑的方式。

## 1.ulr映射视图函数例子

你的Django项目结构和代码清晰明了，下面是对你的代码的简要总结：

### 主 `urls.py`:

```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('playground/', include('playground.urls'))
]
```

- `path('admin/', admin.site.urls)`: 将 `admin` 应用程序的 URL 配置包含在主 URL 配置中，使得可以通过 `/admin/` 访问 Django 管理后台。

- `path('playground/', include('playground.urls'))`: 将 `playground` 应用程序的 URL 配置包含在主 URL 配置中，使得可以通过 `/playground/` 访问 `playground` 应用程序的功能。

### `playground` 应用程序的 `urls.py`:

```python
from django.urls import path
from . import views

urlpatterns = [
    path('hello/', views.say_hello)
]
```

- `path('hello/', views.say_hello)`: 定义了一个 URL 规则，当用户访问 `/playground/hello/` 时，Django 将调用 `views.say_hello` 处理该请求。

### `playground` 应用程序的 `views.py`:

```python
from django.shortcuts import render
from django.http import HttpResponse

def say_hello(response):
    return HttpResponse("Hello World!")
```

- `say_hello` 视图函数：处理 `/playground/hello/` 路径的请求，返回一个包含 "Hello World!" 的 HTTP 响应。

总体来说，你的Django项目遵循了典型的Django应用程序结构，使得代码模块化、清晰可读。通过这样的组织方式，你可以轻松添加和管理不同应用程序的功能，并确保项目的可扩展性和可维护性。

## 2.模板例子

下面代码在views.py中，

```
from django.shortcuts import render
from django.http import HttpResponse


def say_hello(request):
    return render(request,'hello.html')
```

这段代码定义了一个Django视图函数，该函数名为 `say_hello`。以下是对这段代码的简要解释：

1. **导入必要的模块：**
   - `from django.shortcuts import render`: 导入 Django 提供的用于渲染模板的 `render` 函数。
   - `from django.http import HttpResponse`: 导入 Django 提供的用于创建 HTTP 响应的 `HttpResponse` 类。

2. **定义视图函数：**
   - `def say_hello(request):`: 定义了一个名为 `say_hello` 的视图函数，接受一个 `request` 参数，即 Django 的请求对象。

3. **返回渲染后的模板：**
   - `return render(request, 'hello.html')`: 使用 `render` 函数渲染名为 `hello.html` 的模板，并将渲染后的内容作为 HTTP 响应返回给客户端。

4. **模板文件 `hello.html`：**
   - 这个模板文件应该位于Django项目中的某个 `templates` 目录下，并包含用于显示 "Hello World!" 的HTML代码。

翻译为简单的语言：这个代码定义了一个视图函数，当用户访问与该视图关联的URL时，它渲染了一个名为 `hello.html` 的模板，并将渲染后的内容作为响应返回给用户。在模板中，可能有一些HTML代码，用于显示 "Hello World!" 或其他内容。

## 3.Django Views 和 模板例子

#### `views.py` 代码：

```python
from django.shortcuts import render
from django.http import HttpResponse

def say_hello(request):
    return render(request, 'hello.html', {'name': 'Mosh'})
```

#### `hello.html` 模板文件：

```html
{% if name %}
    <h1>Hello {{ name }}</h1>
{% else %}
    <h1>Hello World</h1>
{% endif %}
```

#### 笔记总结：

1. **`views.py` 中的 `say_hello` 视图函数：**
   - 使用 `render` 函数渲染了名为 `hello.html` 的模板。
   - 传递了一个包含 `'name': 'Mosh'` 的上下文字典，将变量 `name` 传递给模板。

2. **`hello.html` 模板文件：**
   - 使用 Django 模板语法，通过 `{% if name %}` 条件语句检查 `name` 是否存在。
   - 如果 `name` 存在，则显示 `<h1>Hello {{ name }}</h1>`，否则显示 `<h1>Hello World</h1>`。

3. **模板语法解释：**
   - `{% if name %}`: 检查变量 `name` 是否存在。
   - `<h1>Hello {{ name }}</h1>`: 如果 `name` 存在，显示 `Hello` 后跟变量 `name` 的值。
   - `<h1>Hello World</h1>`: 如果 `name` 不存在，显示默认的 `Hello World`。

4. **上下文数据传递：**
   - 通过在视图中使用 `render` 函数的第三个参数，将 `'name': 'Mosh'` 这个字典传递给模板，使得模板能够访问和显示这个数据。

通过这个简单的例子，你学会了在Django中如何创建视图函数、渲染模板以及在模板中使用条件语句展示不同的内容。

# 储存和检索数据的模型

## 定义模型的属性字段类型

在 Django 中，你可以使用不同的字段类型来定义模型的属性。以下是一些常用的字段类型：

1. **`CharField`：**
   - 用于存储短文本字符串，例如标题或姓名。
   - 示例：`name = models.CharField(max_length=100)`

2. **`TextField`：**
   - 用于存储较长的文本字符串，例如文章内容。
   - 示例：`content = models.TextField()`

3. **`IntegerField`：**
   - 用于存储整数。
   - 示例：`quantity = models.IntegerField()`

4. **`DecimalField`：**
   - 用于存储十进制数，通常用于货币或其他需要高精度的数值。
   - 示例：`price = models.DecimalField(max_digits=5, decimal_places=2)`

5. **`DateField`：**
   - 用于存储日期。
   - 示例：`date_published = models.DateField()`

6. **`DateTimeField`：**
   - 用于存储日期和时间。
   - 示例：`last_updated = models.DateTimeField(auto_now=True)`

7. **`BooleanField`：**
   - 用于存储布尔值（True 或 False）。
   - 示例：`is_published = models.BooleanField(default=True)`

8. **`EmailField`：**
   - 用于存储电子邮件地址。
   - 示例：`email = models.EmailField()`

9. **`ImageField`：**
   - 用于存储图片文件的路径。
   - 示例：`profile_picture = models.ImageField(upload_to='profile_pics/')`

10. **`ForeignKey`：**
    - 用于定义一个关联到另一个模型的外键。
    - 示例：`author = models.ForeignKey(Author, on_delete=models.CASCADE)`

11. **`ManyToManyField`：**
    - 用于定义多对多关系的字段。
    - 示例：`tags = models.ManyToManyField(Tag)`

这只是一小部分 Django 中可用的字段类型。根据你的数据需求，你可能会使用到其他字段类型。此外，Django 还支持创建自定义字段类型。学习这些字段类型以及它们的选项和用法将有助于你更好地建模你的数据。

## 1.创建一个数据模型

在 Django 中建立数据模型是通过创建一个 Python 类来完成的，这个类继承自 `django.db.models.Model`。每个类的属性都代表模型的一个字段。下面是一个简单的例子，演示如何创建一个简单的数据模型：

假设我们要创建一个博客应用，有文章（Post）和作者（Author）两个模型。

首先，打开你的 Django 项目中的一个应用的 `models.py` 文件，并添加以下内容：

```python
from django.db import models

class Author(models.Model):
    name = models.CharField(max_length=100)
    email = models.EmailField(unique=True)

    def __str__(self):
        return self.name

class Post(models.Model):
    title = models.CharField(max_length=200)
    content = models.TextField()
    pub_date = models.DateTimeField(auto_now_add=True)
    author = models.ForeignKey(Author, on_delete=models.CASCADE)

    def __str__(self):
        return self.title
```

上述代码定义了两个模型：`Author` 和 `Post`。这些模型继承自 `models.Model`，并且每个类属性都代表了一个字段。

- `Author` 模型有两个字段：`name` 和 `email`，分别是作者的姓名和电子邮件地址。

- `Post` 模型有四个字段：`title`，`content`，`pub_date` 和 `author`。`author` 字段是一个外键，它关联到 `Author` 模型，表示文章的作者。

在定义模型之后，你需要运行以下命令来进行数据库迁移：

```bash
python manage.py makemigrations
python manage.py migrate
```

这两个命令将创建数据库表以存储你定义的模型。然后，你可以在 Django 的管理界面中操作这些模型数据，也可以在代码中使用这些模型进行数据库操作。

## 2.选择字段

在 Django 中，你可以使用 `CharField` 的一个特定变体 `choices` 来定义选择字段，这样你可以在一组预定义的选项中选择一个值。这通常用于定义模型中的某个属性只能取特定值的情况。

以下是一个例子，假设你有一个 `Product` 模型，每个产品都有一个状态，可以是 "In Stock"、"Out of Stock" 或者 "Backordered"：

```python
from django.db import models

class Product(models.Model):
    STATUS_CHOICES = [
        ('in_stock', 'In Stock'),
        ('out_of_stock', 'Out of Stock'),
        ('backordered', 'Backordered'),
    ]

    title = models.CharField(max_length=255)
    status = models.CharField(max_length=20, choices=STATUS_CHOICES)
    # 其他字段...

    def __str__(self):
        return self.title
```

在这个例子中，`STATUS_CHOICES` 是一个包含元组的列表，每个元组包含两个值：数据库中存储的值和在管理界面中显示的值。然后，我们使用 `CharField` 来存储产品的状态，并通过 `choices` 参数将预定义的选项传递给它。

这样做的好处之一是，它确保数据库中存储的值是你事先定义过的，不会有拼写错误或其他非法值。此外，这也使得在管理界面中选择产品状态更为方便。

在使用选择字段时，确保你了解 `choices` 参数的使用方式，并根据你的需求设置合适的选项。

## 3.定义一对一关系

在 Django 中，你可以使用 `OneToOneField` 来定义一对一关系。一对一关系意味着两个模型之间的每个实例都只关联到另一个模型的一个实例。以下是一个简单的示例，演示如何定义一对一关系：

假设你有两个模型：`Person` 和 `Profile`。每个人都有一个对应的个人资料。

```python
from django.db import models

class Person(models.Model):
    first_name = models.CharField(max_length=50)
    last_name = models.CharField(max_length=50)

    def __str__(self):
        return f'{self.first_name} {self.last_name}'

class Profile(models.Model):
    bio = models.TextField()
    birth_date = models.DateField()
    person = models.OneToOneField(Person, on_delete=models.CASCADE)

    def __str__(self):
        return f'Profile for {self.person.first_name} {self.person.last_name}'
```

在这个例子中：

- `Person` 模型包含了一个人的基本信息。
- `Profile` 模型包含了个人资料信息，并通过 `OneToOneField` 与 `Person` 模型关联。

`OneToOneField` 接受一个参数 `on_delete`，它指定了当关联的 `Person` 实例被删除时，与之关联的 `Profile` 实例应该如何处理。在上述例子中，`on_delete=models.CASCADE` 表示当关联的 `Person` 实例被删除时，与之关联的 `Profile` 实例也会被删除。

这样，每个人都有一个与之关联的个人资料，而且这两个模型之间是一对一的关系。你可以通过 Django 的管理界面或在代码中进行操作这些模型的实例，访问一对一关系的数据。

## 4.定义一对多关系

在 Django 中，你可以使用 `ForeignKey` 来定义一对多关系。一对多关系表示一个模型的实例关联到另一个模型的多个实例。以下是一个简单的示例，演示如何定义一对多关系：

假设你有两个模型：`Author` 和 `Book`。每个作者可以有多本书。

```python
from django.db import models

class Author(models.Model):
    name = models.CharField(max_length=100)

    def __str__(self):
        return self.name

class Book(models.Model):
    title = models.CharField(max_length=200)
    publication_date = models.DateField()
    author = models.ForeignKey(Author, on_delete=models.CASCADE, related_name='books')

    def __str__(self):
        return self.title
```

在这个例子中：

- `Author` 模型包含了作者的基本信息。
- `Book` 模型包含了书籍的信息，并通过 `ForeignKey` 与 `Author` 模型关联。`on_delete=models.CASCADE` 表示当关联的 `Author` 实例被删除时，与之关联的所有书籍也会被删除。
- `related_name='books'` 用于设置从 `Author` 到 `Book` 的反向关系的名称，使得你可以通过 `author.books.all()` 访问一个作者的所有书籍。

这样，每个作者可以关联到多本书，而每本书只能关联到一个作者。你可以通过 Django 的管理界面或在代码中操作这些模型的实例，访问一对多关系的数据。

## 5.定义多对多关系

在 Django 中，你可以使用 `ManyToManyField` 来定义多对多关系。多对多关系表示两个模型的实例之间可以互相关联多个实例。以下是一个简单的示例，演示如何定义多对多关系：

假设你有两个模型：`Student` 和 `Course`。一个学生可以选择多门课程，而一门课程也可以被多个学生选择。

```python
from django.db import models

class Student(models.Model):
    name = models.CharField(max_length=100)
    courses = models.ManyToManyField('Course', related_name='students')

    def __str__(self):
        return self.name

class Course(models.Model):
    title = models.CharField(max_length=200)

    def __str__(self):
        return self.title
```

在这个例子中：

- `Student` 模型包含了学生的基本信息，并通过 `ManyToManyField` 与 `Course` 模型关联。`related_name='students'` 用于设置从 `Course` 到 `Student` 的反向关系的名称，使得你可以通过 `course.students.all()` 访问选择了某门课程的所有学生。
- `Course` 模型包含了课程的信息。

这样，每个学生可以选择多门课程，而一门课程也可以被多个学生选择。你可以通过 Django 的管理界面或在代码中操作这些模型的实例，访问多对多关系的数据。

## 6.解决循环关系

在 Django 中，循环关系通常是通过将模型的字符串引用延迟（deferred）到后面来解决。这可以通过使用字符串而不是直接引用模型类来实现。下面是一个例子，演示如何解决循环关系：

```python
from django.db import models

class Student(models.Model):
    name = models.CharField(max_length=100)
    courses = models.ManyToManyField('Course', related_name='students')

    def __str__(self):
        return self.name

class Course(models.Model):
    title = models.CharField(max_length=200)

    def __str__(self):
        return self.title
```

在这个例子中，`models.ManyToManyField('Course', related_name='students')` 中的 `'Course'` 是一个字符串，而不是直接引用 `Course` 类。这样做可以避免在解析模型时出现循环引用的问题。

这种方法也适用于其他类型的模型关系，比如一对一关系和一对多关系。在模型的字段引用中，使用字符串引用可以推迟模型的解析，从而解决循环引用的问题。

需要注意的是，尽管使用字符串引用可以解决模型的循环引用问题，但在实际使用时，你可能还需要根据项目的结构和需求来合理设计模型之间的关系，以避免不必要的复杂性。



## 7.通用关系

在 Django 中，通用关系指的是通过使用 `GenericForeignKey` 和 `GenericRelation` 来创建适用于多个模型的关系。通常，这种关系用于构建通用的、可扩展的数据模型，例如评论系统、标签系统等，这些系统需要关联到不同类型的对象。

1. **`GenericForeignKey`：**
   
   - `GenericForeignKey` 允许你在一个模型中创建一个指向任何模型的外键关系。
   - 示例：
     ```python
     from django.contrib.contenttypes.fields import GenericForeignKey
     from django.contrib.contenttypes.models import ContentType
     from django.db import models
     
     class Comment(models.Model):
         content_type = models.ForeignKey(ContentType, on_delete=models.CASCADE)
         object_id = models.PositiveIntegerField()
         content_object = GenericForeignKey('content_type', 'object_id')
         text = models.TextField()
     
         def __str__(self):
             return f"Comment by {self.user} on {self.content_object}"
     ```

在上述例子中，`Comment` 模型使用了 `GenericForeignKey` 来关联到不同类型的对象，而 `TaggedItem` 模型使用了 `GenericRelation` 来实现一个通用的标签关系，可以关联到不同类型的对象（例如 `Article`）。

通过使用通用关系，你可以实现更灵活的模型设计，允许模型与多种类型的对象建立关系，而不必为每种类型都定义一个独立的外键。这对于构建通用的、可扩展的应用程序组件非常有用。

**在这个 `Comment` 模型中，`content_type`、`object_id` 和 `content_object` 的组合用于实现通用关系，允许 `Comment` 关联到任何其他模型的实例。让我逐个解释这些字段的作用：**

1. **`content_type`：**
   - `content_type` 字段是一个外键，它关联到 `ContentType` 模型。`ContentType` 模型是 Django 提供的一个系统模型，用于存储每个模型的元信息。
   - 在这里，`content_type` 用于指示关联的对象是哪个模型。通过 `ForeignKey` 指向 `ContentType` 模型，你可以将 `content_type` 设置为任何模型的主键，从而使得 `Comment` 模型可以与不同类型的对象建立关系。

2. **`object_id`：**
   - `object_id` 字段是一个正整数字段，用于存储关联对象的主键（`id`）。它与 `content_type` 一起，指定了具体关联到哪个对象的实例。

3. **`content_object`：**
   - `content_object` 字段是一个通用外键（`GenericForeignKey`），它是一个虚拟字段，通过 `content_type` 和 `object_id` 来实现与不同类型对象的关联。
   - `GenericForeignKey` 提供了一个便捷的方式，允许你通过 `content_object` 直接访问与 `Comment` 关联的对象。在实例化 `Comment` 时，`content_object` 会根据 `content_type` 和 `object_id` 自动关联到正确的模型实例。

这种设计的好处在于，`Comment` 模型不需要为每一种可能的关联对象定义一个独立的外键。相反，它使用通用的 `content_type` 和 `object_id` 字段，使得可以关联到任何模型。这在需要实现通用关系的场景中非常有用，例如评论系统，其中评论可以关联到文章、图片、用户等不同类型的对象。这样的通用关系使得模型更加灵活和可扩展。

### 实例

```python
from django.db import models
from django.contrib.auth.models import User
from django.contrib.contenttypes.models import ContentType
from django.contrib.contenttypes.fields import GenericForeignKey

class likedItem(models.Model):
    user = models.ForeignKey(User,on_delete=models.CASCADE)
    content_type = models.ForeignKey(ContentType,on_delete=models.CASCADE)
    object_id = models.PositiveIntegerField()
    content_object = GenericForeignKey()
```

这是一个用于记录用户点赞操作的 Django 模型。让我们逐行解释这个模型的各个部分：

1. **`user`：**
   - 这是一个外键字段，关联到 Django 内置的 `User` 模型。它表示点赞的用户。

2. **`content_type`：**
   - 这是一个外键字段，关联到 Django 提供的 `ContentType` 模型。`ContentType` 模型用于存储每个模型的元信息。
   - 这个字段用于指示被点赞对象的模型类型。通过 `ForeignKey` 指向 `ContentType` 模型，可以将 `content_type` 设置为任何模型的主键。

3. **`object_id`：**
   - 这是一个正整数字段，用于存储被点赞对象的主键（`id`）。它与 `content_type` 字段一起，指定了具体被点赞对象的实例。

4. **`content_object`：**
   - 这是一个通用外键（`GenericForeignKey`）。通用外键允许将模型关联到不同类型的对象，而无需为每一种类型都定义一个独立的外键。
   - 在这里，`GenericForeignKey` 的声明中没有明确指定 `content_type` 和 `object_id`，这是因为这两个字段在前面已经在 `content_type` 和 `object_id` 字段中定义过了。`GenericForeignKey` 会自动使用这两个字段进行关联。

通过这个模型设计，你可以记录用户对任何模型的实例进行的点赞操作。例如，如果你有一个 `Article` 模型，用户可以点赞文章；如果你有一个 `Photo` 模型，用户也可以点赞照片。这样，你可以使用同一个 `likedItem` 模型来追踪用户的点赞行为，而无需为每一种模型都定义一个单独的点赞模型。这种通用关系的设计使得模型更加灵活和可扩展。

# 建立数据库

## 1.创建迁移

如果你确定 `storefront` 应用程序的模型在 `models.py` 文件中已经定义，并且在 `INSTALLED_APPS` 中添加了 `'storefront'`，但是运行 `python manage.py makemigrations` 时没有生成 `storefront` 的迁移文件，可以尝试手动创建迁移文件。执行以下步骤：

1. 在 `storefront` 应用程序的目录下，确保存在 `models.py` 文件。该文件应该包含你要迁移的模型定义。

2. 打开命令行终端，确保当前工作目录在包含 `manage.py` 文件的 Django 项目的根目录下。

3. 运行以下命令，手动生成迁移文件：
   ```bash
   python manage.py makemigrations storefront
   ```

4. 如果一切正常，应该看到有关 `storefront` 应用程序的新迁移文件生成的消息。

如果手动生成迁移文件也不起作用，可能存在其他问题。在这种情况下，你可以尝试检查控制台输出，看是否有关于错误或警告的信息。如果问题仍然存在，可能需要进一步调查，例如检查 `storefront` 应用程序的目录结构、确保没有语法错误等。

## 2.运行迁移

一旦你已经创建了迁移文件，接下来就可以运行迁移来将数据库与模型同步。运行迁移的步骤如下：

1. 在终端中，确保你的当前工作目录在包含 `manage.py` 文件的 Django 项目的根目录下。

2. 运行以下命令，将迁移应用到数据库：
   ```bash
   python manage.py migrate
   ```

3. 如果你只想迁移某个应用程序，可以指定应用程序的名称：
   ```bash
   python manage.py migrate storefront
   ```

4. 查看控制台输出，确保没有错误消息。如果一切正常，你的数据库应该与模型同步。

注意事项：
- 如果在运行 `migrate` 时遇到任何错误，检查控制台输出以获取详细信息。错误消息将帮助你确定发生了什么问题以及如何解决它。
- 如果有多个数据库配置，确保使用正确的数据库配置，可以在命令中使用 `--database` 参数指定数据库。

通过这些步骤，你应该能够成功运行迁移，将数据库更新为最新的模型定义。

## 3.定制数据库模式

在 Django 中，可以通过使用模型的 Meta 类来进行数据库模式的定制。Meta 类包含了一系列选项，允许你配置模型的行为，包括数据库表名、索引、排序等。以下是一些常用的定制选项：

1. **表名 (Table Name):**
   
   - `db_table`: 定义数据库中表的名称。
   ```python
   class MyModel(models.Model):
       # 模型定义...
   
       class Meta:
           db_table = 'custom_table_name'
   ```
   
2. **索引 (Indexes):**
   
   - `indexes`: 定义模型中的索引。
   ```python
   class MyModel(models.Model):
       # 模型定义...
   
       class Meta:
           indexes = [
               models.Index(fields=['field_name']),
           ]
   ```

这只是一些常见的选项，还有其他可用的选项。通过使用 Meta 类，你可以更精细地控制模型在数据库中的表现形式。要查看所有可用的选项，请参阅 Django 官方文档中关于 [Model Meta options](https://docs.djangoproject.com/en/3.2/ref/models/options/) 的部分

## 4.还原迁移

如果在应用迁移时出现了问题，可以使用以下步骤进行迁移的回滚和还原。

1. **查看可用的迁移点：**
   运行以下命令，查看可用的迁移点（migration points）：
   ```bash
   python manage.py showmigrations
   ```
   这将列出所有已应用和未应用的迁移。找到你想要回滚到的迁移点。

2. **回滚到指定的迁移点：**
   使用以下命令回滚到指定的迁移点（replace `your_migration_name` with the actual migration name）：
   ```bash
   python manage.py migrate your_app_name your_migration_name
   ```
   或者如果你想回滚到最初的状态，可以使用 `zero`：
   ```bash
   python manage.py migrate your_app_name zero
   ```

3. **重新应用迁移：**
   如果需要重新应用之前回滚的迁移，可以再次运行 `migrate` 命令：
   
   ```bash
   python manage.py migrate
   ```
   这将应用未应用的迁移，并将数据库状态还原到最新的迁移点。

请注意：
- 回滚迁移可能会导致数据丢失，因此在执行此操作之前，请确保已备份数据库。
- 如果迁移包含数据库表的创建操作，还原迁移可能需要手动删除相应的表。在执行还原之前，请仔细阅读迁移文件以了解它所执行的操作。

根据你的具体情况，选择适当的迁移点并执行上述步骤。如果还有其他问题或需要更详细的帮助，请提供更多上下文信息，我将尽力提供支持。

## 5.生成虚拟数据

可以使用网站**mockaroo.com** 定义虚拟数据







# Django ORM

# 查询对象

Django ORM（Object-Relational Mapping）是 Django 框架中的一个功能，用于在应用程序代码和数据库之间建立映射关系。**ORM 的目标是让开发者能够使用面向对象的方式操作数据库，而不必直接编写 SQL 查询语句。**

Django的ORM（Object-Relational Mapping）是一种将数据库表与Python对象关联起来的技术，使得在Python代码中可以使用对象的方式来进行数据库操作，而不必直接使用SQL语句。

以下是Django ORM的一些基本概念和使用方法：

### 1. **定义模型类（Model）**
Django的模型类对应数据库中的表，模型类的属性对应表的字段。例如：

```python
from django.db import models

class Book(models.Model):
    title = models.CharField(max_length=100)
    author = models.CharField(max_length=50)
    publication_date = models.DateField()

    def __str__(self):
        return self.title
```

### 2. **创建数据库迁移**
模型类定义好后，需要通过以下命令生成数据库迁移文件：

```bash
python manage.py makemigrations
```

### 3. **应用数据库迁移**
将生成的迁移应用到数据库：

```bash
python manage.py migrate
```

### 4. **查询数据**
使用模型类进行数据库查询：

```python
# 查询所有图书
books = Book.objects.all()

# 条件查询
recent_books = Book.objects.filter(publication_date__gte='2022-01-01')

# 获取单个对象
book = Book.objects.get(pk=1)
```

### 5. **插入和更新数据**
使用模型类创建对象，然后保存到数据库：

```python
new_book = Book(title='New Book', author='Author Name', publication_date='2022-02-01')
new_book.save()

# 更新数据
book = Book.objects.get(pk=1)
book.title = 'Updated Title'
book.save()
```

### 6. **删除数据**
使用 `delete()` 方法删除数据：

```python
book = Book.objects.get(pk=1)
book.delete()
```

### 7. **关联关系**
处理模型之间的关联关系，如一对多、多对多：

```python
class Author(models.Model):
    name = models.CharField(max_length=50)

class Book(models.Model):
    title = models.CharField(max_length=100)
    author = models.ForeignKey(Author, on_delete=models.CASCADE)
```

### 8. **使用管理器（Manager）**
Django提供了默认的管理器，允许你执行数据库查询：

```python
# 自定义查询集
class CustomQuerySet(models.QuerySet):
    def recent_books(self):
        return self.filter(publication_date__gte='2022-01-01')

class Book(models.Model):
    title = models.CharField(max_length=100)
    author = models.CharField(max_length=50)
    publication_date = models.DateField()

    # 使用自定义查询集
    objects = CustomQuerySet.as_manager()
```

这些是Django ORM的一些基础概念和用法。通过使用ORM，你可以更方便地与数据库交互，而不必直接编写SQL语句。

## 一.管理器和问题集

在Django中，`managers` 和 `querysets` 是与数据库交互的重要组件。它们允许你执行数据库查询和操作，以及定义自定义查询方法。

### Managers（管理器）

`Manager` 是Django模型的一个管理类，它充当模型的数据库代理，为模型提供一些用于数据库操作的方法。每个Django模型都有一个默认的管理器，可以通过 `objects` 访问。你也可以为模型定义自己的自定义管理器。

**示例：**

```python
from django.db import models

class CustomManager(models.Manager):
    def published_books(self):
        return self.filter(status='published')

class Book(models.Model):
    title = models.CharField(max_length=100)
    author = models.CharField(max_length=50)
    status = models.CharField(max_length=20)

    # 使用自定义管理器
    objects = CustomManager()
```

在上面的例子中，我们为 `Book` 模型定义了一个自定义管理器 `CustomManager`，并添加了一个查询方法 `published_books`，用于查询状态为 'published' 的图书。

### Querysets（查询集）

`QuerySet` 是Django的数据库查询抽象。它是一个可以被过滤、切片和操作的查询集合。每个模型都有一个默认的查询集，通常通过模型的 `objects` 属性访问。

**示例：**

```python
# 获取所有图书
books = Book.objects.all()

# 过滤查询
published_books = Book.objects.filter(status='published')

# 链式操作
recent_books = Book.objects.filter(status='published').order_by('-publication_date')[:5]
```

`QuerySet` 的方法返回一个新的 `QuerySet` 对象，允许你链式操作，构建复杂的查询。

### 自定义Querysets

你还可以为模型定义自定义 `QuerySet` 方法，类似于为管理器定义自定义方法。

**示例：**

```python
class BookQuerySet(models.QuerySet):
    def published_books(self):
        return self.filter(status='published')

class Book(models.Model):
    title = models.CharField(max_length=100)
    author = models.CharField(max_length=50)
    status = models.CharField(max_length=20)

    # 使用自定义QuerySet
    objects = BookQuerySet.as_manager()
```

在上述例子中，我们为 `Book` 模型定义了一个自定义 `QuerySet` 类 `BookQuerySet`，并在模型的 `objects` 属性中使用 `as_manager()` 方法将其作为默认管理器。

通过自定义管理器和查询集，你可以使模型的数据库交互更加灵活和可定制。这有助于使你的代码更清晰、模块化，并提供更高级别的抽象。

## 二.检索(获得)对象

在Django中，检索（或获取）对象是一项基本任务，通常通过使用查询集（QuerySet）来完成。以下是一些常见的检索对象的方法：

### 1. 获取所有对象：

```python
# 获取模型的所有对象
all_objects = YourModel.objects.all()
```

### 2. 根据主键（ID）获取单个对象：

```python
# 获取主键为1的对象
single_object = YourModel.objects.get(pk=1)
```

### 3. 使用 `filter` 进行过滤：

```python
# 根据条件过滤对象
filtered_objects = YourModel.objects.filter(some_field=some_value)
```

### 4. 使用 `exclude` 进行排除：

```python
# 排除满足条件的对象
excluded_objects = YourModel.objects.exclude(some_field=some_value)
```

### 5. 使用 `first` 获取第一个对象：

```python
# 获取符合条件的第一个对象
first_object = YourModel.objects.filter(some_field=some_value).first()
```

### 6. 使用 `last` 获取最后一个对象：

```python
# 获取符合条件的最后一个对象
last_object = YourModel.objects.filter(some_field=some_value).last()
```

### 7. 使用 `values` 获取特定字段的值：

```python
# 获取特定字段的值列表
values_list = YourModel.objects.filter(some_field=some_value).values('field1', 'field2')
```

### 8. 使用 `get_or_create` 避免重复创建对象：

```python
# 获取或创建对象，如果不存在则创建新对象
obj, created = YourModel.objects.get_or_create(some_field=some_value, defaults={'field1': 'value1'})
```

### 9. 使用 `exists` 检查是否存在符合条件的对象：

```python
# 检查是否存在符合条件的对象
exists = YourModel.objects.filter(some_field=some_value).exists()
```

### 10. 使用 `values_list` 获取特定字段的值列表：

```python
# 获取特定字段的值列表
values_list = YourModel.objects.filter(some_field=some_value).values_list('field1', flat=True)
```

这些是一些基本的方法，你可以根据需要组合使用它们，以满足你的具体需求。记住在处理数据库查询时，注意错误处理，并确保不会引发未处理的异常。

## 实例

```python
from django.shortcuts import render
from django.core.exceptions import ObjectDoesNotExist
from django.http import HttpResponse
from store.models import Product


def say_hello(request):
    product = Product.objects.filter(pk=1).first()

    return render(request, 'hello.html', {'name': 'Mosh'})
```

通过使用filter(pk=1).first() **可以即使查询结果没有 也不会报错**    

first()它会返回一个None

也有一个exists() 他会返回true 或 false

## 三.过滤对象

在Django中，过滤对象是一项常见的数据库操作。你可以使用 `filter()` 方法来从数据库中检索满足特定条件的对象。以下是一些常见的过滤对象的例子：

### 1. 基本过滤：

```python
# 获取某个字段等于特定值的对象
filtered_objects = YourModel.objects.filter(some_field=some_value)
```

### 2. 多个条件的过滤：

```python
# 获取满足多个条件的对象
filtered_objects = YourModel.objects.filter(field1=value1, field2=value2)
```

### 3. 使用 `__exact` 进行精确匹配：

```python
# 获取字段精确匹配特定值的对象
exact_match_objects = YourModel.objects.filter(some_field__exact=some_value)
```

### 4. 使用 `__iexact` 进行忽略大小写的精确匹配：

```python
# 获取字段忽略大小写精确匹配特定值的对象
iexact_match_objects = YourModel.objects.filter(some_field__iexact=some_value)
```

### 5. 使用 `__contains` 进行包含匹配：

```python
# 获取字段包含特定值的对象
contains_objects = YourModel.objects.filter(some_field__contains=some_value)
```

### 6. 使用 `__icontains` 进行忽略大小写的包含匹配：

```python
# 获取字段忽略大小写包含特定值的对象
icontains_objects = YourModel.objects.filter(some_field__icontains=some_value)
```

### 7. 使用 `__in` 进行范围匹配：

```python
# 获取字段值在特定列表中的对象
in_objects = YourModel.objects.filter(some_field__in=[value1, value2, value3])
```

### 8. 使用 `__gt`, `__lt`, `__gte`, `__lte` 进行比较匹配：

```python
# 获取字段值大于、小于、大于等于、小于等于某个值的对象
gt_objects = YourModel.objects.filter(some_field__gt=value)
lt_objects = YourModel.objects.filter(some_field__lt=value)
gte_objects = YourModel.objects.filter(some_field__gte=value)
lte_objects = YourModel.objects.filter(some_field__lte=value)
```

### 9. 复杂的 Q 对象：

使用 `Q` 对象可以构建复杂的查询条件，可以使用 `|`（或）和 `&`（与）进行组合。

```python
from django.db.models import Q

# 获取满足多个条件之一的对象
complex_objects = YourModel.objects.filter(Q(condition1) | Q(condition2))
```

这只是过滤对象的一些基本示例，你可以根据具体需求组合使用这些方法。查看 [Django文档中的查询API](https://docs.djangoproject.com/en/3.2/topics/db/queries/) 以获取更多详细信息。

`__range` 是Django查询中用于指定范围条件的查询条件之一。它允许你筛选在指定范围内的对象。`__range` 主要用于对日期、时间或数字字段进行范围查询。

### 1. 范围查询对日期字段的应用：

```python
# 获取在指定日期范围内的对象
start_date = datetime.date(2022, 1, 1)
end_date = datetime.date(2022, 12, 31)
objects_in_range = YourModel.objects.filter(date_field__range=(start_date, end_date))
```

这将返回 `date_field` 字段在 `start_date` 和 `end_date` 之间的所有对象。

### 2. 范围查询对数字字段的应用：

```python
# 获取在指定数字范围内的对象
start_value = 10
end_value = 20
objects_in_range = YourModel.objects.filter(number_field__range=(start_value, end_value))
```

这将返回 `number_field` 字段在 `start_value` 和 `end_value` 之间的所有对象。

## 四.使用 Q 对象进行复杂查询

在Django中，使用Q对象进行复杂的查询可以更灵活地构建查询条件，尤其是涉及AND、OR和NOT等复杂操作的情况。Q对象是`django.db.models`模块中`Q`类的实例。

以下是使用Q对象进行复杂查询的示例：

```python
from django.db.models import Q
from .models import Product

# 示例：检索价格在$20到$30之间的产品，或者评分大于4的产品
queryset = Product.objects.filter(Q(unit_price__range=(20, 30)) | Q(rating__gt=4))

# 另一个示例：检索价格小于$20且（类别为'Electronics'或'Clothing'）的产品
queryset = Product.objects.filter(
    Q(unit_price__lt=20) & (Q(category='Electronics') | Q(category='Clothing'))
)
```

在第一个示例中，使用OR（`|`）运算符将`Q`对象组合在一起。此查询检索价格在$20到$30之间的产品或者评分大于4的产品。

在第二个示例中，使用AND（`&`）运算符将`Q`对象组合在一起。此查询检索价格小于$20且（类别为'Electronics'或'Clothing'）的产品。

您可以使用括号控制操作的顺序，就像在常规的Python表达式中一样。复杂查询在需要表达复杂条件的情况下特别有用。

## 五.使用 F 对象引用字段

在Django中，`F`对象用于引用模型的字段，以便在查询中执行数据库字段之间的比较。以下是一个使用`F`对象的示例：

假设有一个名为`Product`的模型，具有两个字段：`current_price`和`original_price`。我们想要查询出当前价格低于原始价格的所有产品。

```python
from django.db.models import F
from django.shortcuts import render
from store.models import Product

def discounted_products(request):
    queryset = Product.objects.filter(current_price__lt=F('original_price'))
    return render(request, 'discounted_products.html', {'products': list(queryset)})
```

在上述代码中，`F('original_price')`表示对`original_price`字段的引用。这样，`current_price__lt=F('original_price')`就表示查询`current_price`小于`original_price`的产品。

使用`F`对象的好处是，它允许在查询中动态地引用模型的字段，而不是硬编码它们的值，使得查询更加灵活和可维护。

## 六.对数据进行排序

在Django中，你可以使用 `order_by()` 方法对查询结果进行排序。这方法接受一个或多个字段名作为参数，指定按照哪些字段进行排序，还可以使用负号 (`-`) 表示降序排序。

以下是一些示例：

### 1. 升序排序：

```python
# 按照某个字段升序排序
ascending_objects = YourModel.objects.all().order_by('some_field')
```

### 2. 降序排序：

```python
# 按照某个字段降序排序
descending_objects = YourModel.objects.all().order_by('-some_field')
```

### 3. 多字段排序：

```python
# 按照多个字段进行排序，先按照 field1 升序，再按照 field2 降序
multi_field_objects = YourModel.objects.all().order_by('field1', '-field2')
```

### 4. 随机排序：

如果你想要随机排序，可以使用 `?` 作为参数：

```python
# 随机排序
random_objects = YourModel.objects.all().order_by('?')
```

请注意，使用 `?` 随机排序可能在大数据集上效率较低，因为它需要将整个结果集加载到内存中，然后进行排序。

### 5. 对日期字段排序：

```python
# 按照日期字段升序排序
date_sorted_objects = YourModel.objects.all().order_by('date_field')
```

## 七.限制结果

在Django中，`[:n]` 语法用于限制查询结果的数量。这是一种切片（slicing）操作，类似于Python中对列表或其他可迭代对象进行切片的语法。在Django查询中，`[:n]` 用于获取结果集的前 `n` 个对象。

下面是一些使用 `[:n]` 语法的示例：

```python
# 获取模型的前5个对象    0,1,2,3,4索引
first_five_objects = YourModel.objects.all()[:5]
```

```python
#获得模型索引5到索引9的对象
first_five_objects = YourModel.objects.all()[5:10]
```

## 八.选择要查询的字段

在Django中，你可以使用 `values()` 或 `values_list()` 方法来选择要查询的字段，以限制返回的数据。这两种方法可以帮助减少数据库负载，只返回你实际需要的字段数据。

### 1. 使用 `values()` 方法选择特定字段：

```python
# 查询模型的某些字段并返回字典形式的结果
selected_fields = YourModel.objects.values('field1', 'field2', 'field3')
```

此时，`selected_fields` 将是一个包含**字典**的 QuerySet，每个字典表示一个对象，只包含指定的字段。

### 2. 使用 `values_list()` 方法选择特定字段：

```python
# 查询模型的某些字段并返回元组形式的结果
selected_fields_list = YourModel.objects.values_list('field1', 'field2', 'field3')
```

`selected_fields_list` 将是一个包含**元组**的 QuerySet，每个元组表示一个对象，只包含指定的字段。

### 3. 使用 `distinct()` 去除重复的结果：

```python
# 查询某个字段的唯一值
unique_values = YourModel.objects.values('field1').distinct()
```

### 4. 结合其他查询方法和选择字段：

```python
# 查询满足条件的对象，并返回指定字段的结果
filtered_and_selected = YourModel.objects.filter(some_condition).values('field1', 'field2')
```

在这些例子中，你可以根据需要选择查询的字段，以便只返回你实际需要的数据。这不仅可以减少数据库负载，还能提高查询性能。

### 实例

```python
def say_hello(request):
    queryset = Product.objects.values('id','title','collection__title')
 #上面的collection__title 相当于连接其他模型的title 
 #前提需要在Product中有collectionw外键
    return render(request, 'hello.html', {'name': 'Mosh','products': list(queryset)})
```

`__` 是Django中用于表示跨关联的方式。在这里，`collection__title` 表示你想要获取 `Product` 模型的外键字段 `collection` 所关联对象的 `title` 字段。

## 显示所有被购买的产品实例

在这段代码中，`say_hello` 是一个 Django 视图函数。让我们逐步解释这个函数：

```python
def say_hello(request):
    queryset = Product.objects.filter(
        id__in=OrderItem.objects.values('product_id').distinct()
    )
```

1. `OrderItem.objects.values('product_id').distinct()`：这部分查询是为了从 `OrderItem` 模型中获取所有唯一的 `product_id` 值。`.values('product_id')` 表示只获取 `product_id` 字段的值，而 `.distinct()` 则表示去重，确保我们得到的是唯一的 `product_id`。

2. `Product.objects.filter(id__in=...)`：这部分是为了从 `Product` 模型中获取那些在 `OrderItem` 模型中出现的 `product_id` 的产品。`id__in=` 表示过滤条件，它限制了 `Product` 对象的 `id` 必须在给定的列表中，而给定的列表正是之前从 `OrderItem` 中获取的唯一的 `product_id`。

所以，整体上，`queryset` 包含了所有在 `OrderItem` 中出现过的产品对象。这可能是为了在视图中显示所有被购买的产品，或者做其他类似的操作。

在模板中，你可以通过循环遍历 `queryset` 中的产品对象，并访问它们的属性，例如 `{{ product.id }}`、`{{ product.title }}` 等。

## 九.延迟字段加载

在Django中，"推迟（延迟）某些字段的加载以减少数据库查询的开销。通常，在查询数据库时，Django会加载模型的所有字段，但在某些情况下，你可能只需要加载模型的一部分字段。

使用 `only()` 方法可以选择加载模型的特定字段，而使用 `defer()` 方法可以推迟加载特定字段。这两者的区别在于，`only()` 加载指定的字段，而 `defer()` 推迟加载指定的字段。

以下是 `defer()` 方法的基本用法：

```python
# models.py
class MyModel(models.Model):
    field1 = models.CharField(max_length=100)
    field2 = models.IntegerField()
    field3 = models.BooleanField()
    # ...

# views.py
def my_view(request):
    # 推迟加载 field2 和 field3 字段
    queryset = MyModel.objects.defer('field2', 'field3')
    # 其他操作...
```

在这个例子中，`queryset` 将包含 `MyModel` 对象，但 `field2` 和 `field3` 字段的值不会被立即加载。这对于减轻查询的数据库开销是有帮助的，尤其是当模型有大量字段而你只关心其中的一部分时。

你可以在需要的时候加载这些字段，例如在模板中，通过以下方式：

```html
{% for obj in queryset %}
    {{ obj.field1 }}
    {{ obj.field2 }}
    {{ obj.field3 }}
    <!-- 这时候才会实际加载 field2 和 field3 字段的值 -->
{% endfor %}
```

在使用 `defer()` 方法时要注意一些事项：

- 推迟加载的字段在被访问之前不会被加载，因此如果在数据库查询中使用了推迟加载，确保在需要访问这些字段之前调用了 `defer()` 方法。
- 推迟加载的字段只能在数据库层面进行，因此如果你的模型有一些计算字段或方法，它们不受 `defer()` 的影响。
- 推迟加载的字段不能在查询集中进行过滤、排序等操作，因为这些操作可能涉及到被推迟加载的字段。

在实际使用中，根据具体情况来选择使用 `defer()` 方法，以提高查询性能和减轻数据库负担。

## 十.选择相关对象

在 Django 中，"select_related" 和 "prefetch_related" 是用于优化查询并选择关联对象的两个方法。

### 1. `select_related`：

`select_related` 用于一对一和多对一关系的查询。它执行一个 SQL 查询来获取主对象和关联对象的数据，以减少额外的数据库查询。这在遍历一对一和多对一关系时非常有用。

**示例：**

```python
# models.py
class Author(models.Model):
    name = models.CharField(max_length=100)

class Book(models.Model):
    title = models.CharField(max_length=100)
    author = models.ForeignKey(Author, on_delete=models.CASCADE)
    # ...

# views.py
def my_view(request):
    # 使用 select_related 加载 Book 对象和相关联的 Author 对象
    queryset = Book.objects.select_related('author')
    # 其他操作...
```

在这个例子中，`queryset` 包含了 `Book` 对象和相关联的 `Author` 对象。这样，在模板或视图中访问 `book.author.name` 不会导致额外的数据库查询，因为相关的作者信息已经在原始查询中加载了。

### 2.使用prefetch_related()的基本语法：

`prefetch_related()` 是 Django 中用于优化查询的方法，特别适用于处理多对多关系和反向关系的查询。它通过执行两个独立的查询，将主对象和关联对象的数据一并获取，并在 Python 中将它们合并，以减少额外的数据库查询。

```python
# models.py
class Category(models.Model):
    name = models.CharField(max_length=100)

class Product(models.Model):
    name = models.CharField(max_length=100)
    categories = models.ManyToManyField(Category)
    # ...

# views.py
def my_view(request):
    # 使用 prefetch_related 加载 Product 对象和相关联的 Category 对象
    queryset = Product.objects.prefetch_related('categories')
    # 其他操作...
```

在这个例子中，`queryset` 包含了 `Product` 对象和相关联的 `Category` 对象。这样，在模板或视图中访问 `product.categories.all()` 不会导致额外的数据库查询，因为相关的分类信息已经在原始查询中加载了。

### `prefetch_related()` 的特点和优势：

1. **减少数据库查询次数：** `prefetch_related()` 通过执行两个查询，并在 Python 层面合并结果，减少了额外的数据库查询次数。

2. **处理多对多关系：** 特别适用于处理多对多关系，因为它可以有效地获取主对象和相关联对象之间的关系。

3. **反向关系优化：** 对于反向关系（例如，一对多中的多那一方），`prefetch_related()` 也能有效地减少查询次数。

4. **合并结果：** 将主对象和关联对象的数据在 Python 层面合并，以便在访问关联数据时避免多次数据库查询。

### 示例说明：

考虑一个博客系统，有 `Author` 和 `Post` 两个模型，它们之间是一对多关系（一个作者可以有多篇文章）：

```python
# models.py
class Author(models.Model):
    name = models.CharField(max_length=100)

class Post(models.Model):
    title = models.CharField(max_length=200)
    content = models.TextField()
    author = models.ForeignKey(Author, on_delete=models.CASCADE)
    # ...
```

在这种情况下，如果我们想要获取所有作者及其对应的所有文章，可以使用 `prefetch_related('post_set')`：

```python
# views.py
def authors_with_posts(request):
    authors = Author.objects.prefetch_related('post_set')
    # 其他操作...
```

这将在查询时一次性获取所有作者和他们的所有文章，而不需要在访问每个作者的文章时执行额外的数据库查询。

总的来说，`prefetch_related()` 是一个有力的工具，用于处理复杂的关联查询，提高查询性能，减少数据库负担。

## 十一.反向关系

反向关系在 Django 中具有重要的作用，它为开发者提供了方便的方式来在一个模型中访问与其关联的对象。通过定义反向关系，你可以更自然地遍历模型之间的关联，而不必依赖于原始模型的名称。

考虑以下情况：

```python
# models.py
class Author(models.Model):
    name = models.CharField(max_length=100)

class Book(models.Model):
    title = models.CharField(max_length=100)
    author = models.ForeignKey(Author, on_delete=models.CASCADE)
```

在这个例子中，`Book` 模型有一个外键字段 `author`，它关联到 `Author` 模型。默认情况下，Django 会在 `Author` 模型中自动创建一个反向关系，该关系使用默认的名称 `book_set`。

如果没有定义 `related_name`，你将以如下方式访问关联的书籍：

```python
author = Author.objects.get(id=1)
books = author.book_set.all()  # 获取与作者关联的所有书籍
```

然而，通过使用 `related_name`，你可以自定义这个反向关系的名称：

```python
class Author(models.Model):
    name = models.CharField(max_length=100)

class Book(models.Model):
    title = models.CharField(max_length=100)
    author = models.ForeignKey(Author, on_delete=models.CASCADE, related_name='books')
```

现在，你可以以更直观的方式访问关联的书籍：

```python
author = Author.objects.get(id=1)
books = author.books.all()  # 获取与作者关联的所有书籍
```

**反向关系的意义和优势：**

1. **代码可读性：** 使用自定义的反向关系名称使代码更清晰、更易读，提高了代码的可维护性。

2. **方便访问关联对象：** 通过反向关系，你可以更方便地在一个模型中访问其关联对象，而无需记住或依赖于默认的关系名称。

3. **避免命名冲突：** 在模型中可能存在多个外键指向同一模型的情况，通过自定义反向关系名称可以避免默认名称的冲突。

总体而言，反向关系使得模型之间的关联更加灵活、可读，是 Django 中模型系统的重要特性之一。

### 实例

这行代码是使用 Django 查询 API 来获取订单（Order）对象的查询集（QuerySet）。让我们逐步解释这行代码：

```python
queryset = Order.objects.select_related('customer').prefetch_related('orderitem_set__product').order_by('-placed_at')[:5]
```

1. `Order.objects`: 这是一个 Django 模型查询的入口，表示要查询 `Order` 模型的对象。

2. `.select_related('customer')`: 使用 `select_related` 方法，这是一种优化查询的方式。它指示数据库在查询 `Order` 对象时，一并加载关联的 `customer` 对象。这假设 `Order` 模型有一个外键关联到 `Customer` 模型，例如：

   ```python
   class Order(models.Model):
       customer = models.ForeignKey(Customer, on_delete=models.CASCADE)
       # 其他字段...
   ```

   通过使用 `select_related('customer')`，可以避免在后续代码中对 `customer` 对象执行额外的数据库查询。

3. `.prefetch_related('orderitem_set__product')`: 使用 `prefetch_related` 方法，同样是一种优化查询的方式。它指示数据库在查询 `Order` 对象时，一并加载关联的 `orderitem_set` 对象，并且进一步加载 `orderitem_set` 中每个对象的关联 `product` 对象。这假设 `Order` 模型有一个反向关联到 `OrderItem` 模型的外键，而 `OrderItem` 模型有一个外键关联到 `Product` 模型，例如：

   ```python
   class Order(models.Model):
       # 其他字段...
   
   class OrderItem(models.Model):
       order = models.ForeignKey(Order, on_delete=models.CASCADE)
       product = models.ForeignKey(Product, on_delete=models.CASCADE)
       # 其他字段...
   ```

   注意：这里使用了 `orderitem_set__product`，表示通过反向关系 `orderitem_set` 访问每个订单项的关联产品。

4. `.order_by('-placed_at')`: 使用 `order_by` 方法，按照 `placed_at` 字段降序排列查询结果。这假设 `Order` 模型有一个名为 `placed_at` 的字段，表示订单的下单时间。

5. `[:5]`: 最后，使用切片操作，表示只获取排序后的前 5 条记录。

综合而言，这行代码的目的是获取最近的 5 个订单，并在查询时通过 `select_related` 和 `prefetch_related` 优化加载关联的 `customer` 对象、`orderitem_set` 对象以及每个订单项的关联产品对象，以减少额外的数据库查询次数。

## 十二.聚合对象

在 Django 中，聚合（aggregation）是指对数据库中的一组对象执行某种计算，如计算平均值、总和、最大值等。Django 提供了 `aggregate()` 方法来实现聚合操作。

以下是一个简单的例子，假设你有一个模型 `Book`，其中包含了一些书籍的价格信息：

```python
# models.py
from django.db import models

class Book(models.Model):
    title = models.CharField(max_length=100)
    price = models.DecimalField(max_digits=5, decimal_places=2)
```

现在，如果你想计算所有书籍价格的总和，你可以使用 `aggregate()` 方法：

```python
# views.py
from django.db.models import Sum

total_price = Book.objects.aggregate(total_price=Sum('price'))
```

在这个例子中，`total_price` 将包含一个字典，其中键是指定的聚合别名（在这里是 `total_price`），值是计算的结果。在这个例子中，它将是所有书籍价格的总和。

你还可以使用其他聚合函数，例如 `Avg`（平均值）、`Max`（最大值）、`Min`（最小值）等。以下是一些例子：

```python
from django.db.models import Avg, Max, Min

average_price = Book.objects.aggregate(average_price=Avg('price'))
max_price = Book.objects.aggregate(max_price=Max('price'))
min_price = Book.objects.aggregate(min_price=Min('price'))
```

这些聚合函数可以用于各种场景，以便对一组对象进行复杂的计算。在聚合中，你可以根据自己的需求组合不同的聚合函数，以获取所需的统计信息。

# 表达式类

在 Django 中，表达式类（Expression classes）是用于构建复杂数据库查询的对象。这些表达式类属于 `django.db.models.expressions` 模块，它们允许你在查询中执行各种数据库操作，如聚合、数学运算、日期操作等。

以下是一些常用的 Django 表达式类：

1. **`F()` 对象：** 用于引用数据库中的字段，允许在查询中进行字段之间的比较和操作。

   ```python
   from django.db.models import F

   # 示例：增加每个对象的 count 字段值
   queryset = MyModel.objects.annotate(increased_count=F('count') + 1)
   ```

2. **`Expression()` 类：** 用于执行数学运算和逻辑运算。

   ```python
   from django.db.models import Expression, F

   # 示例：执行数学运算，将 price 字段值减去 discount 字段值
   expression = Expression(F('price') - F('discount'))
   queryset = MyModel.objects.annotate(calculated_value=expression)
   ```

3. **`Func()` 类：** 用于执行数据库函数。

   ```python
   from django.db.models import Func

   # 示例：使用 Func 类执行数据库函数，将 name 字段值转为大写
   class Upper(Func):
       function = 'UPPER'

   queryset = MyModel.objects.annotate(upper_name=Upper('name'))
   ```

4. **`Value()` 类：** 用于插入常量值到查询中。

   ```python
   from django.db.models import Value

   # 示例：插入常量值到查询中
   queryset = MyModel.objects.annotate(constant=Value(42))
   ```

5. **`Case()` 类：** 用于执行条件语句。

   ```python
   from django.db.models import Case, When
   
   # 示例：根据条件执行不同的逻辑
   queryset = MyModel.objects.annotate(
       status_label=Case(
           When(status='A', then=Value('Active')),
           When(status='I', then=Value('Inactive')),
           default=Value('Unknown'),
           output_field=CharField(),
       )
   )
   ```

这些表达式类可以在查询中灵活地组合和使用，使你能够构建更复杂的查询逻辑。在编写复杂查询时，参考 Django 的官方文档和数据库后端文档以确保你使用的表达式类在你的数据库中受支持。



## 十四.注释对象

在 Django 中，注释（annotating）是指为查询集中的每个对象添加额外的字段，这些字段可以是某种计算、聚合结果或其他数据库操作的输出。注释通过使用 `annotate()` 方法来实现。

以下是一个简单的例子，假设你有一个模型 `Book`，其中包含了一些书籍的价格信息：

```python
# models.py
from django.db import models

class Book(models.Model):
    title = models.CharField(max_length=100)
    price = models.DecimalField(max_digits=5, decimal_places=2)
```

如果你想为每本书籍添加一个字段，表示该书的价格与所有书籍价格的平均值的差异，你可以使用 `annotate()` 方法：

```python
# views.py
from django.db.models import F, Avg

average_price = Book.objects.aggregate(average_price=Avg('price'))

books_with_difference = Book.objects.annotate(price_difference=F('price') - average_price['average_price'])
```

在这个例子中，`annotate()` 方法接受一个参数，该参数为新注释字段的定义。在这里，我们使用 `F` 对象表示模型字段，计算每本书的价格与平均价格的差异，并将结果存储在名为 `price_difference` 的新字段中。

你还可以进行其他类型的注释，例如聚合注释，其中你可以使用聚合函数对相关的外键集合进行注释：

```python
# views.py
from django.db.models import Count

authors_with_book_count = Author.objects.annotate(book_count=Count('book'))
```

在这个例子中，我们使用 `Count` 函数注释了每个作者对象，添加了一个名为 `book_count` 的新字段，该字段表示每个作者的书籍数量。

注释提供了一种强大的方式来在查询时为每个对象添加额外的信息，使得在模板或视图中更容易处理数据。

### 实例:

**在使用注释函数时需要值表达时**

```python
from django.shortcuts import render
from django.db.models import Value
from store.models import Product,Customer


def say_hello(request):                     
    queryset = Customer.objects.annotate(is_new =Value(True))


    return render(request, 'hello.html', {'name': 'Mosh', 'result' : list(queryset)})

```

**实例二**

```python
from django.shortcuts import render
from django.db.models import Value,F
from store.models import Product,Customer


def say_hello(request):                      
    queryset = Customer.objects.annotate(is_id =F('id'))


    return render(request, 'hello.html', {'name': 'Mosh', 'result' : list(queryset)})

```

## 十五.调用数据库功能

在Django中，你可以使用 `Func()` 类和 `F()` 对象来调用数据库函数。这些函数用于执行数据库特定的操作，例如在查询中进行字符串拼接、日期计算等。

以下是一些使用 `Func()` 类和 `F()` 对象的示例：

### 使用 `Func()` 类：

```python
from django.db.models import F, Func

# 示例：将数据库中的字符串字段转为大写
class Upper(Func):
    function = 'UPPER'

# 使用 Upper 函数将 name 字段的值转为大写
queryset = Customer.objects.annotate(upper_name=Upper('name'))
```

在这个例子中，`Upper` 类继承自 `Func` 类，它表示执行数据库的 `UPPER` 函数。通过 `annotate` 方法，我们为每个 `Customer` 对象添加了一个新的注释字段 `upper_name`，该字段的值是 `name` 字段的大写形式。

### 使用 `F()` 对象：

```python
from django.db.models import F, Value, CharField

# 示例：将两个字段的值进行字符串拼接
queryset = Customer.objects.annotate(
    full_name=F('first_name') + Value(' ') + F('last_name'), output_field=CharField())
```

在这个例子中，`F('first_name') + Value(' ') + F('last_name')` 使用 `F()` 对象表示数据库字段，并通过 `+` 运算符进行字符串拼接。通过 `annotate` 方法，我们为每个 `Customer` 对象添加了一个新的注释字段 `full_name`，该字段的值是 `first_name`、空格和 `last_name` 三者的字符串拼接。

在Django的`annotate()`方法中，**`output_field`参数用于指定注释字段的数据类型**。在你的例子中：

```python
queryset = Customer.objects.annotate(full_name=F('first_name') + Value(' ') + F('last_name'), output_field=CharField())
```

`output_field=CharField()` 表示 `full_name` 字段的数据类型是字符型（CharField）。这是因为在执行字符串拼接时，Django 需要知道最终结果的数据类型，以便正确地处理和存储结果。

如果不指定 `output_field`，Django 会尝试自动推断最终结果的数据类型，但有时可能无法准确推断，特别是在复杂的查询中。为了确保数据类型的一致性和正确性，最好显式地指定 `output_field`。

这些是一些简单的示例，你可以根据具体的数据库函数和操作来构建自己的查询。在使用这些函数时，确保了解你的数据库支持的函数和语法。

### 十六.数据分组 Group by

在Django中，你可以使用`annotate()`和`values()`方法结合使用来进行数据分组。下面是一个简单的例子：

假设你有一个模型`Order`，表示订单，其中包含订单号、总价等信息：

```python
# models.py
from django.db import models

class Order(models.Model):
    order_number = models.CharField(max_length=100)
    total_price = models.DecimalField(max_digits=5, decimal_places=2)
    customer = models.ForeignKey(Customer, on_delete=models.CASCADE)
    # 其他字段...
```

现在，如果你想按照客户分组，计算每个客户的订单总价的平均值，可以这样做：

```python
# views.py
from django.db.models import Avg

# 获取每个客户的订单总价的平均值
average_order_price_by_customer = Order.objects.values('customer__name').annotate(average_price=Avg('total_price'))
```

- `Order.objects.values('customer__name')`：这部分表示从 `Order` 模型中选择字段，具体是选择 `customer__name` 字段。这相当于一个 SQL 中的 GROUP BY 子句，它告诉数据库你想要按照 `customer__name` 字段进行分组。
- `.annotate(average_price=Avg('total_price'))`：这部分使用 `annotate` 方法，它告诉 Django 在每个分组上进行注释。具体地，在每个分组中，它计算了 `total_price` 字段的平均值，并将结果存储在一个新的字段 `average_price` 中。

综合起来，这段代码的作用是查询订单 (`Order` 模型) 数据，按照客户名 (`customer__name` 字段) 进行分组，并对每个分组计算订单总价 (`total_price` 字段) 的平均值。结果存储在 `average_order_price_by_customer` 变量中，这个变量是一个包含每个客户平均订单总价的查询集。

这样，`average_order_price_by_customer`将是一个包含每个客户平均订单总价的查询集，你可以在模板中或其他地方使用这个数据。

请根据你的具体模型和需求进行适当的调整，以满足你的数据分组和聚合的要求。

### 实例

```python
from django.shortcuts import render
from django.db.models import Count
from store.models import Customer


def say_hello(request):
    queryset = Customer.objects.annotate(
        orders_count = Count('order')
    )

    return render(request, 'hello.html', {'name': 'Mosh', 'result' : list(queryset)})
```

## 十六.使用表达式包装器

Django提供了表达式包装器，以更方便、可读的方式处理查询中的表达式。一些常见的表达式包装器包括`F()`、`Value()`和`ExpressionWrapper()`。

以下是每个表达式包装器的简要概述：

1. **`F()` 对象:**
   - `F()` 对象允许您在查询中引用数据库列的值。
   - 用于在列之间执行操作或比较值。
   - 示例：
     ```python
     from django.db.models import F
     
     # 对所有记录的 'quantity' 值增加 1
     queryset = Product.objects.update(quantity=F('quantity') + 1)
     ```

2. **`Value()` 对象:**
   - `Value()` 对象表示可在查询中使用的常量值。
   - 用于将常量值插入查询表达式。
   - 示例：
     ```python
     from django.db.models import Value
     
     # 将常量值 42 插入所有记录的 'score' 字段
     queryset = Student.objects.update(score=Value(42))
     ```

3. **`ExpressionWrapper()` 类:**  
   
   - `ExpressionWrapper()` 允许您将各种数据库表达式应用于字段。
   - 提供对表达式应用的更多控制。
   - 示例：
     ```python
     from django.db.models import ExpressionWrapper, F, IntegerField
     
     # 创建一个计算折扣价格的表达式
     expression = ExpressionWrapper(F('price') * 0.9, output_field=IntegerField())
     
     # 用折扣价格注释查询集
     queryset = Product.objects.annotate(discounted_price=expression)
     ```

**ExpressionWrapper() 类定义结果的类型，当两类型不同进行计算时，可以定义结果类型**

## 十七.查询通用关系

```python
from django.shortcuts import render
from django.contrib.contenttypes.models import ContentType
from store.models import Product
from tags.models import TaggedItem

def say_hello(request):
    content_type = ContentType.objects.get_for_model(Product)

    queryset = TaggedItem.objects \
        .select_related('tag') \
        .filter(
            content_type = content_type,
            object_id = 1
        )

    return render(request, 'hello.html', {'name': 'Mosh', 'tags' : list(queryset)})

```

这是一个Django视图函数，其目的是从数据库中检索有关特定产品的标签信息，并将结果传递给名为'hello.html'的模板进行渲染。下面是对代码的解释：

1. **导入模块**：
   ```python
   from django.shortcuts import render
   from django.contrib.contenttypes.models import ContentType
   from store.models import Product
   from tags.models import TaggedItem
   ```
   - `render`: 用于将视图的输出渲染到模板。
   - `ContentType`: 用于获取模型的ContentType，以便创建通用关系。
   - `Product`: 假设是来自`store`应用的产品模型。
   - `TaggedItem`: 用于存储标签与其他模型实例的关联信息。

3. **获取ContentType**:
   ```python
   content_type = ContentType.objects.get_for_model(Product)
   ```
   - 使用`get_for_model`方法获取`Product`模型的ContentType。ContentType用于将模型与通用关系关联。

4. **构建查询**:
   
   ```python
   queryset = TaggedItem.objects \
       .select_related('tag') \
       .filter(
           content_type=content_type,
           object_id=1
       )
   ```
   - 构建一个查询，使用`select_related`来获取与标签关联的实际标签对象（假设`TaggedItem`模型中有一个名为`tag`的外键字段）。
   - 使用`filter`方法过滤结果，仅选择`content_type`为`Product`且`object_id`为1的标签项。
   
   **这里的object_id 表示你正在查找与 `Product` 模型中主键（ID）为 1 的特定产品相关联的标签项。**

## 十八.自定义管理器

在Django中，管理器（Manager）是模型的一个类属性，为查询数据库提供了方便的接口。自定义管理器允许你为特定模型自定义查询的方式。以下是有关Django自定义管理器的简要概述：

### 默认管理器：
默认情况下，每个Django模型都会得到一个名为`objects`的管理器。这个管理器负责数据库查询，用于从数据库中检索模型的实例。

### 自定义管理器：
你可以通过定义一个新类并继承`django.db.models.Manager`来创建自己的自定义管理器。然后，你可以将这个自定义管理器添加到你的模型中。

下面是一个示例：

```python
from django.db import models

class CustomManager(models.Manager):
    def get_queryset(self):
        # 根据需要自定义查询集
        return super().get_queryset().filter(is_published=True)

class MyModel(models.Model):
    # 你的模型字段在这里

    # 将自定义管理器添加到模型中
    objects = CustomManager()
```

在这个示例中，`CustomManager`是一个自定义管理器，它覆盖了`get_queryset`方法，以仅过滤已发布的对象（`is_published=True`）。这允许你使用这个管理器只检索模型实例的特定子集。

### 使用自定义管理器：
一旦为模型定义了自定义管理器，你可以在查询中使用它：

```python
# 使用自定义管理器只检索已发布的实例
published_objects = MyModel.objects.all()
```

总的来说，在Django中，自定义管理器和自定义查询集提供了一种方式来封装和重用对模型的常见查询逻辑。当你发现自己在应用程序的不同部分频繁进行类似的查询时，它们特别有用。

### 实例

这个代码片段包含了一个自定义管理器（`TaggedItemManage`）和一个使用该管理器的视图函数（`say_hello`）。下面是对这些代码的解释：

#### 在`models.py`文件中：

```python
# models.py

from django.contrib.contenttypes.models import ContentType
from django.db import models

class TaggedItemManage(models.Model):
    def get_tags_for(self, obj_type, obj_id):
        content_type = ContentType.objects.get_for_model(obj_type)

        return TaggedItem.objects \
            .select_related('tag') \
            .filter(
                content_type=content_type,
                object_id=obj_id
            )

class TaggedItem(models.Model):
    objects = TaggedItemManage()
```

1. `TaggedItemManage` 类是一个继承自 `models.Model` 的类，它充当了 `TaggedItem` 模型的自定义管理器。
2. `get_tags_for` 方法是一个用于获取与给定对象类型和对象ID相关的标签项的自定义方法。
3. 在方法内部，使用 `ContentType` 来获取给定对象类型的内容类型，然后使用 `select_related` 来选择与标签项关联的标签，并使用 `filter` 过滤特定的对象类型和对象ID。

#### 在`views.py`文件中：

```python
# views.py

from django.shortcuts import render
from store.models import Product
from tags.models import TaggedItem

def say_hello(request):
    queryset = TaggedItem.objects.get_tags_for(Product, 1)

    return render(request, 'hello.html', {'name': 'Mosh', 'tags': list(queryset)})
```

1. `say_hello` 视图函数是一个简单的 Django 视图，它使用上述在 `models.py` 中定义的自定义管理器来检索与 `Product` 类型和 ID 为 1 的对象相关的标签项。
2. 查询结果存储在 `queryset` 变量中，并传递给模板以供渲染。

### 相关解释：

- 这个设计的目的是在 `TaggedItem` 模型中使用自定义管理器，使其能够提供更特定的查询接口，而不仅仅是通用的 `objects` 管理器。
- 在视图函数中，`say_hello` 函数使用 `TaggedItem` 模型的自定义管理器的 `get_tags_for` 方法，传递了一个 `Product` 类型和一个对象ID（这里是1），以获取与该产品相关的标签项。
- 最后，查询结果传递给模板进行渲染。

这样的设计使得模型的查询逻辑更清晰，同时提供了更高层次的抽象，可以在整个应用程序中重复使用。

## 十九.连接查询集缓存

在Django中，查询集缓存是指在一次请求中多次使用相同的查询集时，Django会自动对数据库查询的结果进行缓存，避免多次查询数据库，提高性能。这是通过Django的 ORM（对象关系映射）系统实现的。

当你多次对同一个查询集进行查询时，Django会在内存中缓存第一次查询的结果，然后在后续查询中直接返回缓存的结果，而不再向数据库发送相同的查询。

下面是一个简单的示例：

```python
# models.py
from django.db import models

class Book(models.Model):
    title = models.CharField(max_length=100)
    author = models.CharField(max_length=50)
```

```python
# views.py
from django.shortcuts import render
from .models import Book

def book_list(request):
    # 第一次查询，将结果缓存
    books_query = Book.objects.filter(author='John Doe')
    books = list(books_query)

    # 第二次查询，直接返回缓存的结果，而不再向数据库发送查询
    other_books_query = Book.objects.filter(author='John Doe')
    other_books = list(other_books_query)

    return render(request, 'book_list.html', {'books': books, 'other_books': other_books})
```

在这个例子中，第一次查询使用 `Book.objects.filter(author='John Doe')` 获取了作者为'John Doe'的书籍列表，并将结果缓存。接下来的查询使用相同的查询集 `Book.objects.filter(author='John Doe')`，但它不会再次向数据库发送查询，而是直接返回第一次查询的缓存结果。

Django的查询集缓存对于减少数据库查询次数、提高性能以及避免不必要的重复查询非常有帮助。但需要注意的是，查询集缓存仅在同一个请求周期内有效，不同的请求之间不共享缓存。

## 创建对象

在Django中，要创建一个模型的对象（即数据库中的一条记录），你可以使用模型的`create`方法或者通过实例化模型对象并保存来实现。

### 实例化对象并保存：

你也可以通过实例化模型对象、设置字段的值，然后调用`save`方法来保存到数据库。

```python
from yourapp.models import YourModel

# 实例化模型对象
obj = YourModel()

# 设置字段的值
obj.field1 = value1
obj.field2 = value2

# 保存对象到数据库
obj.save()
```

这样更好，当表中列名被改变时，这里面的名字也会跟着改变

## 更新对象

在Django中，要更新模型的对象（即数据库中的一条记录），你可以使用模型的 `update` 方法或者通过实例化模型对象、修改字段的值，然后调用 `save` 方法来实现。以下是这两种方法的示例：

### 使用 `update` 方法：

`update` 方法是 `QuerySet` 对象上的一个方法，用于在数据库中更新匹配某个条件的多个对象。这是一个批量更新的方法，如果你只想更新一个对象，可以在查询中使用 `filter` 条件来确保只匹配到一个对象。

```python
from yourapp.models import YourModel

# 使用 update 方法批量更新匹配条件的对象
YourModel.objects.filter(your_filter_condition).update(field1=new_value1, field2=new_value2)
```

**创建对象用实例化对象保存，更新对象用update方法更新**

## 删除对象

在Django中，要删除模型的对象（即数据库中的一条记录），你可以使用模型的 `delete` 方法或者通过实例化模型对象，然后调用 `delete` 方法来实现。

### 使用 `delete` 方法：

`delete` 方法是 `QuerySet` 对象上的一个方法，用于在数据库中删除匹配某个条件的多个对象。同样，这是一个批量删除的方法，如果你只想删除一个对象，可以在查询中使用 `filter` 条件来确保只匹配到一个对象。

```python
from yourapp.models import YourModel

# 使用 delete 方法批量删除匹配条件的对象
YourModel.objects.filter(your_filter_condition).delete()
```

## 事务

在Django中，事务（transactions）是一种管理数据库操作的机制，它确保一系列相关的数据库操作要么全部成功提交（持久化到数据库），要么全部回滚（不进行持久化）。这确保了数据库的一致性和完整性。

在Django中，你可以使用 `django.db.transaction` 模块来处理事务。通常，事务会自动开始，但在一些情况下，你可能需要手动管理事务。以下是一些关于事务的基本概念和使用方法：

### 自动事务：

Django 的数据库操作通常在请求处理中自动包含在事务中。也就是说，当请求开始时，Django 会自动启动一个事务，当请求处理完成时，如果没有错误发生，它会自动提交事务。如果有错误发生，事务将被回滚。

### 手动事务：

在某些情况下，你可能需要手动管理事务，特别是在需要进行多个数据库操作的复杂场景。以下是手动事务的基本用法：

```python
from django.db import transaction

def my_view(request):
    try:
        with transaction.atomic():
            # 在这里进行数据库操作
            # 如果任何一个操作失败，整个事务将被回滚
            obj1.save()
            obj2.save()
    except Exception as e:
        # 处理错误
        pass
```

在上面的例子中，`transaction.atomic()` 创建了一个原子操作，它包装了在其中执行的所有数据库操作。如果其中任何一个操作引发异常，整个事务将被回滚。如果所有操作成功完成，事务将被提交。

### 嵌套事务：

Django 支持嵌套事务，但是嵌套事务的行为依赖于数据库后端的支持。通常，如果你在一个已经在事务中的上下文中启动了一个新的事务，那么这个新的事务将被视为保存点（savepoint）。如果内部事务失败，将会回滚到最近的保存点而不是整个事务。

```python
from django.db import transaction

def my_view(request):
    try:
        with transaction.atomic():
            # 外部事务

            with transaction.atomic(savepoint=True):
                # 内部事务
                # 如果内部事务失败，将回滚到保存点
                obj1.save()
                obj2.save()
    except Exception as e:
        # 处理错误
        pass
```

在这个例子中，如果内部事务失败，只会回滚到内部事务开始的地方，而不是整个事务。

事务的使用可以确保你的数据库操作是原子的，从而避免了因为一部分操作成功而一部分失败导致的数据不一致的问题。在开发中，确保了良好的事务管理是保障数据完整性和一致性的关键。

## 执行原始SQL查询

在Django中，你可以使用 `django.db.connection` 对象来执行原始的 SQL 查询。这允许你执行自定义的 SQL 语句，但要注意潜在的 SQL 注入风险，确保在构建 SQL 查询时正确地转义参数。

以下是一个简单的例子，展示如何执行原始的 SQL 查询：

```python
from django.db import connection

def execute_raw_sql():
    # 定义 SQL 查询语句
    sql_query = "SELECT * FROM your_table WHERE your_condition = %s"

    # 定义查询参数
    params = ['some_value']

    # 使用 cursor 执行原始 SQL 查询
    with connection.cursor() as cursor:
        cursor.execute(sql_query, params)

        # 获取查询结果
        result = cursor.fetchall()

    return result
```

在这个例子中：

- `sql_query` 是你的原始 SQL 查询语句，其中 `%s` 是占位符，表示一个参数。
- `params` 是查询参数，它是一个列表，包含了要替换占位符的实际值。
- `connection.cursor()` 会创建一个数据库游标，通过游标执行 SQL 查询。
- `cursor.execute(sql_query, params)` 用于执行 SQL 查询，`params` 中的值将替换占位符。
- `cursor.fetchall()` 获取查询结果。

请注意，使用原始 SQL 查询通常是不推荐的，因为它可能导致代码的可移植性下降，并增加了 SQL 注入的风险。在大多数情况下，使用 Django 的 ORM 查询是更安全和更可维护的选择。只有在一些复杂的查询或者需要进行一些数据库特定操作时，才考虑使用原始 SQL 查询。



# Admin Site

Django 的 Admin 网站是一个内置的 Web 管理界面，它允许你轻松地管理你的 Django 应用的后台数据。通过 Admin 网站，你可以执行一系列操作，如查看、添加、编辑和删除数据库中的记录，而无需手动编写自定义的管理页面或者数据库管理工具。

Admin 网站的主要特点包括：

1. **自动生成管理界面：** Django 的 Admin 网站可以根据你的模型（Model）自动生成管理页面，包括列表视图、详细视图、编辑视图等。

2. **定制化：** 你可以通过自定义 `admin.py` 文件来定制 Admin 网站的外观和行为。你可以添加额外的字段、过滤器、搜索功能等，以满足你的需求。

3. **用户权限控制：** Admin 网站支持用户认证和权限控制。你可以通过 Django 的认证系统为用户分配不同的权限，以控制他们在 Admin 网站上的操作。

4. **集成应用程序：** Admin 网站可以集成到你的应用程序中，让你能够直接通过浏览器管理数据库。

要启用 Admin 网站，你需要在你的应用的 `admin.py` 文件中注册你的模型。以下是一个简单的例子：

```python
# 在你的应用的 admin.py 文件中

from django.contrib import admin
from .models import YourModel

# 注册你的模型
admin.site.register(YourModel)
```

这样，你就可以访问 `http://yourdomain.com/admin/`，并使用你的超级用户凭据登录到 Admin 网站。在那里，你将看到一个管理界面，其中包含了你注册的模型的列表视图，并且你可以执行各种操作。

Admin 网站是一个方便的工具，特别适用于快速原型开发和小型应用程序。对于更复杂的管理需求，你可能需要考虑构建自定义管理界面或者使用第三方管理工具。



## 一.注册模型

在Django中，要在Admin网站中注册模型，你需要在应用的`admin.py`文件中进行注册。注册模型后，你就可以通过Admin网站管理界面对该模型进行增删改查等操作。以下是一个简单的示例：

```python
# 在你的应用的 admin.py 文件中

from django.contrib import admin
from .models import YourModel1, YourModel2

# 注册模型
admin.site.register(YourModel1)
admin.site.register(YourModel2)
```

在这个例子中，假设你的应用中有两个模型，分别是`YourModel1`和`YourModel2`。通过`admin.site.register`将它们注册到Admin网站。

如果你想要更多的控制，你可以创建一个继承自`admin.ModelAdmin`的自定义模型管理类，并在注册时使用这个类。这样，你可以定制Admin网站上模型的显示、过滤、搜索等属性。

```python
# 在你的应用的 admin.py 文件中

from django.contrib import admin
from .models import YourModel

class YourModelAdmin(admin.ModelAdmin):
    list_display = ('field1', 'field2', 'field3')
    list_filter = ('field1', 'field2')
    search_fields = ('field1', 'field2')

# 注册模型并关联自定义模型管理类
admin.site.register(YourModel, YourModelAdmin)
```

在这个例子中，`YourModelAdmin` 是一个自定义的模型管理类，定义了一些在Admin网站上显示的配置，包括`list_display`（显示的字段）、`list_filter`（过滤器）和`search_fields`（搜索字段）。然后，通过`admin.site.register`将模型和自定义模型管理类关联起来。

这样注册模型后，你就可以在Admin网站上对相应的模型进行管理了。

### 返回一个可读性较好的字符串表示

在Django的模型中，`__str__` 方法定义了模型实例在被转换成字符串时的行为。通常，这个方法用于返回一个可读性较好的字符串表示，以便在管理界面或者其他地方展示模型实例的信息。

在你提供的代码中：

```python
def __str__(self) -> str:
    return self.title
```

这个 `__str__` 方法返回了模型实例的 `title` 字段的值。因此，当你在需要字符串表示的时候，Django 将调用这个方法，并返回相应的标题字符串。

假设你有一个名为 `collection` 的 `Collection` 模型实例：

```python
collection = Collection.objects.get(pk=1)
print(collection)
```

上述代码中，`print(collection)` 实际上会调用 `collection.__str__()` 方法，由于你在 `__str__` 方法中返回的是 `self.title`，因此会打印出该 `Collection` 实例的标题字符串。

这样的设计有助于在Django的管理界面、shell、日志输出等地方更容易理解和识别模型实例。当你需要以字符串形式表示模型实例时，Django会自动调用 `__str__` 方法，提供更好的可读性。

### 模型的元数据中定义了排序规则

在 Django 的模型中，`Meta` 类用于提供模型的元数据（metadata），其中 `ordering` 是其中一个常用的选项。

在你提供的代码中：

```python
class Meta:
    ordering = ['title']
```

这表示你在模型的元数据中定义了排序规则。具体来说，它告诉 Django 在执行查询时按照 `title` 字段的升序进行排序。也就是说，当你从数据库中检索这个模型的对象时，它们将按照 `title` 字段的字母顺序进行排列。

这在许多情况下是很有用的，尤其是当你在Django管理界面或者其他地方查看对象列表时，它们以某种方式有序，而不是以任意的顺序显示。

你可以通过使用 `'-'` 符号来指定降序排序，例如：

```python
class Meta:
    ordering = ['-title']
```

这将按照 `title` 字段的降序进行排序。你还可以同时使用多个字段进行排序，例如：

```python
class Meta:
    ordering = ['title', 'date_created']
```

这将首先按照 `title` 字段进行升序排序，然后按照 `date_created` 字段进行升序排序。

## 二.自定义列表界面

在Django的Admin网站中，你可以通过自定义`ModelAdmin`类来自定义模型的列表界面。以下是一个简单的例子，演示如何自定义列表界面

### 实例

```python
@admin.register(models.Product)
class ProductAdmin(admin.ModelAdmin):
    list_display = ['title' , 'unit_price']
    list_editable = ['unit_price']
    list_per_page = 10

```

可以浏览这个网页查看`ModelAdmin option`   https://docs.djangoproject.com/zh-hans/4.2/ref/contrib/admin/#modeladmin-options 

查看很多设置网页很便利的方法

## 三.添加计算列

```python
@admin.register(models.Product)
class ProductAdmin(admin.ModelAdmin):
    list_display = ['title' , 'unit_price','inventory_status']
    list_editable = ['unit_price']
    list_per_page = 10

    @admin.display(ordering='inventory') 
    def inventory_status(self, product):
        if product.inventory < 10 :
            return 'Low'
        return 'OK'
```

在这个例子中：

- `list_display` 中添加了一个名为 `inventory_status` 的字段，这是通过 `@admin.display` 装饰器定义的自定义方法。
- `@admin.display(ordering='inventory')` 设置了默认的排序规则，按照 `inventory` 字段升序排序。
- `inventory_status` 方法接收一个模型实例 `obj`（这里假设模型有一个名为 `inventory` 的字段），根据 `inventory` 字段的值返回 `'Low'` 或 `'OK'`，表示库存状态。
- `inventory_status.short_description` 设置了这个列的显示名称，这样它会在 Admin 网站上以 'Inventory Status' 的名字显示。

通过这个配置，你可以在 Django Admin 的列表页面上看到并根据 `inventory` 字段的值显示 `'Low'` 或 `'OK'` 的库存状态，并且这一列可以根据库存字段排序。

## 四.选择相关对象(连接其他模型)

在 Django 的 Admin 中，你可以使用 `list_select_related` 属性来优化查询性能，以减少数据库查询的数量。这在你需要在列表页面显示关联对象的字段时特别有用。

### 实例

```python
@admin.register(models.Product)
class ProductAdmin(admin.ModelAdmin):
    list_display = ['title' , 'unit_price','inventory_status','collection_title']
    list_editable = ['unit_price']
    list_per_page = 10
    list_select_related = ['collection']

    def collection_title(self,product):
        return product.collection.title
```

确保你真正需要在列表中显示的关联对象，以避免不必要的性能开销。

### 实例

```python
#在admin.py
@admin.register(models.Order)
class OrderAdmin(admin.ModelAdmin):
    list_display = ['id','placed_at','customer']
    list_per_page = 10
    list_select_related = ['customer']
 
 #在model.py
 class Customer(models.Model):
    .....其他代码
    
    def __str__(self) -> str:
        return f'{self.first_name} {self.last_name}'
    
    class Meta:
        ordering = ['first_name', 'last_name']
```

## 五.覆盖基本查询集

**类似于在一个模型中添加一个字段**

在 Django 的 `admin.py` 文件中，你可以通过覆盖模型的默认查询集（默认使用 `objects`）来定制 Admin 中的数据展示。具体来说，你可以在模型的 `ModelAdmin` 类中使用 `get_queryset` 方法来实现这个目标。

```python
@admin.register(models.Collection)
class CollectionAdmin(admin.ModelAdmin):
    list_display = ['title','products_count']
    
    def products_count(self,collection):
        return collection.products_count
    
    def get_queryset(self,request):
        return super().get_queryset(request).annotate(
            products_count = Count('product')
        )

```

**`def get_queryset(self, request):`：**

- 覆盖了 `get_queryset` 方法，该方法用于获取模型的默认查询集。在这里，使用了 `super().get_queryset(request).annotate(products_count=Count('product'))`，对默认查询集进行了扩展。具体来说，通过 `annotate` 方法，对每个集合进行了一个额外的计数操作，计算关联的产品数量，并将结果存储在一个名为 `products_count` 的新字段中。

通过以上配置，你在 Django Admin 中查看 `Collection` 模型列表时将会显示标题 (`title`) 和产品数量 (`products_count`)。这样，你就能够方便地了解每个集合关联的产品数量。

## 六.提供其他网页的链接

```python
#需要导入模块
from django.utils.html import format_html

@admin.register(models.Collection)
class CollectionAdmin(admin.ModelAdmin):
    list_display = ['title','products_count']
    
    @admin.display(ordering='products_count')
    def products_count(self,collection):
        return format_html('<a href="http://google.com">{}</a>', collection.products_count)
    
    def get_queryset(self,request):
        return super().get_queryset(request).annotate(
            products_count = Count('product')
        )
```

这样就可以在products_count实例中点击链接 ，进入http://google.com

### 构建一个链接到 Django Admin 中产品列表页的 URL

```python
from typing import Any
from django.contrib import admin
from django.utils.html import format_html ,urlencode
from django.urls import reverse
from django.db.models import Count
from . import models

@admin.register(models.Collection)
class CollectionAdmin(admin.ModelAdmin):
    list_display = ['title','products_count']
    
    @admin.display(ordering='products_count')
    def products_count(self,collection):
            # reverse('admin:app_model_page')
            url =(
                reverse('admin:store_product_changelist') 
                + '?'
                + urlencode({
                    'collection__id' : str(collection.id)
                }))
            return format_html('<a {}">{}</a>', url , collection.products_count)
    
    def get_queryset(self,request):
        return super().get_queryset(request).annotate(
            products_count = Count('product')
        )
```

这段代码是在 Django Admin 中自定义 `Collection` 模型的显示，特别是在列表页上添加了一个带有链接的产品计数字段。让我解释一下其中的关键部分：

1. **`@admin.display(ordering='products_count')`：**
   - 使用了 `@admin.display` 装饰器，指定了在列表页中显示的字段或方法。`ordering='products_count'` 用于指定该字段在列表页上的默认排序顺序，这里是按照 `products_count` 字段排序。

2. **`def products_count(self, collection):`：**
   - 定义了一个名为 `products_count` 的方法，该方法用于显示在列表页中的产品计数字段。
   - 使用了 `reverse('admin_store_product_changelist')` 构建了到产品列表页的 URL。`admin_store_product_changelist` 部分是一个特定于你的应用的 URL 名称，它指向了产品列表页。
   - 使用 `urlencode` 构建了包含查询参数的 URL。在这里，它添加了一个名为 `collection__id` 的查询参数，值为当前集合的 `id`。
   - 使用 `format_html` 构建了一个 HTML 格式的字符串，其中包含一个链接，链接的目标是上面构建的 URL。链接的显示文本为当前集合的产品数量。

3. **`return format_html('<a {}">{}</a>', url , collection.products_count)`：**
   - 返回了一个 HTML 字符串，其中包含一个链接，链接的目标是构建的产品列表页的 URL，显示文本为当前集合的产品数量。

通过这个定制，你在 Django Admin 中的 `Collection` 模型列表页上将会看到一个可以点击的链接，点击该链接将导航到与该集合相关的产品列表页。这个链接的文本是当前集合的产品数量。而且，该字段默认按照产品数量排序。

明白了，让我用更简单的语言解释这段代码。

```python
url = (
    reverse('admin:store_product_changelist')  # 构建产品列表页的URL
    + '?'  # 在URL后面加上问号，表示接下来是查询参数
    + urlencode({'collection__id': str(collection.id)})  # 把集合ID作为查询参数加入URL
)
```

这段代码做了以下事情：

1. **`reverse('admin_store_product_changelist')`**：
   - 创建了一个指向 Django Admin 中产品列表页的链接。

2. **`'?'`**：
   - 在链接的末尾加上了一个问号，表示接下来会添加查询参数。

3. **`urlencode({'collection__id': str(collection.id)})`**：
   - 把当前集合的ID添加为查询参数，确保它以URL安全的方式传递。

最终，这个`url`变量包含一个链接，点击该链接会导航到 Django Admin 中的产品列表页，并且只显示与当前集合相关的产品。这个链接被用于创建一个HTML链接，其中包含在 `format_html` 函数调用中，以便在 Django Admin 的列表页上显示。

## 七.在列表页面添加搜索

```python
@admin.register(models.Customer)
class CustomerAdmin(admin.ModelAdmin):
    list_display = ['first_name','last_name','membership']
    list_editable = ['membership']
    ordering = ['first_name', 'last_name']
    list_per_page = 10
    search_fields = ['first_name__istartswith','last_name__istartswith'] 
```

在Django的`admin.py`文件中，`search_fields`用于定义在Django管理后台的模型列表页面上的搜索框中可以搜索的字段。在你提供的例子中：

```python
search_fields = ['first_name__istartswith', 'last_name__istartswith']
```

这里的`search_fields`设置为一个包含两个字符串的列表。每个字符串都是一个字段的名称，用于指定在搜索框中进行搜索的字段。具体而言，这两个字段分别是`first_name`和`last_name`。

- `'first_name__istartswith'`: 这表示在`first_name`字段上进行搜索，并且使用`istartswith`来进行搜索。`istartswith`是Django的查询表达式之一，表示搜索以指定的字符串开头的数据，并且不区分大小写。这意味着搜索时不考虑字符串的大小写，例如，如果输入"john"，将匹配"John"或"johnny"等。

- `'last_name__istartswith'`: 同样，这表示在`last_name`字段上进行搜索，使用`istartswith`来进行搜索，同样是不区分大小写的。

这样配置后，当你在Django管理后台的`Customer`模型列表页 面上使用搜索框进行搜索时，系统将根据`first_name`和`last_name`字段的开头部分匹配来过滤结果。

## 八.在列表页面添加过滤功能

在Django管理后台的模型列表页面上添加过滤功能，可以让你根据某些条件对数据进行筛选。当你登录到Django管理后台并查看模型的列表页面时，你将看到一个位于页面右侧的侧边栏，其中包含一个可以用于过滤数据的下拉列表。选择过滤器中的选项将筛选出符合条件的数据。

```python
class inventoryFilter(admin.SimpleListFilter):
    title = 'inventory'
    parameter_name = 'inventory'

    def lookups(self, request, model_admin):
        return [
            ('<10','Low')
        ]
    def queryset(self, request, queryset:QuerySet):
        if self.value() == '<10' :
            return queryset.filter(inventory__lt = 10)


@admin.register(models.Product)
class ProductAdmin(admin.ModelAdmin):
    list_display = ['title' , 'unit_price','inventory_status','collection_title']
    list_editable = ['unit_price']
    list_filter = ['collection', 'last_update',inventoryFilter]  # 添加过滤器
    list_per_page = 10
    list_select_related = ['collection']

    def collection_title(self,product):
        return product.collection.title

    @admin.display(ordering='inventory') 
    def inventory_status(self, product):
        if product.inventory < 10 :
            return 'Low'
        return 'OK'
```

这段代码定义了一个自定义的过滤器 `inventoryFilter`，并在 `ProductAdmin` 中应用了这个过滤器。

1. **`class inventoryFilter(admin.SimpleListFilter):`：**
   - 这是一个继承自 `admin.SimpleListFilter` 的自定义过滤器类。它允许你创建一个简单的下拉列表过滤器，以便在 Django Admin 中过滤产品列表。
   - `title` 是过滤器显示的名称。
   - `parameter_name` 是用于构建 URL 查询参数的名称。

2. **`lookups(self, request, model_admin):`：**
   - 这个方法定义了过滤器的选项。在这里，只有一个选项 `('<10', 'Low')`，表示产品库存低于 10 的情况。

3. **`queryset(self, request, queryset: QuerySet):`：**
   - 这个方法根据用户选择的过滤器选项修改查询集。在这里，如果用户选择了 '<10'，则返回库存低于 10 的产品。

4. **`@admin.register(models.Product):`：**
   - 使用 `@admin.register` 装饰器注册了 `Product` 模型，并定义了相应的管理类 `ProductAdmin`。

5. **`list_filter = ['collection', 'last_update', inventoryFilter]`：**
   - 在 `ProductAdmin` 中应用了过滤器。`list_filter` 是一个用于指定应该显示在右侧边栏的过滤器的列表。在这里，包括了集合 (`'collection'`)、最后更新时间 (`'last_update'`) 和自定义的库存过滤器 (`inventoryFilter`)。

6. **`@admin.display(ordering='inventory')`：**
   - 这个装饰器定义了一个用于在产品列表中显示库存状态的方法 `inventory_status`。在这里，如果库存低于 10，返回 'Low'，否则返回 'OK'。

通过这些设置，你在 Django Admin 中的产品列表页上可以看到一个用于过滤库存的下拉列表，并且产品的库存状态将以 'Low' 或 'OK' 的形式显示。

## 九.创建自定义操作



```python
@admin.register(models.Product)
class ProductAdmin(admin.ModelAdmin):
    actions = ['clear_inventory']
    ......
    
    @admin.action(description='Clear inventory')
    def clear_inventory(self , request,queryset):
        updated_count = queryset.update(inventory=0)
        self.message_user(
            request,
            f'{updated_count} product were successfully updated.'
        )

```

这段代码定义了一个名为 `clear_inventory` 的自定义操作。让我逐步解释这个代码块：

1. **`@admin.action(description='Clear inventory')`：**
   - 这是使用 `@admin.action` 装饰器定义的自定义操作。`description` 参数用于设置在管理员界面中显示的操作的名称。在这里，它被设置为 'Clear inventory'，表示清空库存的操作。

2. **`def clear_inventory(self, request, queryset):`：**
   - 这是实际执行清空库存操作的方法。`self` 是 `ProductAdmin` 的实例，`request` 包含了有关当前请求的信息，`queryset` 包含了选定的产品对象。

3. **`updated_count = queryset.update(inventory=0)`：**
   - 这行代码使用 `update` 方法将选定的产品的库存字段设置为 `0`。`queryset` 是一个包含选定产品的查询集。

4. **`self.message_user(request, f'{updated_count} product were successfully updated.')`：**
   - 这一行使用 `message_user` 方法向用户显示一条成功的消息。这个消息将在 Admin 界面的顶部显示。消息内容是一个字符串，包含被成功更新的产品数量。

总体而言，这段代码的作用是创建一个自定义操作，该操作会将选定的产品的库存字段设置为零，并向管理员显示一条成功的消息。管理员可以在产品列表页中选择一个或多个产品，然后使用下拉菜单中的 "Clear inventory" 操作执行此操作。

## 十.自定义表格

```python
@admin.register(models.Product)
class ProductAdmin(admin.ModelAdmin):
    autocomplete_fields = ['collection']
    prepopulated_fields = {
        'slug' : ['title']
    }
@admin.register(models.Collection)
class CollectionAdmin(admin.ModelAdmin):
    list_display = ['title','products_count']
    search_fields = ['title']
```

在这段代码中，`autocomplete_fields`、`prepopulated_fields` 和 `search_fields` 是 Django Admin 中用于定制管理界面的一些选项。

1. **`autocomplete_fields = ['collection']`：**
   - `autocomplete_fields` 允许你为指定的外键字段启用自动完成功能。在这里，`'collection'` 是 `Product` 模型中的一个外键字段，它指向 `Collection` 模型。启用自动完成后，你在管理页面中编辑 `Product` 对象时，可以通过输入 `Collection` 的标题来选择相关的集合，而不必在下拉框中浏览。

2. **`prepopulated_fields = {'slug': ['title']}`：**
   - `prepopulated_fields` 允许你根据其他字段的值自动填充目标字段的值。在这里，`'slug'` 是一个用于 URL 的字段，它会根据 `title` 字段的值进行自动填充。这样可以确保 URL 友好的字符串，避免手动输入。

3. **`search_fields = ['title']`：**
   - `search_fields` 定义了在管理页面上启用搜索功能的字段列表。在这里，设置了 `'title'`，这表示在 `Collection` 模型的管理页面上，你可以通过输入标题来搜索相应的集合。

这些选项都是为了提高在 Django Admin 中管理数据的效率和便利性。通过使用这些选项，你可以更轻松地定位和编辑相关的对象，并在输入数据时减少手动输入和错误。

## 十一.添加数据验证

在 Django Admin 中，你可以通过在模型的管理类中定义 `clean_` 方法来添加数据验证。这样的方法将在模型实例被保存之前执行，允许你在保存数据之前进行一些自定义验证。

下面是一个简单的例子，演示如何在 `Product` 模型中添加数据验证：

```python
from django.contrib import admin
from .models import Product

class ProductAdmin(admin.ModelAdmin):
    list_display = ['title', 'unit_price', 'inventory']

    def clean_title(self, value):
        # 在这里执行自定义的数据验证逻辑
        if len(value) < 5:
            raise forms.ValidationError('Title must be at least 5 characters long.')

        return value

admin.site.register(Product, ProductAdmin)
```

在这个例子中，我们在 `ProductAdmin` 中定义了一个 `clean_title` 方法，用于对 `title` 字段进行数据验证。在这里，我们检查了标题的长度，如果小于5个字符，就引发了一个 `forms.ValidationError`。

请注意，`clean_` 方法的命名约定是在字段名称之前加上 `clean_`。这样的方法将在保存模型实例之前被调用，允许你执行自定义的数据验证。

这只是一个简单的例子，你可以根据你的需求执行更复杂的验证逻辑。在执行验证时，如果有错误，你可以引发 `ValidationError`，该错误将被 Django Admin 捕获，并显示在管理界面上。

### 设置内容可为空

**在models.py文件中设置**

```python
class Product(models.Model):
    description = models.TextField(null=True,blank=True)
```

这代码片段定义了一个 Django 模型（Model）类，名为 `Product`。在这个模型中，有一个字段：

- **`description`：** 这是一个 `TextField` 类型的字段，用于存储产品的描述信息。`TextField` 是一个用于存储大段文本的字段类型，可以存储任意长度的文本数据。在这里，`description` 具有两个可选参数 `null=True` 和 `blank=True`。
- **`null=True`：** 表示数据库中此字段允许存储空值（NULL）。如果某个产品没有描述信息，它在数据库中的 `description` 字段可以为空。
  
- **`blank=True`：** 表示在 Django 表单中，此字段可以是空的。也就是说，当你在创建或编辑产品时，`description` 字段可以留空。

这样的设计允许在数据库中存储可选的产品描述，而且在创建或编辑产品时，你不必为 `description` 提供值。如果你提供了值，它将被存储在数据库中。如果你不提供值，数据库中的 `description` 字段将是空的。

###  数据不可以为负数

**在models.py文件中设置**

```python
from django.core.validators import MinValueValidator
class Product(models.Model):
     unit_price = models.DecimalField(
        max_digits=6,
        decimal_places=2,
        validators=[MinValueValidator(1)])
```

- **`validators=[MinValueValidator(1)]`：** 这里使用了 `validators` 参数，将一个 `MinValueValidator` 验证器添加到 `unit_price` 字段。`MinValueValidator(1)` 表示 `unit_price` 的最小值为1，即产品的单价不能低于1。

所以，这段代码确保了 `unit_price` 字段的数值在数据库中的范围是1到9999.99之间，且至少有两位小数。如果你尝试创建或更新 `Product` 对象时，提供的 `unit_price` 小于1，系统将抛出一个验证错误。这样做是为了确保存储在数据库中的价格是合理的数值。

## 十二.内联编辑

内联编辑（Inline Editing）是 Django Admin 中一种方便的功能，允许你在一个模型的编辑页面上直接编辑与之关联的另一个模型的相关数据。这通常用于处理模型之间的一对多或多对多关系。

以下是一个简单的例子，演示如何使用内联编辑：

假设你有两个模型，一个是 `Author`，另一个是 `Book`，它们之间是一对多的关系，一个作者可以有多本书。你可以使用内联编辑在编辑作者时直接编辑其关联的书。

```python
from django.contrib import admin
from .models import Author, Book

class BookInline(admin.TabularInline):  # 或者 admin.StackedInline
    model = Book
    extra = 1  # 允许添加的书的数量

@admin.register(Author)
class AuthorAdmin(admin.ModelAdmin):
    inlines = [BookInline]  # 将 BookInline 添加到 Author 的管理界面
    list_display = ['name']

@admin.register(Book)
class BookAdmin(admin.ModelAdmin):
    list_display = ['title', 'author', 'published_date']
```

在上述代码中：

- `BookInline` 类继承自 `admin.TabularInline`，用于创建一个嵌套在 `AuthorAdmin` 页面中的表格，用于编辑关联的书。你还可以使用 `admin.StackedInline`，这样会以堆叠的方式显示书的编辑表单。

- `inlines = [BookInline]` 将 `BookInline` 添加到 `AuthorAdmin` 的 `inlines` 属性中，告诉 Django Admin 在编辑作者时显示相关的书。

通过这样的设置，当你在编辑作者时，会在同一页上看到一个嵌套的书表格，可以直接在这个表格中添加、编辑或删除与作者相关联的书。这简化了管理相关模型之间关系的过程。

实例

```python
class OrderItemInline(admin.TabularInline):
    model = models.OrderItem
    autocomplete_fields = ['product']
    extra = 0
    min_num = 1
    max_num = 10


@admin.register(models.Order)
class OrderAdmin(admin.ModelAdmin):
    list_display = ['id','placed_at','customer']
    list_per_page = 10
    inlines = [OrderItemInline]
    list_select_related = ['customer']
    autocomplete_fields = ['customer']

```

- **`model = models.OrderItem`：** 指定了内联编辑的模型，即 `OrderItem` 模型。
- **`autocomplete_fields = ['product']`：** 使用了 `autocomplete_fields` 属性，表示在内联编辑中为 `OrderItem` 的 `product` 字段启用自动完成功能。这允许你通过输入产品的名称或其他关键字来选择相关的产品，而不是在下拉框中浏览。
- **`extra = 0`：** 设置了 `extra` 属性为 `0`，表示默认情况下不显示额外的空白行。这意味着在订单编辑页面中，一开始就显示一个订单关联的商品。
- **`min_num = 1` 和 `max_num = 10`：** 分别设置了最小和最大允许的 `OrderItem` 行数。这限制了在订单编辑页面中可以添加的商品数量，确保在合理的范围内。

## 十三.使用泛型关系

需要内联可以跟上面一样,不过需要导入的模块不一样

```python
from django.contrib.contenttypes.admin import GenericTabularInline
from tags.models import TaggedItem

class TagInline(GenericTabularInline):
    autocomplete_fields = ['tag']
    model = TaggedItem
@admin.register(models.Product)
class ProductAdmin(admin.ModelAdmin):
    inlines = [TagInline] 
```



## 十四.可插拔应用程序

在storefront项目中中为了独立构建和部署接口，我们不能在一个应用程序里出现其他应用程序模型，需要解耦

通过使用一个新的应用程序在里面导入两应用程序模型，在新应用程序中连接

因为应用能够轻松地被集成到不同的Django项目中。通过模型，开发者可以更容易地处理数据库操作，而不必在每个项目中都重新定义相同的数据结构。







# 使用 Django 构建 RESTful API 

当谈到 RESTful API 时，我们通常指的是一种设计 Web 服务的方式，该方式符合 REST（Representational State Transfer）原则。REST 是一种架构风格，其目标是在网络上建立可伸缩、简单、轻量级的服务。

以下是 RESTful API 的一些关键特点：

1. **资源（Resources）：** 在 RESTful 设计中，数据和功能被视为资源，每个资源都有一个唯一的标识符（URI）。例如，一个博客应用可能有文章、评论等资源，每个资源都有对应的 URI。

2. **表现层状态转化（Representational State Transfer，简称REST）：** 客户端通过对资源的表现（通常是 JSON 或 XML 格式）进行操作来实现状态的转化。这意味着客户端通过 HTTP 方法（GET、POST、PUT、DELETE 等）对资源进行操作，从而改变资源的状态。

3. **无状态性（Stateless）：** 每个请求从客户端到服务器都必须包含服务器处理该请求所需的所有信息。服务器不应存储关于客户端状态的信息，所有状态都应由客户端负责维护。

4. **统一接口（Uniform Interface）：** RESTful API 应该有一个统一的、简化的接口。这使得不同的客户端可以以相似的方式与不同的服务进行交互。

5. **客户端-服务器架构（Client-Server）：** 客户端和服务器之间存在清晰的分离，使得客户端和服务器能够独立演化。客户端负责用户界面和用户体验，而服务器负责处理请求并管理资源。

在 Django 中，你可以使用 Django REST framework（DRF）来构建 RESTful API。DRF 提供了一组强大的工具和库，简化了 API 的创建和维护过程。你可以使用 DRF 定义模型序列化器、视图和路由，以便构建具有良好结构和性能的 API。

## 什么是API

API 是应用程序接口（Application Programming Interface）的缩写。它是一种定义软件组件如何互相交互的方式。为了理解 API，可以将其比喻成餐厅的菜单和服务员。

想象你在餐厅用餐，菜单就是一种接口。它提供了一份可选项列表，你可以选择你想要的菜品。接着，你通过服务员（服务接口）告诉厨房（服务提供者）你的选择，然后厨房准备好食物并交给服务员，最终服务员将食物端到你的桌子上。

在软件开发中，API 就像是一个应用的菜单，它定义了可以用来与应用程序交互的一组规则。这些规则包括哪些功能可用、如何使用这些功能、以及如何与应用程序通信。开发者可以通过 API 向应用程序发出请求，就像你通过服务员向厨房发出点菜的请求一样。

API 允许不同的软件组件之间进行通信，这使得开发者能够更轻松地集成不同的服务、库或应用程序。常见的 API 类型包括 Web API，用于通过网络进行通信，以及库或框架提供的编程接口，用于在同一应用程序内的组件之间进行交互。

## 资源

当我们谈论 RESTful API 资源时，可以将其看作是 Web 服务中的各种实体或对象，它们可以被标识、创建、读取、更新或删除。这些资源通常代表了应用程序中的各种数据或功能。以下是一些简单易懂的示例：

1. **用户资源：**
   - **URI（标识符）：** `/users`
   - **操作：** 通过此资源可以获取所有用户列表、创建新用户、查看特定用户信息、更新用户信息或删除用户。

2. **文章资源：**
   - **URI：** `/articles`
   - **操作：** 提供对文章的基本操作，如获取文章列表、创建新文章、查看特定文章、更新文章或删除文章。

3. **评论资源：**
   - **URI：** `/articles/{article_id}/comments`
   - **操作：** 与特定文章关联，可以获取该文章的所有评论、创建新评论、查看特定评论、更新评论或删除评论。

4. **产品资源：**
   - **URI：** `/products`
   - **操作：** 允许获取产品列表、创建新产品、查看特定产品、更新产品信息或删除产品。

5. **订单资源：**
   - **URI：** `/orders`
   - **操作：** 包括获取订单列表、创建新订单、查看特定订单、更新订单信息或取消订单。

在 RESTful API 中，这些资源通过唯一的 URI 进行标识。通过使用不同的 HTTP 方法（GET、POST、PUT、DELETE 等），我们可以对这些资源进行不同的操作。例如，使用 GET 方法可以获取资源的信息，而使用 POST 方法可以创建新的资源。

总的来说，RESTful API 资源就像是应用程序中的各种实体，通过 API 可以对这些实体进行操作，使其具备标准化的、可伸缩的接口。

## 资源的表现

在 RESTful API 中，资源的表现（Representation）指的是资源的具体数据格式，通常以 JSON 或 XML 的形式呈现。当客户端请求资源时，服务器会以特定的格式返回资源的数据表示。这种数据表示包含了资源的属性、关系和其他相关信息。

举例来说，考虑一个博客应用的文章资源，其表现可能如下所示（使用 JSON 格式）：

```json
{
  "id": 1,
  "title": "RESTful API Basics",
  "content": "This is an introduction to RESTful API...",
  "author": {
    "id": 101,
    "name": "John Doe"
  },
  "created_at": "2023-01-01T12:00:00",
  "updated_at": "2023-01-02T09:30:00",
  "comments": [
    {
      "id": 501,
      "text": "Great article!",
      "user": {
        "id": 102,
        "name": "Jane Smith"
      },
      "created_at": "2023-01-01T13:45:00"
    },
    // Other comments...
  ]
}
```

在这个例子中，文章资源的表现包含了文章的标题、内容、作者等信息。作者信息和评论信息也以嵌套的方式包含在文章资源的表现中。

表现的选择通常取决于客户端和服务器之间的协商。客户端可以请求特定的表现格式，服务器则返回相应格式的资源数据。这种灵活性使得客户端和服务器可以选择最适合它们需求的数据格式，而不受限于单一的标准。

总体而言，资源的表现在 RESTful API 中起到了传递和呈现数据的关键作用，使得客户端能够理解和处理来自服务器的信息。

### 客户端与服务器

当我们谈论客户端和服务器时，可以将其比作一种常见的交流场景：餐厅。在这个场景中，客户端就是顾客，而服务器则是服务员和厨房的组合。

**1. 客户端（顾客）：**

   - **谁？** 顾客就是来到餐厅的人，有自己的需求和期望。
   - **做什么？** 顾客想点菜、付款、享受美食。
   - **怎么做？** 顾客通过菜单（接口）选择想要的食物，然后告诉服务员（服务器）他们的需求，最后等待服务员把食物端上桌。

**2. 服务器（服务员和厨房）：**
   - **谁？** 服务员和厨房是餐厅的工作人员，负责处理顾客的需求并准备食物。
   - **做什么？** 服务员接收顾客的点菜请求，将请求传达给厨房，然后将准备好的食物端到顾客桌上。同时，服务员也负责处理付款等其他服务。
   - **怎么做？** 服务员通过菜单（接口）了解顾客的需求，与厨房（后台系统）进行协调，最终提供顾客所需要的服务。

在计算机领域中，客户端通常是用户使用的设备（如电脑、手机、平板电脑），而服务器是存储和处理数据的计算机。就像在餐厅中，顾客通过与服务员交流来满足他们的需求，计算机系统中的客户端通过与服务器进行通信来获取数据、执行操作等。这种交互是通过定义好的接口（API）进行的，就像餐厅的菜单一样，规定了可用的选项和操作。

## HTTP 方法

HTTP（Hypertext Transfer Protocol）是一种用于传输超文本的协议，广泛用于互联网上的数据传输。在 RESTful API 中，HTTP 方法是指在与服务器交互时，客户端可以使用的不同动作或操作。以下是常见的 HTTP 方法：

1. **GET：**
   - **作用：** 用于从服务器获取资源，没有副作用，不会修改服务器的状态。(获得资源)
   - **示例：** 获取文章列表、获取特定文章的详细信息。

2. **POST：**
   - **作用：** 用于在服务器上创建新的资源。通常伴随着在请求中包含要创建的资源的数据。(创建资源)
   - **示例：** 创建新的用户、提交表单数据。

3. **PUT：**
   - **作用：** 用于更新服务器上的资源，或者在服务器上创建新资源（如果资源标识已存在）。(更新资源)
   - **示例：** 更新特定用户的信息、创建或更新文章。

4. **DELETE：**
   - **作用：** 用于删除服务器上的资源。(删除资源)
   - **示例：** 删除用户、删除文章。

5. **PATCH：**
   - **作用：** 用于对资源进行部分更新，而不是整个资源。(更新部分的资源)
   - **示例：** 更新文章的部分信息而不是整个文章。

6. **OPTIONS：**
   - **作用：** 用于获取目标资源支持的通信选项，例如服务器支持哪些方法、哪些头部信息等。
   - **示例：** 查看服务器支持的方法。

7. **HEAD：**
   - **作用：** 与 GET 方法类似，但服务器不返回实际数据，只返回响应头信息。通常用于检查资源的元数据。
   - **示例：** 获取资源的元信息，如大小或修改时间，而无需获取实际数据。

这些 HTTP 方法提供了一种标准的方式，使客户端能够与服务器进行各种操作。RESTful API 通常利用这些方法来实现对资源的增删改查等操作。在使用这些方法时，开发者需要遵循相应的约定和最佳实践，以确保系统的一致性和可维护性。

## 下载RESTful API 框架

可以使用该命名

```
pipenv install djangorestframework
```

## 一.创建API视图

在 Django 中创建 API 视图通常使用 Django REST Framework（DRF），这是一个强大且灵活的工具集，用于构建 Web APIs。以下是创建 API 视图的基本步骤：

1. **安装 Django REST Framework：**
   首先，确保已经安装了 Django 和 Django REST Framework。可以通过以下命令进行安装：

   ```bash
   pip install django djangorestframework
   ```

2. **创建一个 Django 项目和应用：**
   如果还没有 Django 项目，使用以下命令创建一个新的 Django 项目和应用：

   ```bash
   django-admin startproject your_project
   cd your_project
   python manage.py startapp your_app
   ```

3. **配置 Django REST Framework：**
   在项目的 `settings.py` 文件中，将 DRF 添加到 `INSTALLED_APPS` 中：

   ```python
   INSTALLED_APPS = [
       # ...
       'rest_framework',
       'your_app',
   ]
   ```

4. **创建序列化器（Serializer）：**
   序列化器定义了如何将模型转换为 JSON 格式。在应用的 `serializers.py` 文件中创建一个序列化器，例如：

   ```python
   from rest_framework import serializers
   from .models import YourModel
   
   class YourModelSerializer(serializers.ModelSerializer):
       class Meta:
           model = YourModel
           fields = '__all__'
   ```

5. **创建 API 视图：**
   在应用的 `views.py` 文件中创建 API 视图，使用 DRF 提供的视图类，例如：

   ```python
   from rest_framework import generics
   from .models import YourModel
   from .serializers import YourModelSerializer
   
   class YourModelAPIView(generics.ListCreateAPIView):
       queryset = YourModel.objects.all()
       serializer_class = YourModelSerializer
   ```

   在这个例子中，`YourModelAPIView` 继承了 `ListCreateAPIView`，该视图类提供了获取列表和创建资源的功能。

6. **配置 URL 路由：**
   在应用的 `urls.py` 文件中配置 URL 路由，将视图和路由关联起来：

   ```python
   from django.urls import path
   from .views import YourModelAPIView
   
   urlpatterns = [
       path('api/your-model/', YourModelAPIView.as_view(), name='your-model-api'),
   ]
   ```

   这样，API 的端点就是 `/api/your-model/`。

7. **运行项目：**
   最后，运行 Django 项目并检查 `/api/your-model/` 端点，应该能够看到 API 返回的数据。

这是一个简单的示例，实际项目中可能会涉及更多的配置和功能，但这个基本流程可以帮助你入门创建 Django REST Framework 的 API 视图。

### 实例

在views.py文件中

```python
from django.shortcuts import render
from rest_framework.decorators import api_view
from rest_framework.response import Response


@api_view()
def product_list(request):
    return Response('ok')

@api_view()
def product_detail(request, id):
    return Response(id)

```

在urls.py文件中

```python
from django.urls import path
from . import views

# URLConf
urlpatterns = [
    path('products/', views.product_list),
    path('products/<int:id>/', views.product_detail),
]
```

前提需要去下载RESTframwork 然后加入setting.py文件中的软件把restframwork加进去

在去配置storefront的urls.py文件，把path加进去

```
path('store/', include('store.urls'))
```

## 二.创建序列化器

**在serializers.py文件中**

```python
from rest_framework import serializers


class ProductSerializer(serializers.Serializer):
    id = serializers.IntegerField()
    title = serializers.CharField(max_lenght = 255)
    unit_price = serializers.DecimalField(max_digits=6,decimal_places=2)
```

这是一个 Django REST Framework 中的序列化器，用于定义数据模型（通常是 Django 模型）在传输和存储之间的转换规则。在你的示例中，`ProductSerializer` 是一个用于序列化和反序列化产品数据的类。

这样的序列化器可以用于将产品模型的实例转换为 JSON 数据，或者将接收的 JSON 数据反序列化为产品模型的实例。例如，可以在 API 视图中使用这个序列化器来处理产品数据的创建、更新和获取操作。

## 三.序列化对象

这是一个使用Django REST Framework构建的简单的API视图，用于展示产品列表和产品详情。

1. **导入模块和类：**
   
    ```python
    from django.shortcuts import get_object_or_404
    from rest_framework.decorators import api_view
    from rest_framework.response import Response
    from .models import Product
    from .serializers import ProductSerializer
    ```
    
    这里导入了所需的模块和类，包括Django的`get_object_or_404`函数用于获取对象或返回404页面，以及REST Framework中的`api_view`和`Response`类。
    
2. **产品列表视图：**
   
    ```python
    @api_view()
    def product_list(request):
        queryset = Product.objects.all()
        serializer = ProductSerializer(queryset, many=True)
        return Response(serializer.data)
    ```
    
    这个函数处理获取产品列表的请求。使用`Product.objects.all()`从数据库中获取所有产品，然后使用`ProductSerializer`将产品序列化为JSON格式。`many=True`表示序列化的是一个产品对象列表而不是单个对象。最后，使用`Response`类返回序列化后的数据。
    
3. **产品详情视图：**
   
    ```python
    @api_view()
    def product_detail(request, id):
        product = get_object_or_404(Product, pk=id)
        serializer = ProductSerializer(product)
        return Response(serializer.data)
    ```
    
    这个函数处理获取单个产品详情的请求。使用`get_object_or_404`通过产品的主键`id`从数据库中获取产品对象。然后，再次使用`ProductSerializer`将产品对象序列化为JSON格式。最后，使用`Response`类返回序列化后的数据。

这些视图函数使用了REST Framework的`@api_view`装饰器，这表示这是一个处理API请求的视图。这些函数返回的数据都是以JSON格式的响应。

## 四.创建自定义序列化字段

```python
from rest_framework import serializers
from store.models import Product
from decimal import Decimal

class ProductSerializer(serializers.Serializer):
    id = serializers.IntegerField()
    title = serializers.CharField(max_length = 255)
    price = serializers.DecimalField(max_digits=6,decimal_places=2,source = 'unit_price')
    price_with_tax = serializers.SerializerMethodField(method_name='calculate_tax')

    def calculate_tax(self,product: Product):
        return product.unit_price * Decimal(1.1)
```

在这个序列化器中，`source='unit_price'` 是用来指定 `price` 字段的数据来源。具体来说，这个设置告诉序列化器，要从 `Product` 模型的 `unit_price` 字段获取数据，并将其用作 `price` 字段的值。

在上述代码中，我们使用`SerializerMethodField`创建了一个自定义字段`price_with_tax`，它的值通过调用`calculate_tax`方法来计算。让我解释一下这两部分的作用：

1. **SerializerMethodField:**
   - `SerializerMethodField`是Django REST framework中的一个字段类，它允许你在序列化器中包含一个通过自定义方法计算的字段。
   - 这个字段通常用于序列化器中的自定义计算，而不是直接从模型字段派生。

2. **calculate_tax 方法:**
   - `calculate_tax`是一个自定义方法，它接受一个`Product`对象作为参数。
   - 在这个例子中，`calculate_tax`方法计算产品价格的税后价格。它使用`unit_price`乘以1.1，表示将价格增加10%的税。

这样，当你使用`ProductSerializer`序列化一个`Product`实例时，`price_with_tax`字段将包含`calculate_tax`方法返回的值。确保在你的视图或其他地方正确使用了这个序列化器，以便在生成的 JSON 中看到`price_with_tax`字段。

## 五.序列化关系

好的，让我们更详细地介绍一下在Django Rest Framework（DRF）中序列化关系的各种方法。

### 1. 主键关系

```python
# serializers.py
from rest_framework import serializers
from .models import Product, Collection

class ProductSerializer(serializers.ModelSerializer):
    class Meta:
        model = Product
        fields = ['id', 'title', 'price', 'price_with_tax', 'collection']
```

在这个例子中，`ProductSerializer` 使用 `PrimaryKeyRelatedField` 来表示 `collection` 字段，它将通过其主键表示相关的 `Collection` 对象。

### 2. 字符串表示

```python
# serializers.py
from rest_framework import serializers
from .models import Product, Collection

class ProductSerializer(serializers.ModelSerializer):
    collection = serializers.StringRelatedField()

    class Meta:
        model = Product
        fields = ['id', 'title', 'price', 'price_with_tax', 'collection']
```

这里，`StringRelatedField` 用于 `collection` 字段，它将通过其字符串表示来表示相关的 `Collection` 对象，通常从对象的 `__str__` 方法中获得。

### 3. 嵌套对象

```python
# serializers.py
from rest_framework import serializers
from .models import Product, Collection

class CollectionSerializer(serializers.ModelSerializer):
    class Meta:
        model = Collection
        fields = ['id', 'name']

class ProductSerializer(serializers.ModelSerializer):
    collection = CollectionSerializer()

    class Meta:
        model = Product
        fields = ['id', 'title', 'price', 'price_with_tax', 'collection']
```

在这种情况下，`ProductSerializer` 包含一个嵌套的 `CollectionSerializer` 用于 `collection` 字段，提供了相关 `Collection` 对象的完整表示。

### 4. 超链接

```python
# serializers.py
from rest_framework import serializers
from .models import Product, Collection

class ProductSerializer(serializers.HyperlinkedModelSerializer):
    collection = serializers.HyperlinkedRelatedField(
        view_name='collection-detail',  # Collection详情视图的URL模式名称
        read_only=True
    )

    class Meta:
        model = Product
        fields = ['url', 'id', 'title', 'price', 'price_with_tax', 'collection']
```

在这个例子中，`HyperlinkedRelatedField` 用于 `collection` 字段。它通过超链接表示相关的 `Collection` 对象，而 `view_name` 参数指定了 Collection 详情视图的URL模式名称。

这些示例展示了根据特定用例和前端所需格式使用不同方法序列化关系的不同方法。

### 实例 主要用的

在views.py中

```python
from django.shortcuts import get_object_or_404
from rest_framework.decorators import api_view
from rest_framework.response import Response
from .models import Product
from .serializers import ProductSerializer



@api_view()
def product_list(request):
    queryset = Product.objects.select_related('collection').all()
    serializer = ProductSerializer(queryset,many =True)
    return Response(serializer.data)
```

在serializers.py中

```python
from rest_framework import serializers
from store.models import Product ,Collection
from decimal import Decimal


class CollectionSerializers(serializers.Serializer):
    id = serializers.IntegerField()
    title  = serializers.CharField(max_length=255)

class ProductSerializer(serializers.Serializer):
    id = serializers.IntegerField()
    title = serializers.CharField(max_length = 255)
    price = serializers.DecimalField(max_digits=6,decimal_places=2,source = 'unit_price')
    price_with_tax = serializers.SerializerMethodField(method_name='calculate_tax')
    collection = CollectionSerializers()
    def calculate_tax(self,product: Product):
        return product.unit_price * Decimal(1.1)
```

## 六.模型序列化器

在Django Rest Framework（DRF）中，Model Serializers 是一个用于简化序列化与反序列化 Django 模型实例的工具。Model Serializers 提供了一种快捷的方式，通过声明性的方式定义序列化器，而无需手动编写大量的序列化和反序列化代码。以下是 Model Serializers 的主要特点和使用方法：

### 特点：

1. **自动字段生成：** Model Serializers 会自动根据模型的字段生成相应的序列化和反序列化字段，无需手动添加每个字段。

2. **默认实现：** Model Serializers 默认实现了 `create()` 和 `update()` 方法，简化了创建和更新模型实例的逻辑。

3. **嵌套关系：** Model Serializers 能够处理模型之间的关系，并通过嵌套序列化器实现复杂的嵌套关系表示。

### 使用方法：

1. **定义 Model Serializer：**

   ```python
   # serializers.py
   from rest_framework import serializers
   from .models import YourModel

   class YourModelSerializer(serializers.ModelSerializer):
       class Meta:
           model = YourModel
           fields = '__all__'  # 或者指定需要序列化的字段列表
   ```

2. **在视图中使用：**

   ```python
   # views.py
   from rest_framework import generics
   from .models import YourModel
   from .serializers import YourModelSerializer
   
   class YourModelListView(generics.ListCreateAPIView):
       queryset = YourModel.objects.all()
       serializer_class = YourModelSerializer
   
   class YourModelDetailView(generics.RetrieveUpdateDestroyAPIView):
       queryset = YourModel.objects.all()
       serializer_class = YourModelSerializer
   ```

   在这个例子中，`YourModelSerializer` 被用于序列化和反序列化 `YourModel` 模型的实例。`YourModelListView` 处理列表和创建操作，`YourModelDetailView` 处理单个实例的检索、更新和删除操作。

Model Serializers 简化了 Django 模型实例的序列化和反序列化过程，让开发者能够更专注于业务逻辑而不是繁琐的序列化细节。

## 实例

**在views.py中**

```python
from rest_framework import serializers
from store.models import Product ,Collection
from decimal import Decimal


class CollectionSerializers(serializers.ModelSerializer):
    class Meta:
        model = Collection
        fields = ['id','title']

class ProductSerializer(serializers.ModelSerializer):
    class Meta:
        model = Product
        fields= ['id','title','unit_price','price_with_tax','collection']

    price_with_tax = serializers.SerializerMethodField(method_name='calculate_tax')

    def calculate_tax(self,product: Product):
        return product.unit_price * Decimal(1.1)
```

## 七.反序列化对象

```python
@api_view(['GET','POST'])
def product_list(request):
    if request.method == 'GET':
        queryset = Product.objects.select_related('collection').all()
        serializer = ProductSerializer(queryset,many =True)
        return Response(serializer.data)
    elif request.method == 'POST':
        serializer = ProductSerializer(data=request.data)
        return Response("ok")         
    
```

在你提供的代码中，你定义了一个 `product_list` 视图，它处理包含 GET 和 POST 请求的两种情况。

1. **GET 请求部分:**
   ```python
   if request.method == 'GET':
       queryset = Product.objects.select_related('collection').all()
       serializer = ProductSerializer(queryset, many=True)
       return Response(serializer.data)
   ```
   - 当收到 GET 请求时，你查询所有产品，并使用 `ProductSerializer` 序列化这些产品。
   - `select_related('collection')` 表示在查询中使用 `select_related` 方法，以便在同一查询中获取与产品相关联的集合数据，以避免 N+1 查询问题。
   - 最后，将序列化后的数据包装在 `Response` 对象中返回。

2. **POST 请求部分:**
   ```python
   elif request.method == 'POST':
       serializer = ProductSerializer(data=request.data)
       return Response("ok")
   ```
   - 当收到 POST 请求时，你使用 `ProductSerializer` 反序列化请求中的数据。
   - 这里的 `serializer = ProductSerializer(data=request.data)` 创建了一个序列化器实例，该实例包含了从请求中提取的数据。
   - 注意，你在这里只是返回了一个字符串 "ok"，通常情况下，你可能会在保存数据到数据库之后返回包含新创建对象信息的响应。

需要注意的是，POST 请求的处理部分还缺少保存到数据库的步骤。如果你想将反序列化后的数据保存到数据库中，你需要调用序列化器的 `is_valid` 方法，检查数据的有效性，然后使用 `serializer.save()` 保存对象。最后，你可以返回包含新创建对象信息的响应。

## 八.数据验证

数据验证（Data validation）是在 Django REST framework（DRF）中序列化器（Serializers）中执行的一个关键步骤。序列化器不仅用于将模型实例转换为可渲染的 JSON 数据，还用于从前端接收到的数据中创建或更新模型实例。

在 DRF 中，可以使用序列化器的 `is_valid()` 方法来执行数据验证。这个方法将检查提供的数据是否符合序列化器中定义的规则。如果数据有效，可以继续执行其他操作（例如保存到数据库）；否则，可以检查并返回包含错误信息的响应。

下面是一个简单的例子，演示了如何在 DRF 中进行数据验证：

```python
from rest_framework import serializers
from rest_framework.response import Response
from rest_framework.decorators import api_view

class ProductSerializer(serializers.Serializer):
    title = serializers.CharField(max_length=100)
    price = serializers.DecimalField(max_digits=6, decimal_places=2)

@api_view(['POST'])
def create_product(request):
    if request.method == 'POST':
        serializer = ProductSerializer(data=request.data)
        if serializer.is_valid():
            # 执行保存到数据库等操作
            # serializer.save()
            return Response({"message": "Product created successfully"})
        else:
            return Response(serializer.errors, status=400)
```

在上述例子中，`ProductSerializer` 包含了 `title` 和 `price` 两个字段，它们都有相应的验证规则。在视图函数 `create_product` 中，我们通过 `ProductSerializer(data=request.data)` 创建了一个序列化器实例，并使用 `is_valid()` 方法检查数据的有效性。如果数据有效，你可以执行保存到数据库等操作，否则，你可以返回包含错误信息的响应。

注意：在实际应用中，可以根据需要添加更多的验证规则，例如自定义验证方法、唯一性验证等。 DRF 提供了丰富的验证器，可以灵活应对各种验证需求。

## 实例

```python
@api_view(['GET','POST'])
def product_list(request):
    if request.method == 'GET':
        queryset = Product.objects.select_related('collection').all()
        serializer = ProductSerializer(queryset,many =True)
        return Response(serializer.data)
    elif request.method == 'POST':
        serializer = ProductSerializer(data=request.data)
        serializer.is_valid(raise_exception=True)
        serializer.validated_data
        return Response("ok")  
```

**raise_exception=True** 可以不用if语句，如果传递数据不准确，django会自动返回400

## 九.创建对象，保存对象

```python
from django.shortcuts import get_object_or_404
from rest_framework.decorators import api_view
from rest_framework.response import Response
from .models import Product
from .serializers import ProductSerializer
from rest_framework import status


@api_view(['GET','POST'])
def product_list(request):
    if request.method == 'GET':
        queryset = Product.objects.select_related('collection').all()
        serializer = ProductSerializer(queryset,many =True)
        return Response(serializer.data)
    elif request.method == 'POST':
        serializer = ProductSerializer(data=request.data)
        serializer.is_valid(raise_exception=True)
        serializer.save()
        return Response(serializer.data,status=status.HTTP_201_CREATED)      
    

@api_view(['GET','PUT'])
def product_detail(request, id):
        product = get_object_or_404(Product, pk=id)
        if request.method == 'GET':
            serializer = ProductSerializer(product)
            return Response(serializer.data)
        elif request.method == 'PUT':
            serializer = ProductSerializer(product, data=request.data)
            serializer.is_valid(raise_exception=True)
            serializer.save()
            return Response(serializer.data)
    
```

`serializer = ProductSerializer(product, data=request.data)` 这一行的目的是将已有的产品实例（`product`）与新的数据（`request.data`）结合起来，并创建一个新的序列化器实例。

## 十.删除对象

删除对象在Django Rest Framework（DRF）视图中通常使用HTTP的DELETE请求。以下是一个简单的例子：

```python
from django.shortcuts import get_object_or_404
from rest_framework.decorators import api_view
from rest_framework.response import Response
from .models import Product
from .serializers import ProductSerializer
from rest_framework import status

@api_view(['DELETE'])
def product_delete(request, id):
    product = get_object_or_404(Product, pk=id)

    if request.method == 'DELETE':
        product.delete()
        return Response(status=status.HTTP_204_NO_CONTENT)
```

在这个例子中，我们定义了一个名为`product_delete` 的视图函数，它接收一个`DELETE` 请求并删除具有给定ID的产品。使用`get_object_or_404` 来获取要删除的产品实例，然后调用 `product.delete()` 来从数据库中删除它。

最后，我们返回一个HTTP 204 No Content响应，表示删除成功。

## 实例

```python
@api_view(['GET','PUT','DELETE'])
def product_detail(request, id):
	 elif request.method == 'DELETE':
             if product.orderitem_set.count() > 0 :
                  return Response({'error':'产品不能被删除，因为他与订单项相关联'},
                         status=status.HTTP_405_METHOD_NOT_ALLOWED)
             product.delete()
             return Response(status=status.HTTP_204_NO_CONTENT)
```

这段代码处理了DELETE请求，主要包含以下步骤：

1. `if request.method == 'DELETE':`：检查请求是否是DELETE请求。

2. `if product.orderitem_set.count() > 0:`：检查与当前产品关联的订单项是否存在。如果存在关联的订单项，表示该产品不能被删除，因为有其他对象与之相关联。

3. `return Response({'error':'产品不能被删除，因为他与订单项相关联'},status=status.HTTP_405_METHOD_NOT_ALLOWED)`：如果有关联的订单项，返回一个包含错误信息的HTTP响应，状态码为`405 Method Not Allowed`。这表示不允许执行DELETE操作，因为与订单项相关联。

4. `product.delete()`：如果没有关联的订单项，执行删除操作，从数据库中删除当前产品对象。

5. `return Response(status=status.HTTP_204_NO_CONTENT)`：返回HTTP响应，状态码为`204 No Content`，表示删除成功，且没有响应体。

这段代码的作用是在DELETE请求下，根据产品是否与订单项关联进行相应的处理：如果关联了订单项，则不允许删除，并返回相应的错误信息；如果没有关联订单项，则执行删除操作，返回删除成功的响应。

**httpstatuses.com   所有标准的http状态代码**

## 章节代码

**views.py**

```python
from django.shortcuts import get_object_or_404
from rest_framework.decorators import api_view
from rest_framework.response import Response
from .models import Product,Collection
from .serializers import ProductSerializer,CollectionSerializers
from rest_framework import status
from django.db.models import Count


@api_view(['GET','POST',])
def product_list(request):
    if request.method == 'GET':
        queryset = Product.objects.select_related('collection').all()
        serializer = ProductSerializer(queryset,many =True)
        return Response(serializer.data)
    elif request.method == 'POST':
        serializer = ProductSerializer(data=request.data)
        serializer.is_valid(raise_exception=True)
        serializer.save()
        return Response(serializer.data,status=status.HTTP_201_CREATED)      
    

@api_view(['GET','PUT','DELETE'])
def product_detail(request, id):
        product = get_object_or_404(Product, pk=id)
        if request.method == 'GET':
            serializer = ProductSerializer(product)
            return Response(serializer.data)
        elif request.method == 'PUT':
            serializer = ProductSerializer(product, data=request.data)
            serializer.is_valid(raise_exception=True)
            serializer.save()
            return Response(serializer.data)
        elif request.method == 'DELETE':
             if product.orderitem_set.count() > 0 :
                  return Response({'error':'产品不能被删除，因为他与订单项相关联'},status=status.HTTP_405_METHOD_NOT_ALLOWED)
             product.delete()
             return Response(status=status.HTTP_204_NO_CONTENT)
        

@api_view(['GET','POST'])
def collection_list(request):
    if request.method == 'GET':
        queryset = Collection.objects.annotate(products_count = Count('products')).all()
        serializer = CollectionSerializers(queryset, many=True)
        return Response(serializer.data)
    elif request.method=='POST':
         serializer = CollectionSerializers(data=request.data)
         serializer.is_valid(raise_exception=True) 
         serializer.save()
         return Response(serializer.data,status=status.HTTP_201_CREATED)
    
@api_view(['GET','PUT','DELETE'])
def collection_detail(request, pk):
     collection = get_object_or_404(
          Collection.objects.annotate(
               products_count = Count('products')),pk=pk) 
     if request.method=='GET':
          serializer = CollectionSerializers(collection)
          return Response(serializer.data)
     elif request.method=='PUT':
          serializer = CollectionSerializers(collection,data=request.data)
          serializer.is_valid(raise_exception=True)
          serializer.save()
          return Response(serializer.data)
     elif request.method=='DELETE':
          if collection.products.count() > 0 :
               return Response({'error':'产品不能被删除，因为他与订单项相关联'},status=status.HTTP_405_METHOD_NOT_ALLOWED)
          Product.delete()
          return Response(status=status.HTTP_204_NO_CONTENT)
```

**serializers.py**

```python
from rest_framework import serializers
from store.models import Product ,Collection
from decimal import Decimal


class CollectionSerializers(serializers.ModelSerializer):
    class Meta:
        model = Collection  
        fields = ['id','title','products_count']

    products_count  = serializers.IntegerField()

class ProductSerializer(serializers.ModelSerializer):
    class Meta:
        model = Product
        fields= ['id','title','description','slug','inventory','unit_price','price_with_tax','collection']

    price_with_tax = serializers.SerializerMethodField(method_name='calculate_tax')
    def calculate_tax(self,product: Product):
        return product.unit_price * Decimal(1.1)
```

**urls.py**

```python
from django.urls import path
from . import views

# URLConf
urlpatterns = [
    path('products/', views.product_list),
    path('products/<int:id>/', views.product_detail),
    path('collections/', views.collection_list),
    path('collections/<int:pk>/',views.collection_detail),
]

```



# 高级 API 概念

## 一.基于类的视图

在Django中，Class-Based Views（基于类的视图）是一种处理HTTP请求和生成HTTP响应的方式，它使用Python类来组织和结构化视图代码。与基于函数的视图不同，基于类的视图提供了更强大和灵活的工具，以处理不同HTTP方法、混合多个视图、重用逻辑等。

以下是Class-Based Views的一些关键概念和优势：

1. **继承自基类：** Class-Based Views通常继承自Django提供的基类。这些基类提供了处理常见用例的方法，如`View`、`TemplateView`、`ListView`、`DetailView`等。

2. **Mixin类：** 可以使用Mixin类（混入类）来添加或组合功能。Mixin是一种轻量级的方式，通过将不同的Mixin类组合在一起，创建具有所需功能的视图。

3. **HTTP方法处理：** Class-Based Views允许为不同的HTTP方法（GET、POST、PUT等）提供不同的处理方法，使得代码更加清晰。

4. **类属性和方法：** 可以使用类属性和方法来组织代码，使其更具可读性和可维护性。

5. **多继承和混入：** 可以从多个类继承，使用混入类来共享和重用代码，提高代码的可复用性。

6. **类装饰器：** 通过使用类装饰器，可以在视图执行前后添加额外的逻辑。

以下是一个简单的Class-Based View的例子：

```python
from django.views import View
from django.shortcuts import render

class MyView(View):
    template_name = 'my_template.html'

    def get(self, request, *args, **kwargs):
        context = {'message': 'Hello, this is a Class-Based View!'}
        return render(request, self.template_name, context)
```

在这个例子中，`MyView`继承自`View`基类，它定义了一个`get`方法，该方法处理GET请求。通过使用`render`函数，它将一个包含消息的上下文渲染到指定的模板中。

### 实例

```python
from rest_framework.views import APIView



class ProductList(APIView):
     def get(self,request):
        queryset = Product.objects.select_related('collection').all()
        serializer = ProductSerializer(queryset,many =True)
        return Response(serializer.data)
     
     def post(self, request):
        serializer = ProductSerializer(data=request.data)
        serializer.is_valid(raise_exception=True)
        serializer.save()
        return Response(serializer.data,status=status.HTTP_201_CREATED)     

class ProductDetail(APIView):
    def get(self,request,id):
        product = get_object_or_404(Product, pk=id)
        serializer = ProductSerializer(product)
        return Response(serializer.data)
         
    def put(self,request,id):
        product = get_object_or_404(Product, pk=id)
        serializer = ProductSerializer(product, data=request.data)
        serializer.is_valid(raise_exception=True)
        serializer.save()
        return Response(serializer.data)
    
    def delete(self,request,id):
        product = get_object_or_404(Product, pk=id)
        if product.orderitem_set.count() > 0 :
            return Response(
                {'error':'产品不能被删除，因为他与订单项相关联'},
                status=status.HTTP_405_METHOD_NOT_ALLOWED)
        product.delete()
        return Response(status=status.HTTP_204_NO_CONTENT)
```

**from rest_framework.views import APIView** `APIView`是Django REST framework中的基类，用于创建基于类的API视图。它提供了处理HTTP请求的方法，并支持RESTful风格的API开发。通过继承`APIView`，你可以定义自己的API视图，以便处理各种HTTP方法（GET、POST、PUT、DELETE等）。



## 二.Mixins

在Django REST framework（DRF）中，Mixin是一种用于提供通用功能和行为的机制。Mixins允许你在类中包含和复用一些功能，而不是通过多重继承的方式增加类的复杂性。在DRF中，有一些内置的Mixins可用于视图类，以提供常见的功能。

以下是一些常见的DRF内置Mixins：

1. **`CreateModelMixin`：** 提供处理HTTP POST请求并创建新对象的功能。

2. **`ListModelMixin`：** 提供处理HTTP GET请求并列出对象列表的功能。

3. **`RetrieveModelMixin`：** 提供处理HTTP GET请求并检索单个对象的功能。

4. **`UpdateModelMixin`：** 提供处理HTTP PUT请求并更新现有对象的功能。

5. **`DestroyModelMixin`：** 提供处理HTTP DELETE请求并删除现有对象的功能。

6. **`ListModelMixin`：** 提供处理HTTP GET请求并列出对象列表的功能。

7. **`DestroyModelMixin`：** 提供处理HTTP DELETE请求并删除现有对象的功能。

这些Mixins通常与DRF的`GenericAPIView`结合使用，以提供通用的CRUD操作。以下是一个示例，展示了如何使用一些Mixins创建一个具有常见操作的通用视图：

```python
from rest_framework.generics import GenericAPIView
from rest_framework.mixins import CreateModelMixin, ListModelMixin, RetrieveModelMixin, UpdateModelMixin, DestroyModelMixin
from rest_framework.response import Response
from rest_framework import status
from .models import MyModel
from .serializers import MyModelSerializer

class MyModelAPIView(GenericAPIView, CreateModelMixin, ListModelMixin, RetrieveModelMixin, UpdateModelMixin, DestroyModelMixin):
    queryset = MyModel.objects.all()
    serializer_class = MyModelSerializer

    def get(self, request, *args, **kwargs):
        if 'pk' in kwargs:
            return self.retrieve(request, *args, **kwargs)
        else:
            return self.list(request, *args, **kwargs)

    def post(self, request, *args, **kwargs):
        return self.create(request, *args, **kwargs)

    def put(self, request, *args, **kwargs):
        return self.update(request, *args, **kwargs)

    def delete(self, request, *args, **kwargs):
        return self.destroy(request, *args, **kwargs)
```

在这个例子中，`MyModelAPIView`继承自`GenericAPIView`和一些Mixins，它实现了通用的CRUD操作。你可以根据需要选择性地包含或排除Mixins，以满足你的特定要求。

## 三.通用视图

在Django REST framework (DRF) 中，Generic Views 是一种为你提供了标准 CRUD（Create, Retrieve, Update, Delete） 操作的视图类。**这些视图类已经预先定义好了通用的行为，以减少开发者在创建 API 时的重复劳动。**DRF 的 generic views 有助于快速实现常见的 RESTful 操作。

以下是 DRF 中一些常见的 generic views：

1. **`ListAPIView`：** 用于展示列表数据，对应 HTTP 方法为 GET。它常用于获取资源列表。

   ```python
   from rest_framework.generics import ListAPIView
   from myapp.models import MyModel
   from myapp.serializers import MyModelSerializer

   class MyModelListView(ListAPIView):
       queryset = MyModel.objects.all()
       serializer_class = MyModelSerializer
   ```

2. **`RetrieveAPIView`：** 用于获取单个资源的详细信息，对应 HTTP 方法为 GET。

   ```python
   from rest_framework.generics import RetrieveAPIView
   from myapp.models import MyModel
   from myapp.serializers import MyModelSerializer

   class MyModelDetailView(RetrieveAPIView):
       queryset = MyModel.objects.all()
       serializer_class = MyModelSerializer
   ```

3. **`CreateAPIView`：** 用于创建新资源，对应 HTTP 方法为 POST。

   ```python
   from rest_framework.generics import CreateAPIView
   from myapp.models import MyModel
   from myapp.serializers import MyModelSerializer

   class MyModelCreateView(CreateAPIView):
       queryset = MyModel.objects.all()
       serializer_class = MyModelSerializer
   ```

4. **`UpdateAPIView` 和 `DestroyAPIView`：** 用于更新和删除资源，对应的 HTTP 方法分别为 PUT/PATCH 和 DELETE。

   ```python
   from rest_framework.generics import UpdateAPIView, DestroyAPIView
   from myapp.models import MyModel
   from myapp.serializers import MyModelSerializer
   
   class MyModelUpdateView(UpdateAPIView):
       queryset = MyModel.objects.all()
       serializer_class = MyModelSerializer
   
   class MyModelDeleteView(DestroyAPIView):
       queryset = MyModel.objects.all()
       serializer_class = MyModelSerializer
   ```

这些 generic views 提供了通用的行为和默认的实现，可以通过继承并配置一些属性来快速构建 API 视图。这使得开发者能够专注于业务逻辑而不必重复编写相似的视图代码。 

## 实例

```python
from rest_framework.generics import ListCreateAPIView   

class ProductList(ListCreateAPIView):
    queryset = Product.objects.select_related('collection').all()
    serializer_class = ProductSerializer

    def get_serializer_context(self):
        return {'request': self.request}
```

这是一个使用 DRF 中的 `ListCreateAPIView` 的类视图。让我们逐行解释这段代码：

1. **`class ProductList(ListCreateAPIView):`：** 这个类继承了 DRF 提供的 `ListCreateAPIView` 类，该类已经实现了列表展示和创建资源的通用逻辑。

2. **`queryset = Product.objects.select_related('collection').all()`：** 这是一个查询集，用于获取所有产品对象。`select_related('collection')` 用于在获取产品时同时获取关联的系列（collection）对象，以避免多次查询数据库。

3. **`serializer_class = ProductSerializer`：** 这是用于序列化和反序列化产品对象的序列化器类。

4. **`def get_serializer_context(self):`：** 这是一个自定义方法，用于获取序列化器的上下文。在这里，返回了包含请求（request）的字典作为上下文。这通常用于在序列化器中访问请求的信息。

通过继承 `ListCreateAPIView` 并配置这些属性，你可以轻松地创建一个用于展示产品列表和创建新产品的 API 视图。DRF 的 generic views 大大简化了视图的开发，使开发者能够专注于业务逻辑而不必担心太多的 CRUD 操作的实现。

## 四,自定义视图

在Django Rest Framework（DRF）中，你可以通过继承通用视图（Generic Views）的基类，并添加自定义的逻辑来创建自定义通用视图。以下是创建自定义通用视图的一般步骤：

1. **导入 DRF 中的通用视图基类：**

   ```python
   from rest_framework.generics import ListCreateAPIView
   ```

   这里以`ListCreateAPIView`为例，你可以根据你的需求选择其他基类。

2. **创建自定义通用视图类：**

   ```python
   from rest_framework.response import Response
   from .models import YourModel
   from .serializers import YourModelSerializer

   class YourCustomView(ListCreateAPIView):
       queryset = YourModel.objects.all()
       serializer_class = YourModelSerializer

       def get(self, request, *args, **kwargs):
           # 自定义逻辑，可以根据需要添加额外的处理
           custom_data = {'message': 'Custom GET logic'}
           return Response(custom_data)

       def post(self, request, *args, **kwargs):
           # 自定义逻辑，可以根据需要添加额外的处理
           custom_data = {'message': 'Custom POST logic'}
           return Response(custom_data)
   ```

   你可以根据需要重写通用视图基类提供的各种方法，如 `get`, `post`, `put`, `patch`, `delete` 等。

3. **在 `urls.py` 中配置 URL 映射：**

   ```python
   from django.urls import path
   from .views import YourCustomView
   
   urlpatterns = [
       path('your_custom_path/', YourCustomView.as_view(), name='your_custom_view'),
       # 添加其他 URL 映射...
   ]
   ```

   这将把你的自定义视图映射到指定的路径。

确保你的模型（`YourModel`）、序列化器（`YourModelSerializer`）以及相应的 URL 映射都正确设置，以便在访问相应的路径时触发你的自定义视图逻辑。



### 实例

```python
class ProductDetail(RetrieveUpdateDestroyAPIView):
    queryset = Product.objects.all()
    serializer_class = ProductSerializer
    
    def delete(self,request,pk):
        product = get_object_or_404(Product, pk=pk)
        if product.orderitem_set.count() > 0 :
            return Response({'error':'产品不能被删除，因为他与订单项相关联'},status=status.HTTP_405_METHOD_NOT_ALLOWED)
        product.delete()
        return Response(status=status.HTTP_204_NO_CONTENT)
    
class CollectionDetail(RetrieveUpdateDestroyAPIView):
    queryset = Collection.objects.annotate(
        products_count = Count('products'))
    serializer_class = CollectionSerializers
    
    def delete(self,request,pk):
        collection =get_object_or_404(Collection, pk=pk)
        if collection.products.count() > 0 :
            return Response({'error':'产品不能被删除，因为他与订单项相关联'},status=status.HTTP_405_METHOD_NOT_ALLOWED)
        Product.delete()
        return Response(status=status.HTTP_204_NO_CONTENT)


```

## 五.视图集ViewSets

Django Rest Framework（DRF）中的`ViewSet`是一个处理 HTTP 请求的类，它结合了 Django 的视图类（View）和 Django 模型的查询集（QuerySet）。`ViewSet`简化了视图和 URL 配置，并提供了标准的 CRUD（Create, Retrieve, Update, Delete）操作。

以下是创建和使用`ViewSet`的一般步骤：

1. **导入 DRF 中的 ViewSet 和相关类：**

   ```python
   from rest_framework import viewsets
   from .models import YourModel
   from .serializers import YourModelSerializer
   ```

2. **创建一个继承自 `viewsets.ModelViewSet` 的 ViewSet 类：**

   ```python
   class YourModelViewSet(viewsets.ModelViewSet):
       queryset = YourModel.objects.all()
       serializer_class = YourModelSerializer
   ```

   在这个例子中，`YourModelViewSet` 将包含标准的 CRUD 操作，并使用你的模型和序列化器。

3. **配置 URL 映射：**

   在你的 `urls.py` 文件中，使用 `router` 来自动配置 URL 映射：

   ```python
   from django.urls import path, include
   from rest_framework.routers import DefaultRouter
   from .views import YourModelViewSet
   
   router = DefaultRouter()
   router.register(r'your-model', YourModelViewSet, basename='your-model')
   
   urlpatterns = [
       path('api/', include(router.urls)),
       # 添加其他 URL 映射...
   ]
   ```

   这样会自动创建以下 URL 映射：
   - `/api/your-model/` (GET, POST)
   - `/api/your-model/{pk}/` (GET, PUT, PATCH, DELETE)

   可以根据需要自定义路由和 URL。

通过使用`ViewSet`，你能够简化代码并轻松处理标准的 REST 操作。`ModelViewSet`提供了标准的查询集、序列化器和视图逻辑，而 `DefaultRouter` 则自动处理 URL 映射。

## 实例

```python
from rest_framework.viewsets import ModelViewSet


class ProductViewSet(ModelViewSet):
    queryset = Product.objects.all()
    serializer_class = ProductSerializer

    def get_serializer_context(self):
        return {'request': self.request}

    def delete(self,request,pk):
        product = get_object_or_404(Product, pk=pk)
        if product.orderitem_set.count() > 0 :
            return Response({'error':'产品不能被删除，因为他与订单项相关联'},status=status.HTTP_405_METHOD_NOT_ALLOWED)
        product.delete()
        return Response(status=status.HTTP_204_NO_CONTENT)


class CollectionViewSet(ModelViewSet):
    queryset = Collection.objects.annotate(
        products_count = Count('products')).all()
    serializer_class = CollectionSerializers
    
    def delete(self,request,pk):
        collection =get_object_or_404(Collection, pk=pk)
        if collection.products.count() > 0 :
            return Response({'error':'产品不能被删除，因为他与订单项相关联'},status=status.HTTP_405_METHOD_NOT_ALLOWED)
        Product.delete()
        return Response(status=status.HTTP_204_NO_CONTENT)
```

## 六. 使用路由器来创建路由对于视图集

在Django Rest Framework（DRF）中，使用路由器（`DefaultRouter`）可以方便地为视图集（ViewSets）创建标准的 URL 配置。以下是使用路由器的步骤：

1. **导入 DRF 中的路由器和视图集：**

   ```python
   from rest_framework.routers import DefaultRouter
   from .views import YourModelViewSet
   ```

   在这里，`YourModelViewSet` 是你自定义的视图集。

2. **创建一个路由器实例：**

   ```python
   router = DefaultRouter()
   ```

3. **将你的视图集注册到路由器上：**

   ```python
   router.register(r'your-model', YourModelViewSet, basename='your-model')
   ```

   这里 `'your-model'` 是 URL 的前缀，可以根据需要修改。`basename` 参数是为了为 URL 命名提供前缀。

4. **将路由器的 URL 添加到 Django 项目的 URL 配置中：**

   ```python
   from django.urls import path, include

   urlpatterns = [
       path('api/', include(router.urls)),
       # 添加其他 URL 映射...
   ]
   ```

   这里的 `'api/'` 是你希望在项目中使用的 URL 前缀。`include(router.urls)` 会自动将路由器中注册的视图集的 URL 添加到项目的 URL 配置中。

5. **启动 Django 项目：**

   运行开发服务器，并访问相应的 URL。根据前面注册的视图集，你将能够访问诸如 `/api/your-model/` 这样的 URL。

使用路由器能够自动创建标准的 CRUD 操作的 URL 映射，减少了手动配置 URL 的工作。这对于处理 RESTful API 非常有帮助。

### 实例

```python
from django.urls import path
from rest_framework.routers import DefaultRouter
from . import views


router = DefaultRouter()
router.register('products',views.ProductViewSet)
router.register('collection',views.CollectionViewSet)



# URLConf
urlpatterns = router.urls
```

## 七.建立评论应用程序

构建 Reviews API 涉及创建模型、序列化器、视图集和 URL 配置。以下是一个简单的步骤示例，假设你正在构建一个简单的产品评论系统。

1. **创建 Review 模型：**

   ```python
   # models.py

   from django.db import models
   from store.models import Product

   class Review(models.Model):
       product = models.ForeignKey(Product, on_delete=models.CASCADE)
       author = models.CharField(max_length=255)
       text = models.TextField()
       rating = models.PositiveIntegerField()
       created_at = models.DateTimeField(auto_now_add=True)

       def __str__(self):
           return f"{self.author}'s Review for {self.product}"
   ```

   这个模型表示产品评论，与产品模型通过外键关联。

2. **创建 ReviewSerializer：**

   ```python
   # serializers.py

   from rest_framework import serializers
   from .models import Review

   class ReviewSerializer(serializers.ModelSerializer):
       class Meta:
           model = Review
           fields = ['id', 'product', 'author', 'text', 'rating', 'created_at']
   ```

   创建一个用于 Review 模型的序列化器，定义了你想要在 API 中呈现的字段。

3. **创建 ReviewViewSet：**

   ```python
   # views.py

   from rest_framework import viewsets
   from .models import Review
   from .serializers import ReviewSerializer

   class ReviewViewSet(viewsets.ModelViewSet):
       queryset = Review.objects.all()
       serializer_class = ReviewSerializer
   ```

   创建一个视图集，这里使用了 DRF 的 `ModelViewSet`，它提供了标准的 CRUD 操作。

4. **配置 Reviews URL：**

   ```python
   # reviews/urls.py

   from django.urls import path, include
   from rest_framework.routers import DefaultRouter
   from .views import ReviewViewSet

   router = DefaultRouter()
   router.register(r'reviews', ReviewViewSet, basename='review')

   urlpatterns = [
       path('', include(router.urls)),
   ]
   ```

   在你的主 URL 配置中，包括 ReviewViewSet 的 URL 配置。

5. **在主 URLConf 中包括 Reviews URLs：**

   ```python
   # main/urls.py

   from django.contrib import admin
   from django.urls import path, include

   urlpatterns = [
       path('admin/', admin.site.urls),
       path('api/', include('reviews.urls')),  # Include the reviews app URLs
   ]
   ```

   通过 `include` 添加 Reviews API 的 URL 配置到你的主项目 URL 中。

6. **迁移数据库：**

   运行以下命令来应用新的模型变更：

   ```bash
   python manage.py makemigrations
   python manage.py migrate
   ```

   这将在数据库中创建 Review 模型所需的表。

现在，你的 Reviews API 应该可用于执行 CRUD 操作。你可以通过访问 `/api/reviews/` 来查看所有评论，使用 POST 请求创建新评论，以及使用其他 HTTP 方法执行其他操作。

# kwargs

在Django中，URL模式用于将特定的URL路径映射到相应的视图函数或视图类。当你在URL模式中定义某些参数时，这些参数可以从URL中捕获，并且在视图函数或视图类中可通过`kwargs`（关键字参数的缩写）访问。

通俗地说，就是在URL中如果有一些特定的地方被定义成了参数，比如`<int:product_pk>`，那么当有请求匹配到这个URL时，Django会把这个参数的值捕获下来，并将其放在一个名为`kwargs`的字典中，以便后续的处理使用。

具体来说：

- **URL模式中的参数定义：** 在你的URL模式中，你可以使用尖括号 `< >` 定义参数，例如 `<int:product_pk>`，表示捕获一个整数类型的参数，并将其命名为 `product_pk`。

- **捕获的参数放在kwargs中：** 当有请求匹配到这个URL时，Django会将匹配到的参数的值放在一个字典中，这个字典就是 `kwargs`。

举个例子，假设你有如下的URL模式：

```python
path('products/<int:product_pk>/', views.product_detail)
```

当有请求访问 `/products/42/` 时，Django会将捕获到的参数放在 `kwargs` 字典中，形成类似 `{'product_pk': 42}` 的字典。在视图函数或视图类中，你可以通过 `self.kwargs` 来访问这个字典，然后获取特定参数的值，比如 `self.kwargs['product_pk']` 就会得到 `42`。

所以，`kwargs` 是一个在Django中用于存储从URL中捕获的参数的字典。

## 八.嵌套路由器

需要下载包

```
 pipenv install drf-nested-routers
```

在urls.py中

```python
from django.urls import path
from rest_framework_nested import routers
from . import views

router = routers.DefaultRouter()
router.register('products',views.ProductViewSet)
router.register('collections',views.CollectionViewSet)

products_router=routers.NestedDefaultRouter(router,'products', lookup='product')
products_router.register('reviews',views.ReviewViewSet,basename='product-reviews')
# URLConf
urlpatterns = router.urls + products_router.urls
```

这段代码是使用Django框架和Django REST framework来创建API的一部分。让我逐行解释每一行代码：

1. `from django.urls import path`: 这是导入Django框架中用于定义URL模式的`path`函数。

2. `from rest_framework_nested import routers`: 这是导入Django REST framework中的`routers`模块，它用于处理API路由。

3. `from . import views`: 这是导入当前目录下的`views`模块，该模块包含用于处理API请求的视图函数。

4. `router = routers.DefaultRouter()`: 创建一个默认的Django REST framework路由器。这个路由器用于将API端点映射到视图集。

5. `router.register('products', views.ProductViewSet)`: 将名为'products'的URL端点与`views.ProductViewSet`视图集关联起来。这意味着当访问'products/'时，将使用`ProductViewSet`中定义的方法处理请求。

6. `router.register('collections', views.CollectionViewSet)`: 类似于上一行，将名为'collections'的URL端点与`views.CollectionViewSet`视图集关联起来。

7. `products_router = routers.NestedDefaultRouter(router, 'products', lookup='product')`: 创建一个嵌套路由器，用于处理与'products'相关的嵌套资源。`lookup='product'`指定了嵌套资源的查找字段。

8. `products_router.register('reviews', views.ReviewViewSet, basename='product-reviews')`: 将名为'reviews'的嵌套资源与`views.ReviewViewSet`视图集关联起来。`basename='product-reviews'`定义了该嵌套资源的基本名称。

9. `urlpatterns = router.urls + products_router.urls`: 将主路由器和嵌套路由器的URL模式合并为一个列表，这将用于配置Django应用程序的URLConf（URL配置）。

总体而言，这段代码的目的是创建一个包含产品（products）和相关集合（collections）的API，并且还包括了与产品关联的嵌套资源，即产品的评论（reviews）。

### 在产品评论中我们不想传递产品ID，我们想从URL中阅读

这代码段是一个 Django REST framework 中的视图集（`ViewSet`）的定义，它用于处理关于评论（`Review`）的操作。下面是对其中的`get_serializer_context`方法的解释：

```python
class ReviewViewSet(ModelViewSet):
    queryset = Review.objects.all()
    serializer_class = ReviewSerializer

    def get_serializer_context(self):
        return {'product_id': self.kwargs['product_pk']}
```

1. `get_serializer_context`是 Django REST framework 中的一个方法，用于获取用于序列化或反序列化的上下文数据（serializer context）。

2. 在这个特定的例子中，`get_serializer_context`返回一个字典，其中包含一个键值对 `'product_id': self.kwargs['product_pk']`。

3. `self.kwargs` 是视图类中的一个属性，它包含了从 URL 中捕获的参数。在这里，`'product_pk'` 是一个 URL 参数，表示产品的主键（或ID）。

4. 因此，`{'product_id': self.kwargs['product_pk']}` 的作用是在序列化或反序列化评论时，将当前请求中传递的产品的主键（`product_pk`）作为上下文数据提供给序列化器。这样，评论的序列化器就可以根据产品的主键来执行一些定制的逻辑或处理。

总体而言，`get_serializer_context` 方法的目的是在处理评论时，将与评论相关的上下文信息（在这里是产品的主键）传递给评论的序列化器，以便进行更灵活的序列化或反序列化操作。

当你使用 Django REST framework 中的序列化器来处理数据创建时，`create` 方法是一个特殊的方法，用于在数据库中创建新对象。让我逐行解释你提供的代码：

```python
def create(self, validated_data):
    product_id = self.context['product_id']
    return Review.objects.create(product_id=product_id, **validated_data)
```

1. **`def create(self, validated_data):`：**
   - 这是 `ReviewSerializer` 中的 `create` 方法的定义。在序列化器中，`create` 方法用于处理在创建新对象时的逻辑。

2. **`product_id = self.context['product_id']`：**
   - 这一行从序列化器的上下文（`context`）中获取了名为 `product_id` 的值。上下文是在视图或视图集中设置的，这里是通过 `get_serializer_context` 方法设置的。

3. **`return Review.objects.create(product_id=product_id, **validated_data)`：**
   - 在这一行中，`Review.objects.create` 是Django模型管理器的方法，用于在数据库中创建新的 `Review` 对象。
   - `product_id=product_id`：将从上下文中获取的 `product_id` 值赋给 `Review` 模型的 `product_id` 字段。
   - `**validated_data`：这是 Python 中的一种语法，用于将字典中的键值对作为关键字参数传递给函数。在这里，它用于将从请求中传递并经过验证的数据传递给 `create` 方法，确保所有必需的字段都被正确地传递给 `Review` 模型的 `create` 方法。

整体而言，这个 `create` 方法的目的是在创建评论对象时，将从上下文中获取的产品的主键与评论的其他数据一起保存到数据库中。这种方式可以在创建评论时与相关产品进行关联，保证了数据的完整性。

#### 首先，让我们回顾一下整个流程：

1. 在URL中，有一个参数叫做 `product_pk`，表示产品的主键（ID）。
2. 在视图中，通过 `get_serializer_context` 方法，将 `product_pk` 放入序列化器的上下文中。
3. 在序列化器的 `create` 方法中，通过 `self.context['product_id']` 获取了产品的主键。
4. 在 `Review` 模型的创建时，将产品的主键与评论的其他数据一起保存到数据库中。

这个设计的目的是使得在创建评论时不需要显式传递产品的主键，而是从URL中读取。这种方式更符合 RESTful 设计的原则，因为产品ID是与URL资源关联的，而不是作为请求主体中的数据传递。

例如，如果你想创建一个新的评论，你的请求URL可能是这样的：`/products/1/reviews/`，其中 `1` 是产品的主键。这个URL告诉服务器你想在产品1下创建一条评论，而无需在请求主体中显式提供产品ID，因为它已经在URL中了。

这种方式使得API更加直观和符合RESTful设计原则，同时减少了在请求主体中传递冗余信息的需要。

## 九.过滤

**访问127.0.0：8000/store/products?collection_id=1,获得collection_id=1的所有产品**

```python

class ProductViewSet(ModelViewSet):
    serializer_class = ProductSerializer

    def get_queryset(self):
        queryset = Product.objects.all()
        collection_id = self.request.query_params.get('collection_id')
        if collection_id is not None:
            queryset = queryset.filter(collection_id = collection_id)

        return queryset

```

这段代码是 `ProductViewSet` 中的 `get_queryset` 方法。它的作用是根据查询参数 `collection_id` 来过滤产品的查询集。

让我逐行解释：

1. **`queryset = Product.objects.all()`：**
   - 这一行创建了一个包含所有产品的初始查询集。`Product.objects.all()` 返回一个包含所有 `Product` 模型对象的查询集。

2. **`collection_id = self.request.query_params.get('collection_id')`：**
   - 这一行从请求的查询参数中获取名为 `collection_id` 的值。`self.request` 包含了当前请求的信息，而 `query_params` 是一个包含请求中查询参数的字典。`get('collection_id')` 尝试获取名为 `collection_id` 的查询参数的值，如果没有则返回 `None`。

3. **`if collection_id is not None:`：**
   - 这一行检查是否有传递 `collection_id` 查询参数。如果 `collection_id` 不是 `None`，说明请求中包含了 `collection_id`。

4. **`queryset = queryset.filter(collection_id=collection_id)`：**
   - 如果 `collection_id` 不是 `None`，则使用 `filter` 方法过滤查询集。这样，最终的查询集只包含那些 `collection_id` 与请求中传递的值匹配的产品。

整个方法的目的是根据请求中是否包含 `collection_id` 查询参数，来动态调整返回的产品列表。如果请求中没有传递 `collection_id`，那么返回所有产品；如果传递了 `collection_id`，则返回与之匹配的产品列表。这使得 API 能够根据请求的参数提供灵活的过滤和查询功能。

```python
from django.urls import path
from rest_framework_nested import routers
from . import views


router = routers.DefaultRouter()
router.register('products',views.ProductViewSet,basename='products')
router.register('collections',views.CollectionViewSet)
```

## 十.通用过滤

下第三方过滤器，就可以不用手动写那么多复杂代码

```
pipenv install django-filter
```

每一次安装第三方包，都应该把该包放入应用程序列表中

```python
from django_filters.rest_framework import DjangoFilterBackend


class ProductViewSet(ModelViewSet):
    queryset = Product.objects.all()
    serializer_class = ProductSerializer
    filter_backends = [DjangoFilterBackend] 
    filterset_fields = ['collection_id'] #[]里面可以填想要过滤的字段
    
```

1. **`filter_backends = [DjangoFilterBackend]`：**
   - 配置了视图集使用的过滤后端。在这里，`DjangoFilterBackend` 被添加到 `filter_backends` 列表中，表明使用了 Django REST framework 中提供的过滤器后端，该后端允许在查询中使用过滤器来过滤结果集。
2. **`filterset_fields = ['collection_id']`：**
   - 指定了在使用过滤器时可以过滤的字段。在这里，`collection_id` 被添加到 `filterset_fields` 中，表示可以通过 API 查询参数来过滤 `Product` 模型对象，只返回与指定 `collection_id` 相关的产品。

这个视图集的配置使得它可以根据传递的查询参数动态地过滤产品。例如，通过访问 `/products/?collection_id=1` 可以只返回与 `collection_id` 为 1 的产品相关的数据。这提供了一种灵活的方式，让客户端可以根据特定条件检索所需的产品数据。

想要自定义过滤器可以查看官方网站

```
https://django-filter.readthedocs.io/en/stable/
```

## 十一.搜索

```python
from rest_framework.filters import SearchFilter


class ProductViewSet(ModelViewSet):
    queryset = Product.objects.all()
    serializer_class = ProductSerializer
    filter_backends = [DjangoFilterBackend,SearchFilter]
    filterset_fields = ['collection_id']
    search_fields = ['title','description']
    
```

**导入 `SearchFilter`：**

```python
from rest_framework.filters import SearchFilter
```

- 导入了 Django REST framework 提供的 `SearchFilter` 过滤器，该过滤器用于支持搜索功能。

1. **`filter_backends = [DjangoFilterBackend, SearchFilter]`：**
   - 配置了视图集使用的过滤后端。`DjangoFilterBackend` 负责使用过滤器来过滤结果集，而 `SearchFilter` 负责启用搜索功能。
2. **`filterset_fields = ['collection_id']`：**
   - 指定了在使用过滤器时可以过滤的字段。在这里，`collection_id` 被添加到 `filterset_fields` 中，表示可以通过 API 查询参数来过滤 `Product` 模型对象，只返回与指定 `collection_id` 相关的产品。
3. **`search_fields = ['title', 'description']`：**
   - 指定了允许搜索的字段。在这里，`title` 和 `description` 被添加到 `search_fields` 中，表示可以通过 API 查询参数进行搜索，搜索结果将包含包含匹配搜索关键字的产品。

通过添加 `SearchFilter`，你的 API 就支持根据标题和描述字段进行搜索了。例如，通过访问 `/products/?search=keyword` 可以搜索包含关键字的产品。这为客户端提供了更灵活的方式来检索和过滤数据。

## 十二.对数据进行排序

```python
from rest_framework.filters import SearchFilter,OrderingFilter


class ProductViewSet(ModelViewSet):
    queryset = Product.objects.all()
    serializer_class = ProductSerializer
    filter_backends = [DjangoFilterBackend,SearchFilter,OrderingFilter]
    filterset_fields = ['collection_id']
    search_fields = ['title','description']
    ordering_fields = ['unit_price','last_update']
```

## 十三.分页

1.全局进行排序

```python
REST_FRAMEWORK = {
    'COERCE_DECIMAL_TO_STRING': False ,
    'DEFAULT_PAGINATION_CLASS': 'rest_framework.pagination.PageNumberPagination',
    'PAGE_SIZE' : 10
}
```

2.建一个pagination.py文件

```python
from rest_framework.pagination import PageNumberPagination

class DefaultPagination(PageNumberPagination):
    page_size = 10
```

去想要分页的view类中运用

```python
from store.pagination import DefaultPagination #导入类

class ProductViewSet(ModelViewSet):
    queryset = Product.objects.all()
    serializer_class = ProductSerializer
    pagination_class = DefaultPagination #调用类
```





# 设计购物车API

urls.py

```python
from django.urls import path
from rest_framework_nested import routers
from . import views


router = routers.DefaultRouter()
router.register('products',views.ProductViewSet,basename='products')
router.register('collections',views.CollectionViewSet)
router.register('carts',views.CartViewSet)

products_router=routers.NestedDefaultRouter(router,'products', lookup='product')
products_router.register('reviews',views.ReviewViewSet,basename='product-reviews')

carts_router = routers.NestedDefaultRouter(router,'carts',lookup = 'cart')
carts_router.register('items', views.CartItemViewSet,basename='cart-items')

```

views.py

```python
from django.shortcuts import get_object_or_404
from rest_framework.response import Response
from .models import Product, Collection, Review,Cart,CartItem
from .serializers import UpdateCartItemSerializer,ProductSerializer, CollectionSerializers, ReviewSerializer,CartSerializer,CartItemSerializer,AddCartItemSerializer
from rest_framework import status
from django.db.models import Count
from rest_framework.viewsets import ModelViewSet,GenericViewSet
from django_filters.rest_framework import DjangoFilterBackend
from rest_framework.filters import SearchFilter, OrderingFilter
from store.pagination import DefaultPagination
from rest_framework.mixins import CreateModelMixin,RetrieveModelMixin,DestroyModelMixin


class ProductViewSet(ModelViewSet):
    queryset = Product.objects.all()
    serializer_class = ProductSerializer
    filter_backends = [DjangoFilterBackend, SearchFilter, OrderingFilter]
    filterset_fields = ['collection_id']
    search_fields = ['title', 'description']
    ordering_fields = ['unit_price', 'last_update']
    pagination_class = DefaultPagination

    def get_serializer_context(self):
        return {'request': self.request}

    def delete(self, request, pk):
        product = get_object_or_404(Product, pk=pk)
        if product.orderitem_set.count() > 0:
            return Response({'error': '产品不能被删除，因为他与订单项相关联'}, status=status.HTTP_405_METHOD_NOT_ALLOWED)
        product.delete()
        return Response(status=status.HTTP_204_NO_CONTENT)


class CollectionViewSet(ModelViewSet):
    queryset = Collection.objects.annotate(
        products_count=Count('products')).all()
    serializer_class = CollectionSerializers

    def delete(self, request, pk):
        collection = get_object_or_404(Collection, pk=pk)
        if collection.products.count() > 0:
            return Response({'error': '产品不能被删除，因为他与订单项相关联'}, status=status.HTTP_405_METHOD_NOT_ALLOWED)
        Product.delete()
        return Response(status=status.HTTP_204_NO_CONTENT)


class ReviewViewSet(ModelViewSet):
    serializer_class = ReviewSerializer

    def get_queryset(self):
        return Review.objects.filter(product_id=self.kwargs['product_pk'])

    def get_serializer_context(self):
        return {'product_id': self.kwargs['product_pk']}


class CartViewSet(CreateModelMixin,
                  GenericViewSet,
                  DestroyModelMixin,
                  RetrieveModelMixin):
    queryset = Cart.objects.prefetch_related('items__product').all()
    serializer_class = CartSerializer
    

class CartItemViewSet(ModelViewSet):
    http_method_names = ['get','post','patch','delete']
    
    def get_serializer_class(self):
        if self.request.method == 'POST':
            return AddCartItemSerializer
        elif self.request.method == 'PATCH':
            return UpdateCartItemSerializer
        return CartItemSerializer
    
    def get_serializer_context(self):
        return {'cart_id': self.kwargs['cart_pk']}

    def get_queryset(self):
        return CartItem.objects\
            .filter(cart_id = self.kwargs['cart_pk'])\
            .select_related('product')



```

serializers.py

```python
from rest_framework import serializers
from store.models import Product ,Collection,Review,Cart,CartItem
from decimal import Decimal


class CollectionSerializers(serializers.ModelSerializer):
    class Meta:
        model = Collection  
        fields = ['id','title','products_count']

    products_count  = serializers.IntegerField(read_only=True)#设为只读，不可以更改

class ProductSerializer(serializers.ModelSerializer):
    class Meta:
        model = Product
        fields= ['id','title','description','slug','inventory','unit_price','price_with_tax','collection']

    price_with_tax = serializers.SerializerMethodField(method_name='calculate_tax')
    def calculate_tax(self,product: Product):
        return product.unit_price * Decimal(1.1)


class ReviewSerializer(serializers.ModelSerializer):
    class Meta:
        model = Review
        fields = ['id','date', 'name','description']

    def create(self, validated_data):
        product_id = self.context['product_id']
        return Review.objects.create(product_id= product_id , **validated_data)

class SimpleProductSerializer(serializers.ModelSerializer):
    class Meta:
        model = Product
        fields = ['id','title','unit_price']    

class CartItemSerializer(serializers.ModelSerializer):
    product = SimpleProductSerializer(read_only = True)
    total_price = serializers.SerializerMethodField()

    def get_total_price(self, cart_item: CartItem):
        return cart_item.quantity * cart_item.product.unit_price

    class Meta:
        model = CartItem
        fields = ['id','product','quantity','total_price']

class CartSerializer(serializers.ModelSerializer):
    id = serializers.UUIDField(read_only = True)
    items = CartItemSerializer(many = True,read_only = True)
    total_price = serializers.SerializerMethodField()

    def get_total_price(self,cart):
        return sum([item.quantity * item.product.unit_price for item in cart.items.all()])

    class Meta:
        model = Cart
        fields = ['id','items','total_price']
#0708c739-69b3-4c46-b950-a8320c427cad

class AddCartItemSerializer(serializers.ModelSerializer):
    product_id = serializers.IntegerField()

    def validate_product_id(self,value):
        if not Product.objects.filter(pk=value).exists():
            raise serializers.ValidationError('No product with the given ID was found.')
        return value

    def save(self, **kwargs):
        cart_id = self.context['cart_id']
        product_id = self.validated_data['product_id']
        quantity = self.validated_data['quantity']

        try:
            cart_item = CartItem.objects.get(cart_id =cart_id , product_id = product_id)
            cart_item.quantity +=quantity
            cart_item.save()
            self.instance= cart_item
        except CartItem.DoesNotExist:
            self.instance = CartItem.objects.create(cart_id=cart_id, **self.validated_data)

        return self.instance 


    class Meta:
        model = CartItem
        fields = ['id','product_id','quantity']

class UpdateCartItemSerializer(serializers.ModelSerializer):
    class Meta:
        model = CartItem
        fields = ['quantity']
```

models.py

```python
from django.db import models
from django.core.validators import MinValueValidator
from uuid import uuid4


class Promotion(models.Model):
    description = models.CharField(max_length=255)
    discount = models.FloatField()


class Collection(models.Model):
    title = models.CharField(max_length=255)
    featured_product = models.ForeignKey(
        'Product', on_delete=models.SET_NULL, null=True, related_name='+')

    def __str__(self) -> str:
        return self.title
    
    class Meta:
        ordering = ['title']


class Product(models.Model):
    title = models.CharField(max_length=255)
    slug = models.SlugField()
    description = models.TextField(null=True,blank=True)
    unit_price = models.DecimalField(
        max_digits=6,
        decimal_places=2,
        validators=[MinValueValidator(1)])
    inventory = models.IntegerField()
    last_update = models.DateTimeField(auto_now=True)
    collection = models.ForeignKey(Collection, on_delete=models.PROTECT,related_name='products')
    promotions = models.ManyToManyField(Promotion,blank=True)
    
    def __str__(self) -> str:
        return self.title
    
    class Meta:
        ordering = ['title']

class Customer(models.Model):
    MEMBERSHIP_BRONZE = 'B'
    MEMBERSHIP_SILVER = 'S'
    MEMBERSHIP_GOLD = 'G'

    MEMBERSHIP_CHOICES = [
        (MEMBERSHIP_BRONZE, 'Bronze'),
        (MEMBERSHIP_SILVER, 'Silver'),
        (MEMBERSHIP_GOLD, 'Gold'),
    ]
    first_name = models.CharField(max_length=255)
    last_name = models.CharField(max_length=255)
    email = models.EmailField(unique=True)
    phone = models.CharField(max_length=255)
    birth_date = models.DateField(null=True)
    membership = models.CharField(
        max_length=1, choices=MEMBERSHIP_CHOICES, default=MEMBERSHIP_BRONZE)
    
    def __str__(self) -> str:
        return f'{self.first_name} {self.last_name}'
    
    class Meta:
        ordering = ['first_name', 'last_name']
   

class Order(models.Model):
    PAYMENT_STATUS_PENDING = 'P'
    PAYMENT_STATUS_COMPLETE = 'C'
    PAYMENT_STATUS_FAILED = 'F'
    PAYMENT_STATUS_CHOICES = [
        (PAYMENT_STATUS_PENDING, 'Pending'),
        (PAYMENT_STATUS_COMPLETE, 'Complete'),
        (PAYMENT_STATUS_FAILED, 'Failed')
    ]

    placed_at = models.DateTimeField(auto_now_add=True)
    payment_status = models.CharField(
        max_length=1, choices=PAYMENT_STATUS_CHOICES, default=PAYMENT_STATUS_PENDING)
    customer = models.ForeignKey(Customer, on_delete=models.PROTECT)


class OrderItem(models.Model):
    order = models.ForeignKey(Order, on_delete=models.PROTECT,)
    product = models.ForeignKey(Product, on_delete=models.PROTECT)
    quantity = models.PositiveSmallIntegerField()
    unit_price = models.DecimalField(max_digits=6, decimal_places=2)


class Address(models.Model):
    street = models.CharField(max_length=255)
    city = models.CharField(max_length=255)
    customer = models.ForeignKey(
        Customer, on_delete=models.CASCADE)


class Cart(models.Model):
    id = models.UUIDField(primary_key=True,default=uuid4)
    created_at = models.DateTimeField(auto_now_add=True)


class CartItem(models.Model):
    cart = models.ForeignKey(Cart, on_delete=models.CASCADE,related_name='items')
    product = models.ForeignKey(Product, on_delete=models.CASCADE)
    quantity = models.PositiveSmallIntegerField(
        validators=[MinValueValidator(1)]
    )

    class Meta:
        unique_together = [['cart','product']]


class Review(models.Model):
    product = models.ForeignKey(Product,on_delete=models.CASCADE,related_name='reviews')
    name = models.CharField(max_length=255)
    description = models.TextField()
    date = models.DateField(auto_now_add=True)
```









# Django 身份验证系统

## 一.自定义用户模型

在Django中，**扩展用户模型**和**创建用户配置文件**是两种不同的方法，用于添加额外的信息到用户身上。下面是它们之间的主要区别：

1. **扩展用户模型**：
   - **方法**：通过创建一个新的用户模型，该模型继承自`AbstractUser`或`AbstractBaseUser`，并在其中添加额外的字段。
   - **例子**：在前面的回答中，我提到了通过继承`AbstractUser`来创建自定义用户模型的方法。
   - **优点**：这种方法适用于在用户模型本身上添加较少的额外信息，并且不需要创建新的模型。它更直接，更紧密地集成到用户模型中。
   - **缺点**：如果你需要与用户模型关联的信息较多，或者你的应用需要多个相关联的配置，可能会变得复杂。
   
2. **创建用户配置文件**：
   - **方法**：通过创建一个新的模型，该模型与用户模型使用`OneToOneField`或其他关联字段关联，将额外的信息存储在这个新的模型中。这个新的模型通常称为用户配置文件。
   - **例子**：在前面的回答中，我提到了创建一个`UserProfile`模型，该模型与用户模型通过`OneToOneField`关联。
   - **优点**：这种方法适用于你需要存储大量额外信息，或者你希望将相关的配置拆分到单独的模型中。它使得代码更有组织性，更易于维护。
   - **缺点**：需要创建并维护两个模型，而且在处理用户信息时可能需要进行更多的查询。

选择哪种方法取决于你的具体需求和应用程序的结构。如果你只需添加几个额外的字段，并且这些字段紧密地与用户相关，那么扩展用户模型可能是一个更简单的选择。如果你有大量额外的信息或者希望将用户配置拆分到单独的模型中，那么创建用户配置文件可能更合适。

## 二.扩展用户模型

扩展用户模型是一种常见的需求，允许你添加额外的字段以满足你的应用程序的特定要求。在Django中，有两种主要的扩展用户模型的方法：一是使用`OneToOneField`，另一种是继承`AbstractUser`。

### 使用 `OneToOneField`

1. **创建一个新的模型**：

   在你的应用的`models.py`中创建一个新的模型，该模型包含你想要添加的额外字段。然后，使用`OneToOneField`将它与用户模型关联起来。

   ```python
   from django.contrib.auth.models import User
   from django.db import models
   
   class UserProfile(models.Model):
       user = models.OneToOneField(User, on_delete=models.CASCADE)
       bio = models.TextField(blank=True)
       profile_picture = models.ImageField(upload_to='profile_pics', blank=True)
   ```

2. **创建信号以自动创建或更新关联模型**：

   你可以使用Django信号来确保每次创建新用户时都会创建相应的`UserProfile`。添加信号的代码可能如下所示：

   ```python
   from django.db.models.signals import post_save
   from django.dispatch import receiver
   
   @receiver(post_save, sender=User)
   def create_user_profile(sender, instance, created, **kwargs):
       if created:
           UserProfile.objects.create(user=instance)
   
   @receiver(post_save, sender=User)
   def save_user_profile(sender, instance, **kwargs):
       instance.userprofile.save()
   ```

3. **在注册表单中添加额外字段**：

   如果你使用Django的内置表单系统，确保在用户注册表单中包含新的字段。

### 继承 `AbstractUser` 

1. **创建一个新的用户模型**：

   在你的应用的`models.py`中创建一个新的用户模型，继承自`AbstractUser`，并添加你自己的字段。

   ```python
   from django.contrib.auth.models import AbstractUser
   from django.db import models

   class CustomUser(AbstractUser):
       bio = models.TextField(blank=True)
       profile_picture = models.ImageField(upload_to='profile_pics', blank=True)
   ```

2. **更新 `settings.py` 中的用户模型**：

   在你的项目的`settings.py`文件中，更新`AUTH_USER_MODEL`设置以指定使用你的新用户模型。

   ```python
   # settings.py
   AUTH_USER_MODEL = 'yourapp.CustomUser'
   ```

   替换 `yourapp` 为包含你的 `CustomUser` 类的应用的实际名称。

3. **创建并应用数据库迁移**：

   运行以下命令创建并应用数据库迁移以更新数据库模式：

   ```bash
   python manage.py makemigrations
   python manage.py migrate
   ```

请根据你的具体需求选择其中一种方法。使用 `OneToOneField` 更加灵活，因为你可以与多个模型关联，但在某些情况下，继承 `AbstractUser` 可能更为简单。在任何情况下，确保在进行模型更改之前备份数据库，并谨慎测试以确保一切正常工作。

## 三.创建用户配置文件

创建用户配置文件是一种常见的做法，特别是当你需要为用户存储额外的信息时。通常，用户配置文件是一个与用户模型相关联的模型，通过 `OneToOneField` 与用户模型建立关系。以下是一个简单的例子，演示如何在 Django 中创建用户配置文件：

1. **创建用户配置文件模型**：

   在你的应用的 `models.py` 文件中，创建一个用户配置文件模型。这个模型通常包含额外的信息字段，并与用户模型通过 `OneToOneField` 关联。

   ```python
   from django.contrib.auth.models import User
   from django.db import models

   class UserProfile(models.Model):
       user = models.OneToOneField(User, on_delete=models.CASCADE)
       bio = models.TextField(blank=True)
       profile_picture = models.ImageField(upload_to='profile_pics', blank=True)

       def __str__(self):
           return self.user.username
   ```

2. **迁移数据库**：

   运行以下命令创建并应用数据库迁移，以确保新的模型被添加到数据库中：

   ```bash
   python manage.py makemigrations
   python manage.py migrate
   ```

3. **在注册视图中创建用户配置文件**：

   当用户注册时，你可以在注册视图中创建用户配置文件。以下是一个简单的例子：

   ```python
   from django.contrib.auth.forms import UserCreationForm
   from django.shortcuts import render, redirect
   from .models import UserProfile

   def register(request):
       if request.method == 'POST':
           form = UserCreationForm(request.POST)
           if form.is_valid():
               user = form.save()
               # 创建用户配置文件
               UserProfile.objects.create(user=user)
               return redirect('login')
       else:
           form = UserCreationForm()
       return render(request, 'registration/register.html', {'form': form})
   ```

   这里假设你使用 Django 的内置的用户注册表单 `UserCreationForm`，但你也可以使用自定义的注册表单。

4. **在视图或模板中访问用户配置文件**：

   一旦用户配置文件被创建，你可以在视图或模板中访问它的信息。例如，通过在视图中使用 `user.userprofile` 或在模板中使用 `{{ user.userprofile.field_name }}`。

   ```python
   def profile(request):
       user_profile = request.user.userprofile
       return render(request, 'profile.html', {'user_profile': user_profile})
   ```

   在模板中：

   ```html
   <h2>{{ user_profile.user.username }}'s Profile</h2>
   <p>Bio: {{ user_profile.bio }}</p>
   <img src="{{ user_profile.profile_picture.url }}" alt="Profile Picture">
   ```

这只是一个简单的示例，你可以根据你的应用程序的需求和设计进行更复杂的用户配置文件的创建和使用。

## 四.group是权限的集合





# 确保API安全

## 一.添加Django认证终端

**令牌的作用为当我们需要访问受保护的端点时，我们需要去得到权限，以一种令牌的形式来访问受保护的端点**

Djoser是一个用于Django的REST框架的扩展，它提供了一组用于处理身份验证、用户注册、密码重置等功能的视图和端点。其主要目的是简化处理用户身份验证和账户管理的流程，为Django开发人员提供了一组灵活的工具。

以下是Djoser的一些主要功能：

1. **用户注册和认证：** Djoser提供了视图和端点，使用户能够注册账户并通过电子邮件确认身份。
2. **密码重置：** 用户可以请求通过电子邮件进行密码重置，并且Djoser提供了相应的视图和端点来处理这个过程。
3. **基于令牌的身份验证：** Djoser支持基于令牌的身份验证，可以用于安全地验证用户的身份。
4. **令牌的创建和刷新：** Djoser提供了端点，使客户端能够获取访问令牌，并在需要时刷新令牌。
5. **用户配置：** 可以轻松配置用户模型，例如通过使用电子邮件或用户名作为登录字段。
6. **可扩展性：** Djoser是可扩展的，允许你自定义视图、序列化器和其他组件以满足项目的特定需求。

通过使用Djoser，开发人员能够更轻松地集成身份验证和用户管理功能，而不必从头开始编写这些功能。这提高了开发效率，同时也确保了一定程度的安全性和最佳实践。

https://djoser.readthedocs.io/en/latest/getting_started.html#installation 这个链接提供第三方库关于djoser包 **配置相关文件**

## 二.注册用户

我们可以访问http://127.0.0.1:8000/auth/users/去注册用户

如果我们想去添加额外的字段如 ‘first_name’, 'last_name' 需要去自定义创建用户序列化

这个序列化需要放到core应用程序中的serializers.py文件中

```python
from djoser.serializers import UserCreateSerializer as BaseUserCreateSerializer

class UserCreateSerializer(BaseUserCreateSerializer):

    class Meta(BaseUserCreateSerializer.Meta):
        fields = ['id','username','password','email','first_name','last_name',]
```

还需要到settings.py中去设置该创建用户的序列化器在哪个地方

```python
DJOSER = {
    'SERIALIZERS':{
        'user_create' : 'core.serializers.UserCreateSerializer'
    }
}
```



## 三.构建配置文件 API

正常配置API



## 四.对用户进行身份验证

身份令牌（Token）是一种在身份验证（Authentication）过程中用于确认用户身份的一种方式。在 Web 开发中，常见的身份验证方式包括用户名和密码，但为了增加安全性和方便性，使用令牌成为了一种常见的选择。

JSON Web Token（JWT）是一种开放标准（RFC 7519），定义了一种紧凑且自包含的方式，用于在各方之间作为 JSON 对象安全地传输信息。JWT 可以包含用户的身份信息，也可以包含其他元数据，例如权限或其他声明。在身份验证过程中，用户通常在登录成功后会获得一个 JWT，然后**在后续的请求中将该令牌作为身份验证凭证进行传递。**

对于 Django REST Framework（DRF）来说，`/auth/jwt/create` 是一个常见的端点，用于生成 JWT。用户可以通过提供有效的用户名和密码，向该端点发送 POST 请求，服务器将验证用户身份，如果验证成功，将生成一个包含用户信息的 JWT，并将其返回给客户端。客户端在后续的请求中，可以将该 JWT 放置在请求头中，作为身份验证的凭证。

使用 JWT 的好处包括：

1. **状态无关性（Stateless）：** 服务器不需要存储用户的登录状态，因为所有必要的信息都包含在 JWT 中。
   
2. **跨域支持：** 由于 JWT 是在客户端生成的，因此可以轻松地在不同的域之间进行身份验证。

3. **可扩展性：** JWT 可以包含任意的声明，可以用于扩展身份验证系统的功能。

4. **安全性：** JWT 使用数字签名或加密来确保令牌的完整性和安全性。

需要注意的是，在使用 JWT 进行身份验证时，必须确保令牌的安全性，避免在不安全的环境中泄漏令牌。此外，令牌的有效期也需要合理设置，以平衡安全性和用户体验。



http://127.0.0.1:8000/auth/jwt/create 通过访问这个链接，去登录，然后会获得用户令牌

可以在settings.py文件中设置令牌时间

```python
from datetime import timedelta

SIMPLE_JWT = {
    "ACCESS_TOKEN_LIFETIME": timedelta(days=1),
}
```



http://127.0.0.1:8000/auth/jwt/refresh通过访问refresh端点把refresh令牌传上去可以得到访问令牌

## 五.获取当前用户

**需要下载modheader插件**

ModHeader 是一个用于浏览器的插件，主要用于修改 HTTP 请求和响应的标头信息。这个插件可以让开发者更方便地模拟不同的网络环境、测试特定的 HTTP 头、修改请求和响应等。

具体而言，ModHeader 提供了一个用户界面，允许你添加、编辑和删除请求和响应的标头。这对于调试和测试网络应用程序时非常有用，特别是在处理跨域请求、设置 Cookie、验证身份等方面。

一些常见的用途包括：

1. **模拟不同的网络环境：** 你可以使用 ModHeader 来模拟不同的网络条件，如慢速网络、断开的连接等，以测试应用在不同网络环境下的性能。

2. **设置自定义标头：** 你可以添加自定义的 HTTP 标头，以便测试应用对特定标头的处理。

3. **修改请求和响应：** 你可以编辑请求和响应的标头信息，包括修改 User-Agent、添加授权标头等。

4. **处理跨域请求：** 在开发阶段，为了模拟跨域请求，你可以使用 ModHeader 添加 CORS 相关的标头，以便测试应用对跨域请求的处理。

总的来说，ModHeader 是一个方便的工具，可以帮助开发者更轻松地进行网络调试和测试。注意，它通常用于开发和测试阶段，不建议在生产环境中使用。



需要访问所有用户，需要下载modheader插件 然后需要在里面发送JWT令牌才能访问http://127.0.0.1:8000/auth/users/me/

想要在http://127.0.0.1:8000/auth/users/me/里面查看first_name,last_name,想要去自定义序列化器

**用完modheader插件一定一定要关掉**

## 六.如何获取或更新当前用户的配置文件

**前提想要使用modheader插件,来获取当前用户配置文件**

```python
class CustomerViewSet(CreateModelMixin,RetrieveModelMixin, UpdateModelMixin,GenericViewSet):
    queryset = Customer.objects.all()
    serializer_class = CustomerSerializer

    @action(detail=False,methods=['GET','PUT'])
    def me(self,request):
        (customer,created) = Customer.objects.get_or_create(user_id = request.user.id)
        if request.method == 'GET':
            serializer = CustomerSerializer(customer)
            return Response(serializer.data)
        elif request.method == 'PUT':
            serializer = CustomerSerializer(customer, data=request.data)
            serializer.is_valid(raise_exception=True)
            serializer.save()
            return Response(serializer.data)

```

这是一个Django REST framework中的`ViewSet`，名为`CustomerViewSet`，并且它使用了一些混合（mixins）以及自定义的`@action`装饰器。

1. `CreateModelMixin`：提供了处理创建对象的功能。
2. `RetrieveModelMixin`：提供了处理检索（获取）对象的功能。
3. `UpdateModelMixin`：提供了处理更新对象的功能。
4. `GenericViewSet`：是一个通用的视图集，结合了以上三个混合以提供通用的视图功能。

然后，你在`CustomerViewSet`中定义了一个自定义的动作`me`，这个动作是一个特殊的视图，用于处理关于当前用户的信息。具体解释如下：

- `@action(detail=False, methods=['GET', 'PUT'])`：这是一个`@action`装饰器，表示`me`是一个自定义的动作，`detail=False`表示这个动作不是针对某个具体对象的，而是整个视图集的。
  
- `def me(self, request)`：这是`me`动作的具体实现。在这个动作中，你首先尝试从数据库中获取与当前用户相关联的`Customer`对象，如果不存在则创建一个新的对象。

- `if request.method == 'GET':`：如果请求的方法是GET，表示客户端希望获取当前用户的信息。在这种情况下，你使用`CustomerSerializer`将`customer`对象序列化为JSON格式，并返回包含该JSON数据的`Response`对象。

- `elif request.method == 'PUT':`：如果请求的方法是PUT，表示客户端希望更新当前用户的信息。在这种情况下，你使用`CustomerSerializer`将`customer`对象与请求中的数据进行反序列化和验证，然后保存更新后的对象。最后，返回包含更新后的JSON数据的`Response`对象。

这个`me`动作的目的是提供一个端点，使客户端能够获取或更新与当前用户相关的`Customer`对象的信息。



## 七.应用权限

在Django中，应用权限是指在应用中定义的控制访问的规则。这些规则确定了哪些用户有权执行特定操作，例如查看、创建、更新或删除对象。Django提供了一种灵活的权限系统，允许你定义和控制应用中的访问级别。

以下是在Django中处理应用权限的一般步骤：

1. **导入权限类：** Django提供了一些内置的权限类，如`IsAuthenticated`（用户已登录）和`IsAdminUser`（用户是管理员）。你可以从`django.contrib.auth.permissions`中导入这些权限类，或者自定义自己的权限类。

   ```python
   from django.contrib.auth.permissions import IsAuthenticated
   ```

2. **定义权限类：** 如果内置权限类不符合你的需求，你可以自定义权限类。一个权限类通常继承自`BasePermission`，然后实现`has_permission`和/或`has_object_permission`方法。

   ```python
   from rest_framework.permissions import BasePermission

   class CustomPermission(BasePermission):
       def has_permission(self, request, view):
           # 自定义权限逻辑
           return True  # 或者根据需要返回 True 或 False
   ```

3. **将权限应用于视图：** 在你的Django视图中，你可以使用`permission_classes`属性来指定视图所需的权限类。例如，如果你要确保只有已经登录的用户可以访问视图，可以这样做：

   ```python
   from rest_framework.permissions import IsAuthenticated

   class MyApiView(APIView):
       permission_classes = [IsAuthenticated]

       def get(self, request):
           # 处理 GET 请求的逻辑
           return Response("只有已登录用户才能访问这个视图。")
   ```

   如果你使用Django的类视图，你也可以在`get_permissions`方法中动态设置权限：

   ```python
   from rest_framework.permissions import IsAuthenticated

   class MyViewSet(ModelViewSet):
       def get_permissions(self):
           if self.action == 'list':
               permission_classes = [IsAuthenticated]
           else:
               permission_classes = [CustomPermission]

           return [permission() for permission in permission_classes]
   ```

4. **全局默认权限：** 你还可以在Django REST framework的设置中设置全局默认权限。这样，如果某个视图未指定权限类，将使用这些全局默认权限。

   ```python
   REST_FRAMEWORK = {
       'DEFAULT_PERMISSION_CLASSES': [
           'rest_framework.permissions.IsAuthenticated',
       ],
   }
   ```

这些步骤提供了一种在Django中定义和应用应用权限的方式。根据你的需求，你可以选择使用内置权限类，自定义权限类，或者在视图中动态设置权限。	

### 实例

**我希望所有用户都可以查看顾客，但是如果想要更新顾客需要登录**

```python
class CustomerViewSet(CreateModelMixin,RetrieveModelMixin, UpdateModelMixin,GenericViewSet):
    queryset = Customer.objects.all()
    serializer_class = CustomerSerializer
    permission_classes = [IsAuthenticated]

    def get_permissions(self):
        if self.request.method == 'GET':
            return [AllowAny()]
        return [IsAuthenticated()]
```

1. **权限设置：**
   - `permission_classes`: 指定视图集所需的权限类。在这里，`IsAuthenticated` 表示只有已经通过身份验证的用户才能执行相关操作。
2. **`get_permissions` 方法：**
   - 定义了动态获取权限的方法。在这里，根据请求的方法类型，返回不同的权限类列表。
     - 对于 `GET` 请求，返回 `AllowAny()`，表示允许任何人执行该操作。
     - 对于其他请求（如 `POST`、`PUT` 等），返回 `IsAuthenticated()`，要求用户必须通过身份验证。

这种设置允许在不同的请求方法下使用不同的权限策略，例如，获取对象时允许任何人查看，但创建或更新对象时要求用户身份验证。这有助于更灵活地定义 API 的权限规则。

## 八.应用自定义权限

这里的API只限管理员可以使用所有功能，和给定权限的人才行，其他人不能访问

```python
class CustomerViewSet(ModelViewSet):
    queryset = Customer.objects.all()
    serializer_class = CustomerSerializer
    permission_classes = [IsAdminUser]


    @action(detail=False,methods=['GET','PUT'],permission_classes =[IsAuthenticated])
    def me(self,request):
        (customer,created) = Customer.objects.get_or_create(user_id = request.user.id)
        if request.method == 'GET':
            serializer = CustomerSerializer(customer)
            return Response(serializer.data)
        elif request.method == 'PUT':
            serializer = CustomerSerializer(customer, data=request.data)
            serializer.is_valid(raise_exception=True)
            serializer.save()
            return Response(serializer.data)

```



另外一种创建permissions.py文件自定义权限

```python
from rest_framework import permissions


class IsAdminOrReadOnly(permissions.BasePermission):
    def has_permission(self, request, view):
        if request.method in permissions.SAFE_METHODS:
            return True
        return bool(request.user and request.user.is_staff)
            
```

在视图函数中去调用

```python
class CollectionViewSet(ModelViewSet):
    queryset = Collection.objects.annotate(
        products_count=Count('products')).all()
    serializer_class = CollectionSerializer
    permission_classes = [IsAdminOrReadOnly] #调用自定义权限
```

## 九.模型权限

在http://127.0.0.1:8000/admin/中有权限group 可以分给某一个用户,

那个用户就有相关权限去操作API

如果在views.py中使用了DjangoModelPermissions情况就变的不一样了,需要当前用户有相关权限才可以有相关行为权限,具体看视频

```python
class CustomerViewSet(ModelViewSet):
    queryset = Customer.objects.all()
    serializer_class = CustomerSerializer
    permission_classes = [DjangoModelPermissions] #使用了DjangoModelPermissions
```

## 十.自定义模型权限

**先在models.py中去创建permission**

```python
class Customer(models.Model):
    .......
    class Meta:
        ordering = ['user__first_name', 'user__last_name']
        permissions = [
            ('view_history','可以查看历史')
        ]
```

**再到permissions.py文件中自定义权限**

```python
class ViewCustomerHistoryPermission(permissions.BasePermission):
    def has_permission(self, request, view):
        return request.user.has_perm('store.view_history')
```

这是一个自定义的 Django 权限类 (`ViewCustomerHistoryPermission`)，它继承自 `permissions.BasePermission`。该权限用于控制用户是否有查看客户历史记录的权限。

具体来说，`has_permission` 方法定义了在请求中是否有权限执行相关操作。在这里，`has_permission` 方法检查用户是否具有 'store.view_history' 的权限，如果是，则返回 `True`，表示有权限，否则返回 `False`，表示没有权限。

这个权限类可以被用于 Django 视图中，以确保只有具有 'store.view_history' 权限的用户可以执行相关的操作。例如：

```python
from rest_framework import generics
from rest_framework.permissions import IsAuthenticated
from .models import YourModel
from .serializers import YourModelSerializer
from .permissions import ViewCustomerHistoryPermission

class YourModelListView(generics.ListAPIView):
    queryset = YourModel.objects.all()
    serializer_class = YourModelSerializer
    permission_classes = [IsAuthenticated, ViewCustomerHistoryPermission]
```

上面的代码中，`YourModelListView` 视图要求用户既必须是认证的 (`IsAuthenticated`)，又必须具有 'store.view_history' 权限 (`ViewCustomerHistoryPermission`) 才能访问。

**再去views.py中去调用ViewCustomerHistoryPermission**

```python
class CustomerViewSet(ModelViewSet):
    queryset = Customer.objects.all()
    serializer_class = CustomerSerializer
    permission_classes = [IsAdminUser]
    
    @action(detail=True,permission_classes = [ViewCustomerHistoryPermission])
    def history(self,request,pk):
        return Response('ok')

```

最后到http://127.0.0.1:8000/admin/core/user/给特定用户赋予该权限



# 设计和构建订单API

### 一.GET 查询订单

在建立Orders API时我们需要通过用户去查看查看我们的api,而不是通过域名ID去查看订单 (**管理员可以查看所有订单，用户只能查看自己的订单**)

1.先从GET开始，以model为基础创建序列化器，然后设置视图函数，添URL(**把最基本的创建好**)

2.需要我们在GET请求中去设置权限,

### 二.POST 创建订单

我们需要把cart_id发送到服务器，来创建订单

在订单视图函数中，由于我们需要创建订单，就需要重写序列化器，如果是'GET'怎么样，如果是‘POST’怎么样

我们需要一个新的序列化器来发送cart_id,然后需要到里面写save()方法来保存这个订单到数据库

### 三.创建订单项

主要思路，通过购物车中的购物车项，把它们传递给订单项,然后删除购物车

需要我们去创建订单序列化中的save()方法中传递购物车项给订单项

首先获得筛选出购物车项整体，再通过列表表达式传递每一个订单项对象,给订单项

把订单项通过这个语法传递给数据库

```python
OrderItem.objects.bulk_create(order_items) 
```

然后删除购物车再save()方法中

```python
Cart.objects.filter(pk = self.validated_data['cart_id']).delete() 
```

### 四.重写视图函数的creat()方法，获取创建订单

```python
class OrderViewSet(ModelViewSet):
    permission_classes = [IsAuthenticated]
    
    def create(self, request, *args, **kwargs):
        serializer = CreateOrderSerializer(
            data=request.data,
            context = {'user_id': self.request.user.id})
        serializer.is_valid(raise_exception=True)
        order = serializer.save()
        serializer = OrderSerializer(order)
        return Response(serializer.data)
    
    def get_serializer_class(self):
        if self.request.method == 'POST':
            return CreateOrderSerializer
        return OrderSerializer
    
    
    def get_queryset(self):
        if self.request.user.is_staff:
            return Order.objects.all()
        
        customer_id =Customer.objects.only('id').get(user_id=self.request.user.id)
        return Order.objects.filter(customer_id=customer_id)
        
```

关于 `create` 方法，你正确地使用了 `CreateOrderSerializer` 来处理创建订单的请求。在 `create` 方法中，你使用了 `serializer.save()` 来保存订单，并将其序列化后返回给客户端。这样客户端在创建订单时，会得到包含订单信息的响应。

### 五.验证购物车

第一种情况 ：需要验证购物车是否存在，需要去创建订单序列化器中去自定义方法

第二种情况 ： 我们创建一个空购物车去创建订单，得到一个空订单，去没有意义,需要去创建订单序列化器中去自定义方法

```python
class CreateOrderSerializer(serializers.Serializer):
    cart_id = serializers.UUIDField()
    
    def validate_cart_id(self, cart_id):
        if not Cart.objects.filter(pk = cart_id).exists():
            raise serializers.ValidationError('购物车ID无效')
        if CartItem.objects.filter(cart_id=cart_id).count() ==0:
            raise serializers.ValidationError('购物车是空的')
        return cart_id
    
```

### 六.对权限进行优化

我希望只有管理员才可以删除，更新订单,用户只能更新自己的订单

```python
class OrderViewSet(ModelViewSet):
    http_method_names = ['get','patch','delete','head','options']
    
    def get_permissions(self):
        if self.request.method in ['PATCH','DELETE']:
            return [IsAdminUser()]
        return [IsAuthenticated()]
```

首先，`http_method_names` 属性是一个列表，用于指定视图集支持的 HTTP 方法。在你的例子中，`OrderViewSet` 仅支持 GET、PATCH、DELETE、HEAD、OPTIONS 这几种 HTTP 方法。其他未在列表中的方法，比如 POST，将不被允许。

然后，`get_permissions` 方法用于确定在执行不同 HTTP 方法时应该应用的权限类（Permission classes）。在你的代码中，它被重写以动态返回不同的权限类列表。

- 如果请求方法是 PATCH 或 DELETE，即修改或删除订单的请求，`get_permissions` 返回了包含 `IsAdminUser` 权限类的列表。这表示只有管理员用户才能执行这些敏感操作。
- 对于其他请求方法，比如 GET，`get_permissions` 返回了包含 `IsAuthenticated` 权限类的列表。这表示对于这些请求，用户需要经过身份验证才能访问相关资源。

这样的设计是为了根据请求的性质动态地应用不同的权限。对于普通的查询和查看订单信息的请求，用户只需经过身份验证即可，而修改或删除订单等敏感操作则需要管理员权限。

### 七.更新订单

订单中我们需要修改的只有支付方式，所以重新写一个序列化器来出来更新

## 八.信号

使用signal来分离我们的应用程序，防止它们踩到对方的脚趾头

在Django中，信号（Signals）是一种机制，允许发送者（sender）和接收者（receiver）之间进行解耦合的通信。当某个特定的事件发生时，信号被发送，然后与该信号相关联的所有接收者将执行其预定义的操作。信号的使用有助于在应用程序的不同部分之间实现松耦合，提高代码的灵活性和可维护性。

```python
#signals.py
from django.conf import settings
from django.db.models.signals import post_save
from django.dispatch import receiver
from .models import Customer


@receiver(post_save, sender = settings.AUTH_USER_MODEL)
def create_customer_for_new_user(sender, **kwargs): 
    if kwargs['created']:
        Customer.objects.create(user = kwargs['instance'])
        
#apps.py
from django.apps import AppConfig


class StoreConfig(AppConfig):
    default_auto_field = 'django.db.models.BigAutoField'
    name = 'store'

    def ready(self) -> None:
        import store.signals
```

这段代码是使用 Django 的信号（Signal）机制，在用户模型 (`settings.AUTH_USER_MODEL`) 的保存事件 (`post_save`) 中创建一个关联的顾客模型 (`Customer`)。下面我来逐步解释：

1. `@receiver(post_save, sender=settings.AUTH_USER_MODEL)`：这是一个装饰器，它将下面的函数 (`create_customer_for_new_user`) 注册为 `post_save` 信号的接收者。具体来说，这个接收者会在用户模型 (`settings.AUTH_USER_MODEL`) 的实例保存后被触发。
2. `def create_customer_for_new_user(sender, **kwargs):`：这是被装饰器装饰的函数，用于处理 `post_save` 信号。`sender` 是发送信号的模型类，而 `**kwargs` 是保存信号时传递的其他参数。在这个例子中，我们关注是否是新创建的实例，也就是 `kwargs['created']`。
3. `if kwargs['created']:`：这是一个条件语句，检查是否是新创建的用户。如果是新创建的用户，就执行下面的代码块。
4. `Customer.objects.create(user=kwargs['instance'])`：在这个代码块中，它使用 `Customer` 模型的 `create` 方法创建了一个关联的顾客对象。`kwargs['instance']` 是触发信号的用户模型实例，通过这个实例创建了对应的顾客。

总结一下，这段代码的作用是在保存用户模型实例时，检查是否是新创建的用户，如果是则创建一个关联的顾客模型实例。通常，这种做法用于确保每个用户都有一个对应的顾客记录，保持用户和顾客模型之间的一对一关系。这对于扩展用户模型以及与用户相关的信息是很有用的。

至于 `apps.py` 中的代码，`ready` 方法用于在应用准备就绪时执行一些初始化操作。在这个例子中，它导入了 `store.signals` 模块，触发了信号的注册。这是 Django 1.7 之后的应用配置方式，确保信号的注册在应用准备就绪时执行。

## 九.自定义信号

在 Django 中，你可以通过使用 `django.dispatch.Signal` 类来定义自己的信号。自定义信号允许你在你的应用中创建自己的触发和响应机制，类似于 Django 内置的信号机制。以下是创建和使用自定义信号的简单步骤：

1. **导入 Signal 类：**

   在你的应用中，首先需要导入 `Signal` 类。通常，你可以在你的 `signals.py` 文件中进行这个操作。

   ```python
   from django.dispatch import Signal
   ```

2. **创建信号对象：**

   创建一个 `Signal` 对象，通常在模块级别进行。

   ```python
   my_signal = Signal()
   ```

3. **定义信号处理函数：**

   创建一个处理信号的函数，这个函数会在信号被触发时执行。

   ```python
   def my_signal_handler(sender, **kwargs):
       print("My custom signal was triggered!")
   ```

4. **连接信号和处理函数：**

   使用 `connect` 方法将信号和处理函数连接起来。这通常在应用的 `apps.py` 文件的 `ready` 方法中完成。

   ```python
   from django.apps import AppConfig

   class MyAppConfig(AppConfig):
       default_auto_field = 'django.db.models.BigAutoField'
       name = 'myapp'

       def ready(self) -> None:
           import myapp.signals
   ```

   在 `myapp/signals.py` 文件中：

   ```python
   from django.dispatch import Signal
   from myapp.models import MyModel

   my_signal = Signal()

   def my_signal_handler(sender, **kwargs):
       print("My custom signal was triggered!")

   my_signal.connect(my_signal_handler, sender=MyModel)
   ```

   在上述代码中，`my_signal.connect` 将 `my_signal_handler` 函数与信号 `my_signal` 关联起来，表示当 `MyModel` 模型的实例保存时，该处理函数将被执行。

5. **触发信号：**

   在你的代码中，当你想要触发这个信号时，可以使用 `send` 方法。

   ```python
   my_signal.send(sender=my_instance)
   ```

   其中 `my_instance` 是触发信号的对象。

这就是一个简单的自定义信号的示例。通过这种方式，你可以定义自己的事件和响应机制，让不同部分的代码更加灵活、解耦合。希望这能帮助你理解如何在 Django 中定义和使用自定义信号。如果有其他问题，随时问我！







# 上传文件

## 一.管理媒体文件

在Django项目中管理媒体文件涉及到处理用户上传的文件，比如图片、视频和其他媒体资源的存储、上传和提供服务。Django提供了`django.core.files`模块以及`MEDIA_ROOT`和`MEDIA_URL`设置来帮助管理媒体文件。

以下是在Django项目中管理媒体文件的逐步指南：

1. **配置媒体设置：**

   在Django的设置文件中，确保已定义了`MEDIA_ROOT`和`MEDIA_URL`。这些设置决定了上传的媒体文件存储的位置和访问的URL。

   ```python
   # settings.py

   MEDIA_ROOT = BASE_DIR / "media"
   MEDIA_URL = "/media/"
   ```

   在这个例子中，`MEDIA_ROOT`指定了媒体文件的存储路径，而`MEDIA_URL`则指定了这些媒体文件在浏览器中的访问路径。

2. **配置URL路由：**

   在Django项目的主urls.py文件中，确保你配置了媒体文件的URL路由。这样Django服务器就能够为这些媒体文件提供服务。

   ```python
   # urls.py

   from django.conf import settings
   from django.conf.urls.static import static

   urlpatterns = [
       # ... 其他URL配置
   ]

   # 添加以下配置用于提供媒体文件服务
   if settings.DEBUG:
       urlpatterns += static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)
   ```

   这个配置只在开发环境中使用，生产环境中通常由Web服务器（比如Nginx或Apache）来处理媒体文件的服务。

3. **在模型中处理媒体文件：**

   如果你的模型需要处理媒体文件，你可以使用`FileField`或`ImageField`字段。确保在模型中定义了适当的字段，以及上传到媒体文件夹的子文件夹。

   ```python
   # models.py

   from django.db import models

   class MyModel(models.Model):
       title = models.CharField(max_length=100)
       media_file = models.FileField(upload_to='my_media_files/')
   ```

   在上述例子中，`media_file`字段使用`FileField`，并通过`upload_to`参数指定了上传的子文件夹。

4. **上传媒体文件：**

   在你的视图或表单中，确保你能够处理用户上传的媒体文件，并将它们保存到指定的位置。

   ```python
   # views.py
   
   from django.shortcuts import render
   from .models import MyModel
   
   def upload_file(request):
       if request.method == 'POST':
           new_file = MyModel(media_file=request.FILES['file'])
           new_file.save()
       return render(request, 'upload_success.html')
   ```

   上述代码片段演示了一个简单的视图，用于处理用户上传的文件并将其保存到数据库中。

## 二.到产品中添加照片

```python

class ProductImage(models.Model):
    product = models.ForeignKey(Product,on_delete=models.CASCADE,related_name='images')
    image = models.ImageField(upload_to='store/images')
```

upload_to= 属性指定当前照片储存的地址 ,它依赖于MEDIA_ROOT路径，把这个照片储存在该根路径的子路径中



下载第三方包

```python
 pipenv install pillow
```

`Pillow` 允许你在 Python 中进行各种图像处理操作，如打开、编辑、保存图像文件，以及进行基本的图像处理操作，比如调整大小、裁剪、旋转等。

在Django中，`Pillow` 通常用于处理`ImageField`中的图片上传和显示。当你使用Django的`ImageField`字段存储图片时，`Pillow`将帮助你处理这些图片的各种操作。这包括生成缩略图、调整图片大小、处理图像格式等。安装`Pillow`后，Django会默认使用它作为图像处理库。

## 三.建立上传图像API

正常的创建序列化器，视图函数，url

我们想在(http://127.0.0.1:8000/store/products/1/images/)这个里面去添加该产品的照片,但是不去指定product_id，

让Django自动去指定,所以需要到序列化器中去重写creat方法

```python
#序列化器
class ProductImageSerializer(serializers.ModelSerializer):
    
    def create(self, validated_data):
        product_id = self.context['product_id']
        return ProductImage.objects.create(product_id = product_id, **validated_data)
    
    
    class Meta:
        model = ProductImage
        fields = ['id','image']
#视图函数
class ProductImageViewSet(ModelViewSet):
    serializer_class = ProductImageSerializer
    
    def get_serializer_context(self):
        return {'product_id' : self.kwargs['product_pk']}
    
    def get_queryset(self):
        return ProductImage.objects.filter(product_id = self.kwargs['product_pk'])
#url
products_router = routers.NestedDefaultRouter(
    router, 'products', lookup='product')
products_router.register('reviews', views.ReviewViewSet,basename='product-reviews')
products_router.register('images',views.ProductImageViewSet,basename='product-images')#嵌套在products后面
```

## 四.返回产品列表时，归还它们的图片

 去产品序列化器中添加一个字段,导入该字段的序列化器

由于查询过多，需要优化，去产品视图函数程序集中加 prefetch_related('images')

## 五.验证上传的文件

创建验证文件validators.py

```python
from django.core.exceptions import ValidationError

def validate_file_size(file):
    max_size_kb = 50
    
    if file.size > max_size_kb * 1024 :
        raise ValidationError('文件不能高于50kb')
```



去models.py中去调用

```python
class ProductImage(models.Model):
    product = models.ForeignKey(Product,on_delete=models.CASCADE,related_name='images')
    image = models.ImageField(
        upload_to='store/images',
        validators=[validate_file_size])
```

## 六.设置后台管理页面加image











# 发送电子邮件

# 运行后台任务

# 自动测试

# 性能测试

# 缓存

# 生产准备

# 部署



