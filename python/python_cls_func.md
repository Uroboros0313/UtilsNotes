# 类

# 魔术方法

## `__new__(cls)`

`__new__`方法通过调用object类的`__new__`方法创建对象，再把对象传递给`__init__`方法(`__new__`在`__init__`前执行)

- 以下情况`__init__`不会被执行
1. 不在`__new__()`调`object`的`__new__`方法不会创建对象
2. 如果不在`__new__`方法return创建的对象
   
```python
class BaseCls:
    def __init__(self):
        print("__init__ runs after __new__")
        
    def __new__(cls, *args, **kwargs):
        print("rewrite __new__ to print INFO")
        return super().__new__(cls,*args,**kwargs)

base_cls = BaseCls()
# rewrite `__new__` to print INFO
# `__init__` runs after `__new__`
```
## `__del__(self)`

实例在内存中被释放时，自动执行。    
Python中大部分情况下关心内存的释放的情况较少，解释器自动执行。

## `__call__(self)`

1. 作用: 让类实例可以像调函数一样调用。
2. `__call__`方法的执行是由**<类实例>**后加括号触发的

```python
class BaseCls:
    def __init__(self):
        pass

    def __call__(self, *args, **kwargs):
        print("call CLS instance as func")

base_cls = BaseCls()
base_cls() # 类实例加括号调用
# call CLS instance as func
```
## `__len__(self)`

`len(cls_instance)`时自动调用:

```python
from collections import defaultdict

class Query2KeyValueType():
    def __init__(self):
        self.q2kv_dict = defaultdict(dict)
    
    def __len__(self):
        print("rewrite `__len__` func")
        value_count = 0
        for kv in self.q2kv_dict.values():
            for v in kv.values():
                value_count += len(v)
        return value_count

q2kv = Query2KeyValueType()
for i in range(3):
    for j in range(4):
        q2kv.q2kv_dict[i][j]=list(range(4))
print(len(q2kv))

# 48
```

## `__repr__(self)/__str__(self)`

- `repr()`是便于开发者理解的方式返回对象的字符串表示形式。
- `str()`以便于用户理解的方式返回对象的字符串表示形式

1. 只有`__repr()__`时,`print()/str()/repr()`及实例化时返回`__repr__()`的返回值
2. 只有`__str__()`时,`print()/str()`返回`__repr__()`的返回值,实例化及`repr()`返回类名及内存地址
3. 同时定义时,实例化返回`__repr__()`的返回值,其余方法返回`__str__()`返回值
```python
class StructPrinter(StructDict):
    def __init__(self,):
        super().__init__()
    
    def __repr__(self,):
        content = ','.join([f'struct(key:{k},value:{v})' for k,v in self.struct_dict.items()])
        return f"StructDict({content})"
    
    def __str__(self,):
        return "StructDict"

udd_2 = StructPrinter()
udd_2.struct_dict = dict([(key, key**2) for key in range(3)])
print(udd_1)
print(udd_2)
print(repr(udd_2))
print(str(udd_2))
udd_2

# <__main__.StructDict object at 0x000001E7DD27AEB8>
# StructDict
# StructDict(struct(key:0,value:0),struct(key:1,value:1),struct(key:2,value:4))
# StructDict
# StructDict(struct(key:0,value:0),struct(key:1,value:1),struct(key:2,value:4))
```

## `__eq__(self, obj)`

调用相等判断时自动执行,判断相等判断另一侧的实例`<obj>`是否等于自身

```python
class BaseCls:
    def __init__(self, value = 1):
        self.value = value
    def __eq__(self,obj):
        print("rewrite `__eq__`, determine how to evaluate if `self == obj`")
        return self.value ** 2 == obj.value ** 2

case_1 = BaseCls(value = 1)
case_2 = BaseCls(value = -1)
print(case_1 == case_2)
# True
```
## `__hash__(self)`    

1. `hash()`方法自动调用
2. `__hash__`计算哈希值
3. 计算哈希值需要使用不可变数据类型(`str`,`int`等,`float`不可以)

```python
class BaseCls:
    def __init__(self, value = 1):
        self.value = value
    def __hash__(self):
        print("rewrite `__hash__`, use cls name to calculate hash value")
        return hash(self.__class__.__name__)

case = BaseCls()
print(hash(case))
# -4023088111989652003
```

## `__getitem__(self,key):`

把类中的属性定义为**序列**，可以使用`__getitem__()`函数输出序列属性中的某个元素，这个方法返回与指定键关联的值。

在类中定义了`__getitem__()`方法，那么它的实例对象(假设为`case`)就可以以`case[key]`形式取值。

当对类的属性进行下标的操作时，首先会被`__getitem__()`拦截，从而执行在`__getitem__()`方法中设定的操作，如赋值，修改内容，删除内容等。

```python
class StructType():
    def __init__(self, value: int = 10):
        self.value = value ** 2

class StructDict():
    def __init__(self,):
        self.struct_dict = dict()
    def __getitem__(self,key):
        return self.struct_dict.get(key, None)

udd = StructDict()
udd.struct_dict = dict([(key, key**2) for key in range(10)])
print(udd[1])
print(udd[9])
# 1
# 81
```

