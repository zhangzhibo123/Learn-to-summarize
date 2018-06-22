### 返回查询集的方法称为过滤器

  all()  返回所有数据

  filter()  返回符合条件的数据

  exclude()  过滤掉符合条件的数据

  order_by()  排序

  values()  一条数据就是一个字典，返回一个列表



### 返回单个数据

get()：返回一个满足条件的对象

​     如果没有找到符合条件的对象，会引发 模型类.DoesNotExist异常

​     如果找到多个，会引发  模型类.MultiObjectsReturned 异常

first()：返回查询集中的第一个对象

last()：返回查询集中的最后一个对象

count()：返回当前查询集中的对象个数

exists()：判断查询集中是否有数据，如果有数据返回True没有反之

### 限制查询集

studentList = Student.objects.all()[0:5]  

### 字段查询

contains：是否包含，大小写敏感，filter(sname__contains='赵')

startswith,endswith：以values开头或结尾，大小写敏感

以上四个在运算符前加上 i(ignore)就不区分大小写了 iexact...

### URL路由配置

导入包含

  fromdjango.conf.urls import include,url

```
  urlpatterns = [ 
  				url(r'^xxx/',include('App.urls')),
  				url(r'^add_student', views.add_student,name='add'),
  				]
```

url匹配正则注意事项:

  正则匹配时从上到下进行遍历，匹配到就不会继续向后查找了

  匹配的正则前方不需要加反斜线

  正则前需要加 （r）表示字符串不转义 

获取url路径上的参数:

- 如果需要从url中获取一个值,需要对正则加小括号

  匹配年月日:url(r'^news/(\d{4})/(\d)+/(\d+)$',views.getNews)


### HttpRequest对象

服务器接收http请求之后,会根据报文创建HttpRequest对象

#### 属性:

path:请求的完整路径(不包含域名和端口)

method 表示请求的方式,常用的有get,post

encoding:表示游览器提交的编码方式,一般为utf_8

GET 类似字典的对象,包含了get请求的所有参数

POST 类似字典的对象,包含了post请求的所有参数

FILES 类似字典的对象,包含了所有上传的文件

COOKIES 字典,包含所有cookie

SESSION 类似字典的对象,表示当前会话

#### 方法:

is_ajax(): 如果是通过XMLHttpRequest发起的,返回True

#### QueryDict对象

requsest对象中的get,post都属于QueryDict对象

方法: get()  通过键获取值,只能获取一个值.   

 www.zhangzhib.top/hello?sname=小王&sage=20     request.GET.get(sname)

getlist() 将键的值以列表的形式返回

 www.zhangzhib.top/hello?sname=小王&sname=小明&sage=20 



#### Response:

HttpResponse由程序猿自己创建

  1.不使用模板，直接返回数据HttpResponse()

```
from django.http import HttpResponse
def index(request):
    return HttpResponse('hello,world!!!')
```

  2.调用模板，进行渲染

  	2.1先load模板，再渲染

  	2.2直接使用render一步到位

render(request,template_name[,context])

​	request   请求体对象

​	template_name  模板路径

​	context  字典参数，用来填坑

```
from django.shortcuts import render
def get2(request):
    return render(request, 'myApp/register.html')
```



#### 404

配置修改 DEBUG = True 永远不会调用404页面,应该把True改为False 

```
ALLOWED_HOSTS = ["*"]
```

在templates目录下直接创建名为404.html的文件

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>404页面</title>
</head>
<body>
    <h1>页面丢失</h1>
    <h2>{{request_path}}</h2>
</body>
</html>
```

#### cookie和session

```
def cookietest(request):
    res = HttpResponse()
    cookie = request.COOKIES 获取cookie值sunck:good
    res.write("<h1>"+cookie["sunck"]+"</h1>")
    # cookie = res.set_cookie("sunck","good")   # 返回response-cookie:sunck,good
    return res
```

#### 文件上传

文件数据存储在request.FILES属性中

```
form表单上传文件需要添加enctype='multipart/form-data'
文件上传必须使用POST请求方式
存储
	在static文件夹下创建uploadefiles用与存储接收上传的文件
	在settings中配置，MEDIA_ROOT=os.path.join(BASE_DIR,r'static/uploadefiles')
在开发中通常是存储的时候，我们要存储到关联用户的表中
```

```
<form method='post' action='xxx' enctype='multipart/form-data'>
	{% csrf_token %}
	<input type='file' name='icon'>
	<input type='submit'  value='上传'>
<form>
def savefIcon(request):
	if request.method == 'POST'
		f = request.FILES['icon']
		filePath = os.path.join(settings.MEDIA_ROOT,f.name)
		with open(filePath,'wb) as fp:
			for part in f.chunks():
				fp.write(part)
```

