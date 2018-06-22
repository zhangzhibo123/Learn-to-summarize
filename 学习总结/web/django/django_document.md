### 运行服务器

python manage.py runserver   # 默认监听本机8000端口

更换端口

python manage.py runserver 8080

更换ip

python manage.py runserver 0:8080  # **0** 是 **0.0.0.0** 的简写

### url参数

route 匹配url的准则 , 这些准则不会匹配GET和POST参数或域名

name 为你的 URL 取名能使你在 Django 的任意地方唯一地引用它，尤其是在模板中。这个有用的特性允许你只改一个文件就能全局地修改某个 URL 模式

### models模型迁移

python manage.py makemigrations app

python manage.py sqlmigrate app 0001  # 查看sql语句

1. 数据库表名默认是由应用名(polls)和模型名的小写形式(question和choice)连接而来
2. 主键会被自动创建
3. Django默认会在外键字段'名后追加字符串"_id'

python manage.py check 检查项目中的问题

python manage.py migrate 迁移

