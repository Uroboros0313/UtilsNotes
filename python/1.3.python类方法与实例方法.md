# 类的方法
## 类方法(@classmethod)


## 静态方法(@staticmethod)
装饰器`@staticmethod`修饰静态方法，入参不能存在`cls`和`self`。

静态方法既不依赖实例对象也不依赖于类，所以可以通过`类对象`和`实例对象`进行调用，需要注意的是在静态方法中无法使用实例属性和方法。

- 作用:功能与类较为独立的方法可以使用静态方法
```python
class BaseCls:
    def __init__(self):
        pass

    @staticmethod
    def add(num_1, num_2):
        return num_1 + num_2
case = BaseCls
print(case.add(1,1)) # 2
print(BaseCls.add(1,1)) # 2
```
## 抽象类与抽象方法(@abstractmethod)

- ABC:抽象基类             
- abstractmethod:抽象方法         

1. 抽象基类不能实例化
2. 继承抽象基类的子类需要重写基类中的所有@abstracmethod装饰的抽象方法，否则不能实例化
3. 抽象基类的作用是定义统一的接口，例如一个支付场景下利用多个app进行支付，则可以定义一个抽象基类，子类重写所有基类的抽象方法

```python
from abc import abstractmethod,ABC

class BaseClass(ABC):
    @abstractmethod
    def basefunc(self):
        print("basefunc implement")

class InstanceClass(BaseClass):
    def basefunc(self):
        print("instance implement")

class BadInstanceClass(BaseClass):
    def badbasefunc(self):
        print("instance bad implement")

instance = InstanceClass() # 可以实例化
bad_instance = BadInstanceClass() # 无法实例化

```

## Property(@property)

- **property**:一种用起来像是使用的实例属性一样的特殊属性，对应于某个方法,需要调用方法的方式类似于调用属性时，在一个方法加上@property

- property属性的功能是：property属性内部进行一系列的逻辑计算，最终将计算结果返回。

- property属性有三种访问方式，并分别对应了三个被@property、@方法名.setter、@方法名.deleter修饰的方法

```python
class BaseClass:
    def __init__(self):
        self.baseattr = 1024
        self.frac = 0.5
    @property
    def baseprop(self):
        return self.baseattr * self.frac

    @baseprop.setter
    def baseprop(self, newattr):
        self.baseattr = newattr

    @baseprop.deleter
    def baseprop(self):
        del self.baseattr

base_inst = BaseClass()
print(base_inst.baseprop) # 512.0
base_inst.baseprop = 2048
print(base_inst.baseprop) # 1024.0
del base_inst.baseprop
try:
    print(base_inst.baseprop) # 'BaseClass' object has no attribute 'baseattr'
except AttributeError:
    print('BaseClass object has no attribute baseattr')
```