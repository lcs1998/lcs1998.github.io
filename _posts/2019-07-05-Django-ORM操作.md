---
layout:     post
title:      Django ORM操作
subtitle:   Django ORM
date:       2019-07-05
author:     Jacob
header-img: img/post-bg-js-version.jpg
catalog: true
tags:

    - Django
    - ORM
---

# Django ORM操作

> Django中集成了ORM框架，可以直接使用orm对数据库进行增删查改等操作，相对sql语句来说，orm语句更加简洁易懂，方便开发者进行开发

## 1.增加数据

数据库中的表有一对一关系，一对多关系和多对多关系，对于这几种关系我们有不同的方法去实现增加数据操作。

### 一对一关系

对于一对一关系比较简单，我们假设有一张表student，里面有student_id(学号)和name(两个属性)，代码如下：

```bash
# 使用如下方法时，需要先引入数据库
from .models import Student

# 第一种方法
Student.obects.create(student_id='123456', name='lcs')

# 第二种方法
stu = Student(student_id='123456', name='lcs')
stu.save()
```

### 一对多关系

我们在student表中添加一个属性**counselor**，表示他的辅导员是谁，辅导员对于学生是**一对多**的关系

```bash
# 使用如下方法时，需要先引入数据库
from .models import Student

# 第一种方法
Student.obects.create(student_id='123456', name='lcs', counselor_id=2)

# 第二种方法
stu = Student(student_id='123456', name='lcs', counselor_id=2)
stu.save()
```

### 多对多关系

比如说我们在表中添加一个字段teacher，他表示这个学生的老师。显然，一个学生对应多个老师，一个老师对应多个学生，所以这个是多对多关系。

我们新建一个Teacher表，表示这个学校所有的老师

```bash
# 同样，我们需要先引入这连个表
from .models import Teacher, Student

# 获得学生和老师
stu = Student.objects.get(name='lcs')
teacher_1 = Teacher.objects.get(name='hch')
teacher_2 = Teacher.objects.get(name='hyh')

# 将两个teacher对象添加到这个学生teacher字段中
stu.teacher.add(teacher_1, teacher_2)
```

## 2.删减数据

删除操作比较简单，但是要注意级联删除操作的存在，否则会造成不可预估的后果

```bash
# 引入数据表
from .models import student

student.objects.filter(student_id='1213131').delete()
```

## 3.查找数据

关于查找数据有比较多的方法，如果只看sql语句的话，有大于，小于，大于等于，小于等于，in操作等，下面介绍一下比较基本的操作

```bash
# 引入数据库
from .models import student

# 查找所有数据
student.objects.all()

# 按条件筛选数据，没有返回为空
student.objects.filter(name='lcs')
# 返回符合条件的第一条数据
student.objects.filter(name='lcs').first()
# 返回符合条件的最后一条数据
student.objects.filter(name='lcs').last()

# 按条件返回数据，没有符合条件的数据则报错
student.objects.get(name='lcs')

# 对所有的名字去重后返回
student.objects.values('name').distinct()
```

下面介绍sql语句中in，>，>=，<，<=等操作

```bash
# 引入数据库
from .models import student

# 获取个数
student.objects.filter(name='seven').count()

# 大于，小于
student.objects.filter(age__gt=21)              	# 获取age大于21的值
student.objects.filter(age__gte=21)              	# 获取age大于等于21的值
student.objects.filter(age__lt=21)             		# 获取age小于21的值
student.objects.filter(age__lte=21)             	# 获取age小于21的值
student.objects.filter(age__lt=20, age__gt=18)   	# 获取age大于18 且 小于21的值

# in操作
student.objects.filter(age__in=[18,19,20])   			# 获取id等于18,19,20的数据
student.objects.exclude(age__in=[18,19,20])  			# not in

# isnull操作
student.filter(teacher__isnull=True)

# contains操作
student.objects.filter(name__contains="ven")
student.objects.filter(name__icontains="ven") 
student.objects.exclude(name__icontains="ven")		# icontains大小写不敏感

# range操作
student.objects.filter(age__range=[18, 21])   		# 年龄在18和21之间的学生

# 其他类似操作
# startswith，istartswith, endswith, iendswith,

# order by
student.objects.filter(age=21).order_by('student_id')    # asc
student.objects.filter(age=21).order_by('-student_id')   # desc

# group by
student.objects.filter(age=20).values('name').annotate(name=Count('name'))

# limit 、offset
student.objects.all()[10:20]
```

## 4.更新数据

```bash
# 引入数据库
from .models import student

# 第一种方法
obj = student.objects.get(student_id='121212')
obj.age = '20'
obj.save()

# 第二种方法
student.objects.filter(student_id='121212').update(age=20)
```

