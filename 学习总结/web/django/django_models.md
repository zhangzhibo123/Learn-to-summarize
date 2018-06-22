### 模型参数

AutoField

CharField

TextField 大文本字段

IntegerField

DecimalField(max_digits=None, decimal_places=None)

max_digits : 位数总数 decimal_places:小数点后的数字总数

FloatField

BooleanField

NullBooleanField

DateField([auto_now=True, auto_now_add])日期

(auto_now 每次保存对象时,自动设置该字段为当前时间,用于最后一次修改)lasttime

(auto_now_add 当对象第一次被创建时自动设置当前时间,用于当前的时间戳)createtime

DateTimeField  日期时间

TimeField  时间

FileField 上传文件的字段

ImageField 图片字段

关系:

ForeignKey  一对多

ManyTOManyField  多对多

OneToOneField  一对一

### 元选项

```
class Meta:
	db_table = 'student'
	ordering = ['-create_date','username']
	前面没有“-”的字段表示正序
	"-" 前面带有可选的“-”前缀表示倒序
	"?" 表示随机排序

```

自定义模型管理器

```
stuObj = models.Manager()
```



### 创建对象方案

1. 在模型类中增加类方法去创建对象

   ```
   @classmethod
   def create(cls, name, age):
   ```

2. 在自定义的管理器中添加方法来创建对象


### 字段查询

对sql中where的实现，作为方法filter(),exclude(),get()的参数

语法:属性名称__比较运算符=值

#### 比较运算符

contains 是否包含, 大小写敏感    filter(sname__contains='赵')

```
#描述中带有'薛延美'这三个字的数据时属于哪个班级的
grade = Grades.objects.filter(students__scontend__contains='薛延美')

# 班级等于多少的学生信息
Grades.students_set.all()
```

startswith,endswith  :在运算符前加上 i(ignore)就不区分大小写了

in 是否包含在范围内  filter(pk__in=[2,4,6,8])

gt,gte,lt,lte：大于，大于等于，小于小于等于filter(sage__gt=30)

#### 聚合函数

使用aggregate()函数返回聚合函数的值

Avg：平均值

Count：数量

Max：最大

Min：最小

Sum：求和

Student.objects().aggregate(Max('sage'))

### 自定义模型管理器

```
class Student(models.Model)：
		stuManager = models.Manager()
```

自定义模型管理器作用:

可以向管理器中添加额外的方法

修改管理器返回的原始查询集

提供创建对象的方式

### 模型的对应关系

1 : 1 使用models.OneToOneField()进行关联

1 :  N

  使用models.ForeignKey关联

  删除时同 1   ： 1

  获取对应元素  grade.student_set  

### F, Q对象

F对象:允许Django在未实际链接数据的情况下具有对数据库字段的值的引用。通常情况下我们在更新数据时需要先从数据库里将原数据取出后方在内存里，然后编辑某些属性，最后提交。

可以使用模型的A属性与B属性进行比较

支持F对象的算术运算, 及时间加减

```
Grades.objects.filter(ggirlnum__gt=F('gboynum')+20)
```

Q对象:Q对象(django.db.models.Q)可以对关键字参数进行封装，从而更好地应用多个查询。可以组合使用 &（and）,|（or），~（not）操作符，当一个操作符是用于两个Q的对象,它产生一个新的Q对象

```
studentsList = Students.stuObj2.filter(~Q(pk__lte=3))
 Q(create_time=date(2016, 10, 2)) | Q(create_time=date(2016, 10, 6))
```





​


