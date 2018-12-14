# Python

## Python的面向对象
其实比较简单，写了半年的`pyhton`，今天重温了一下，感觉收获良多。

### 内置属性类
- __dict__ : 类的属性（包含一个字典，由类的数据属性组成）
- __doc__ :类的文档字符串
- __name__: 类名
- __module__: 类定义所在的模块（类的全名是'__main__.className'，如果类位于一个导入模块mymod中，那么className.__module__ 等于 mymod）
- __bases__ : 类的所有父类构成元素（包含了一个由所有父类组成的元组）

```python
#!/usr/bin/python
# -*- coding: UTF-8 -*-

class Employee:
    """ 所有员工的基类 """
    empCount = 0

    def __init__(self, name, salary):
        self.name = name
        self.salary = salary
        Employee.empCount += 1

    def displayCount(self):
        print "Total Employee %d" % Employee.empCount

    def displayEmployee(self):
        print "Name : ", self.name,  ", Salary: ", self.salary

    print "Employee.__doc__:", Employee.__doc__
    print "Employee.__name__:", Employee.__name__
    print "Employee.__module__:", Employee.__module__
    print "Employee.__bases__:", Employee.__bases__
    print "Employee.__dict__:", Employee.__dict__

# ------------------ 结 果 ------------------
Employee.__doc__: 所有员工的基类
Employee.__name__: Employee
Employee.__module__: __main__
Employee.__bases__: ()
Employee.__dict__: {'__module__': '__main__', 'displayCount': <function displayCount at 0x10a939c80>, 'empCount': 0, 'displayEmployee': <function displayEmployee at 0x10a93caa0>, '__doc__': '\xe6\x89\x80\xe6\x9c\x89\xe5\x91\x98\xe5\xb7\xa5\xe7\x9a\x84\xe5\x9f\xba\xe7\xb1\xbb', '__init__': <function __init__ at 0x10a939578>}

```
[这个例子来自菜鸟教程](http://www.runoob.com/python/python-object.html)

### 类的继承

```python
#!/usr/bin/python
# -*- coding: UTF-8 -*-

class Parent:        # 定义父类
    parentAttr = 100
    def __init__(self):
        print "调用父类构造函数"

    def parentMethod(self):
        print '调用父类方法'

    def setAttr(self, attr):
        Parent.parentAttr = attr

    def getAttr(self):
        print "父类属性 :", Parent.parentAttr

class Child(Parent): # 定义子类
   def __init__(self):
      print "调用子类构造方法"

   def childMethod(self):
      print '调用子类方法'

c = Child()          # 实例化子类
c.childMethod()      # 调用子类的方法
c.parentMethod()     # 调用父类方法
c.setAttr(200)       # 再次调用父类的方法 - 设置属性值
c.getAttr()          # 再次调用父类的方法 - 获取属性值

# ------------------ 结 果 ------------------
调用子类构造方法
调用子类方法
调用父类方法
父类属性 : 200
```
这个在(flask)[]中的 RESTful API 的实现用到
```python
from flask import request
from flask_restful import Resource
# 做了restful的继承，继承相关的方法，这块一用到之后一会的方法重写
class APIClassXXX(Resource):
    def get(self):
        user = request.args.get('user', '')
        ...

```
了解*[flask-restful](https://flask-restful.readthedocs.io/en/0.3.5/quickstart.html)*

了解*[RESTful AP-阮一峰](http://www.ruanyifeng.com/blog/2018/10/restful-api-best-practices.html)*


### 基础重载方法
这个我也还没有用过

| 方法 | 描述 | 简单调用|
|---|---|---|
|`__init__ ( self [,args...] )`|构造函数|简单的调用方法: `obj = className(args)`|
|`__del__( self )`|析构方法, 删除一个对象|简单的调用方法 : `del obj`|
|`__repr__( self )`|转化为供解释器读取的形式|简单的调用方法 : `repr(obj)`|
|`__str__( self )`|用于将值转化为适于人阅读的形式|简单的调用方法 : `str(obj)`|
|`__cmp__ ( self, x )`|对象比较|简单的调用方法 : `cmp(obj, x)`|

[运算法重载](http://www.runoob.com/python/python-object.html)

### 私有属性
python中的*私有属性*用 `__` 两个下划线来开头

- `__foo__`: 定义的是特殊方法，一般是系统定义名字 ，类似 `__init__()` 之类的。

- `_foo`: 以单下划线开头的表示的是 protected 类型的变量，即保护类型只能允许其本身与子类进行访问，不能用于 `from module import *`

- `__foo`: 双下划线的表示的是私有类型(private)的变量, 只能是允许这个类本身进行访问了。

*Python不允许实例化的类访问私有数据，但你可以使用 `object._className__attrName`（ 对象名._类名__私有属性名 ）访问属性*

### 是否需要预加载
在声明class的时候，我们可以使用`@classmethod`,在外部可以免实例化，直接引用。
```python
class example_class():

    # 这里的参数可以只会加载一次
    # 我一般会在这里 redis_db.hscan(), 这样的化在这里只加载一次就好
    init_A = []

    @classmethod
    def temp_args(cls):
        """免事例的函数"""
        print cls.init_A
        print cls.init_A.get('xxx', ')
        ...

# -------------- 使用方法 --------------
example_class.temp_args()
```
我在下面写一个对比
```python
class self_func_demo():
    """
        这个是需要实例话的机器
    """
    def __init__(self):
        """
            只加载一次 
        """
        redis_db = falconRedis.new_redis_client()
        self.user_all = redis_db.hgetall('xxx')

    def get_func(self, key):
        """ 方法xxx """
        user = self.user_all.get(key, '')
        ...
# -------------- 使用方法 --------------
f = self_func_demo()
f.get_func(key)
```