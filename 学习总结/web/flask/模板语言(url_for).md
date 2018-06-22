flask

路由生成：{{  url_for("模块名.视图名") }}

静态文件加载 {{ url_for('static', filename="静态文件路径") }} 

templates 只查询内部  static也只查询内部

```
redirect('/home/login')
redirect(url_for("home.home_login"))

<a class="curlink" href="{{ url_for('home.register') }}"><span class="glyphicon glyphicon-plus"></span>&nbsp;注册</a>

<script src="{{ url_for('static',  filename='base/js/jquery.min.js') }}"></script>
<script src="{{ url_for('static',  filename='base/js/bootstrap.min.js') }}"></script>
```

django

{% url 'name' %}  路由生成

```
urlpatterns = [
    url(r'^add_student', views.add_student,name='add'),
]

def index2(request):
    return redirect('add')
    
<form action="{% url 'add' %}" method="get">
    {% csrf_token %}
    <p>学生姓名: <input type="text" name="stu_name" /></p>
    <p>学生性别:男请输入True,女为false <input type="text" name="stu_sex" /></p>
    <p>学生年龄: <input type="text" name="stu_age" /></p>
    <p>学生地址: <input type="text" name="stu_address" /></p>
    <p>学生班级: <input type="text" name="cls_id" /></p>
    <input type="submit" value="提交"/>
</form>
```

静态文件加载

templates static 先查询外部再查询内部

```
模板中的声明
{% load static%} 或 {% load staticfiles %}

在引用资源的时候使用
{% static 'xxx' %}   xxx 就是相对于static的一个位置
```

```
{% load staticfiles %}
<link rel="stylesheet" href="{% static 'base/css/bootstrap.min.css' %}">
<script src="{% static 'base/js/jquery.min.js' %}"></script>
<script src="{%  static 'base/js/bootstrap.min.js' %}"></script>
<img src="{% static 'base/images/logo.png' %}" style="height:30px;">
```

