1. 获取关联对象的集合

   对象名.关联的类名小写_set.all()

   ```django
   cate.product_set.all()
   # 相当于
   Product.objects.filter(cid = cate.id)
   ```



### 站点管理Admin

创建管理员用户:python manage.py createsuperuser

汉化:

```
LANGUAGE_CODE = 'zh-hans'

TIME_ZONE = 'Asia/Shanghai'
```

```
#先导入
from .models import Grades,Students
#在注册
admin.site.register(Grades)
```

#### 列表页属性

```
class GradeAdmin(admin.ModelAdmin):
    list_display = ['pk', 'gname', 'gdate', 'ggirlnum', 'gboynum', 'isDelete'] # 显示字段
        list_filter = ['gname'] # 过滤器
        search_fields = ['gname'] # 搜索字段
        list_per_page = 5 #分页
        # ordering
admin.site.register(Grades, GradeAdmin)
```

#### 添加   修改页属性

```
fields = ['ggirlnum', 'gboynum','gdate','gname','isDelete'] #修改属性顺序
fieldsets = [
        ('num', {'fields':['ggirlnum','gboynum']}),
        ('base',{'fields':['gname','gdate','isDelete']})]       
# exclude 不显示的字段
# 分组fleldsets和fields,exclude不能同时使用
```

#### 关联对象

```
# 在创建一个班级时可以直接添加几个学生
class StudentsInfo(admin.TabularInline):  # StackedInline另一种写法
    model = Students
    extra = 2
class GradeAdmin(admin.ModelAdmin):
    inlines = [StudentsInfo]
```

修改bool值及列名称

```
class StudentsAdmin(admin.ModelAdmin):
    # 列表页属性
    def gender(self):
        if self.sgender:
            return '男'
        else:
            return '女'
    # 设置页面列的名称
    gender.short_description = '性别'
    list_display = ['pk', 'sname', gender, 'sage', 'scontend', 'isDelete','sgrade' ] # 显示字段
```

#### #执行动作的位置

```
actions_on_top = False
actions_on_bottom = True
```

#### 用装饰器注册

```
admin.site.register(Students, StudentsAdmin)
@admin.register(Students)
```

