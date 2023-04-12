# 对象荒原

![[Pasted image 20221108100453.png]]

从函数洞窟走出后，Alice面前出现了一片荒原……

## 面向对象

首先需要声明的是，这里提到的对象不是男女朋友那种关系上的“对象”，当然也不是调侃时说送你一对象的象棋中的“对象”，这里所提到的“对象”是指**面向对象**（Object Oriented）的*软件开发方法，是一种普遍的编程范式*。目前面向对象这个概念已经超越了原本的领域，总体而言，面向对象是一种对现实世界理解和抽象的方法，是计算机编程技术发展到一定阶段后的产物。

读者们或许也经常听到某某语言是面向对象的编程语言，当然Python也是其中之一，但是这不代表着只要使用Python就是面向对象编程了，而是要使用面向对象的编程方法，才能算是面向对象编程。

读者们可能还不能很好理解什么是面向对象，这里我们对以前实现过的功能进行回顾，我们需要定义两个玩家并打印相关信息。

```python 3
Alice = {'name': 'Alice', 'age': 18, 'ID': 4321}
Tom = {'name': 'Tom', 'age': 28, 'ID': 4322}

def info_printer(player):
    print('='*10 + '<Player Info>' + '='*10)
    for k, v in player.items():
        print(k, '--->', v)

info_printer(Alice)

——————————————————————————————
==========<Player Info>========== 
name ---> Alice 
age ---> 18 
ID ---> 4321
```

读者可以回顾我们实现以上功能的方法，在之前的学习内容中，我们可以通过字典（某种数据结构）创建用户信息，可以通过一个输出信息函数，具体来说就是打印字典内容来实现用户信息的输出。以上方法的弊端是创建每个用户时我们都要单独创建一个新的字典，而且仅仅是个字典，同时我们只能输出字典内的内容，我们想要实现用户其他功能只能通过外部函数的方式实现。

那么在这一章中我们要逐渐学习面向对象的方法来实现上述功能，首先我们来看**类**的概念，这是一套与真实世界打交道的编程视角。

### 类

我们直接看一个类的模板，这里我们定义一个“猫”类：

```python 3
class Cat:
    def __init__(self, name, color):
        self.name = name
        self.color = color
    
    def sound(self):
        print('meow ~')
```

从形式上看**类**（Class）的名字叫CAt，里面有两个函数（由def引导），其中__init__称之为*初始化函数*，它包含三个参数，self、name和color，self这个参数是一个定式，代表类实例本身，同时也需要知道初始化函数是一个*固定形式*，它用来描述*属性部分*，要注意init前后各有两个短下划线“\_”，这是Python中的“魔术方法”。

另外一个函数是sound函数，只实现一个功能就是模仿猫叫，这是一个*功能函数*，具体实现什么功能可以读者自己设定。

在读者初始阶段可以通过“照猫画虎”的方式先实现类，然后再去慢慢学习其中的细节。

在构造了一个类之后，我们需要*构造具体的实例*，为什么要构造具体的实例呢？因为类是一个具有共性的大集合，只是一个类别，我们创建了一个“猫”的大类。但是当你需要具体描述某一只猫的时候，就需要具象描述实例，这一步就叫做**对象实例化**。

笔者家里有两只猫，我们现在实例化这两只猫，*实例就是这个类的一个具体指向*：

```python 3
cat_yj = Cat('英俊', 'Dragon-Li')
cat_sr = Cat('松茸', 'Orange')

print(cat_yj.name, cat_yj.color)
cat_yj.sound()

——————————————————————
英俊 Dragon-Li 
meow ~
```

实例化的操作实质上是给类的初始化函数进行传参，读者需要注意实例化的固定套路，括号外是类名，括号内是初始化函数除self外的两个参数，以cat_yj实例为例，这是一个猫类（Cat）中的实例，其中name为'英俊'，color为'Dragon-Li'，注意要按照参数的顺序进行传入。这就完成了一个实例化的过程，实例的名字为cat_yj。

如何调用呢？对于实例中的属性，可以使用“实例名.属性名”的方式，如“cat_yj.name”，对于实例中的功能，可以使用“实例名.函数名()”的方式，如“cat_yj.sound()”，则会实现该函数的对应功能。所谓的面向对象编程，就是面向这些实例编程。

当我们构建了一个猫类的时候，我们发现还有很多类似的猫科动物，比如老虎、狮子等，这些动物都属于猫科动物所以有一些共性，他们之间的区别可能体现在叫声不同等方面，那如何利用猫这个类来定义狮子类呢？

```python 3
class Lion(Cat):
    def __init__(self, name, color):
        super().__init__(name, color)
    
    def sound(self):
        print('roar ~')

simba = Lion('Simba', 'yellow')
print(simba.name, simba.color)
simba.sound()
```

与上述定义不同的是，我们在狮子Lion类后加了个括号，里面有一个Cat，这表示作为猫科动物，狮子类是猫类的一个*子类*，狮子类*继承*了猫类的一些属性。对于名字、颜色这些属性是可以共性描述的，因此初始化函数不需要重写，只需要利用super()方法继承猫类（父类）中的初始化函数即可。

但与此同时，我们没有见过喵喵喵的狮子，所以对于非共性的部分，重新定义了狮子的功能函数（发声函数）。我们对Lion类进行实例化操作，定义了一个simba实例，他的名字叫'Simba'，颜色为'yellow'。我们通过继承实现了类共性的最大化使用。

#### 抽象类

陀思妥耶夫斯基有句名言是我们*要爱具体的人*。人类是一个抽象的概念，而具体的人是人类的一个实例。有些类同样也过于抽象和广泛，比如一些描述过大的类。上述我们定义了猫类、狮子类，但如果我们构建一个动物类，我们是很难找到一些共性的，因此我们很难对这些类进行实例化，找到某一个具体的对应，这样的类就是抽象类。

利用现实世界中抽象的概念，我们可以*定义抽象类*，注意这些类*不能实例化*。假设我们要构建动物类这么一个抽象类，首先要从abc中调用ABC方法和抽象方法abstractmethod，其中abc是Python内置的*抽象基类*，即Abstract Base Class。

```python 3
from abc import ABC, abstractmethod

class Animal(ABC):
    def __init__(self, name):
        self.name = name
        
    @abstractmethod
    def skill(self):
        pass
```

此时Animal类继承了ABC类，Animal就是一个抽象类，是不能被实例化的，此时的共性可能只有一个姓名属性，而每个动物的技能都不相同，因此利用抽象方法对技能函数（功能函数）进行装饰，而功能函数中只有个pass，表示什么都不做，而任意一个属于Animal的类中功能函数必须重写。*抽象类代表的是更高维度的共性*。

紧接着我们就可以构建一些更具体的类来继承动物类（比如具体的Dog类、Bird类等）：

```python 3
class Dog(Animal):
    def __init__(self, name):
        super().__init__(name)
    
    def skill(self):
        print('Good nose')

class Bird(Animal):
    def __init__(self, name):
        super().__init__(name)
    
    def skill(self):
        print('fly, fly, fly')

roy = Dog('roy')
jo= Bird('jo')

roy.skill()
jo.skill()
```

我们在Animal类的基础上构建了Dog类和Bird类，这里每个类继承了Animal的属性，而由于Animal类是抽象类且其中的功能函数需要重写，因此我们对每个类中的功能函数（skill函数）进行了重写。此后，我们实例化了一只名为roy的狗和一只名为jo的鸟。

抽象类主要用于较大型项目的开发和管理。

### 一切都是对象

我们曾经提过，不是只要使用Python就是面向对象编程了，而是要使用面向对象的编程方法，具体来说就是*使用类的方法*进行编程。接下来我们来看Python的内在逻辑，具体来说**Pyhton里的一切都是对象**。

我们在学习变量类型的时候曾经让读者利用type()方法识别变量的类型

```python 3
x = 'hello'
y = 5
def f():
    pass

print(type(x))
print(type(y))
print(type(f))
——————————————————————
<class 'str'> 
<class 'int'> 
<class 'function'>
```

我们对字符串型、整型进行了判断，也对函数进行了判断，但是我们一直没有提到前面的**class**，这时的你或许应该理解这里的class是什么意思了，实际上x就是str类的一个实例化，y是int类的一个实例化，f()就是function类的一个实例化。

前文我们还进行过字符串型和整型的相互转换

```python 3
int('666')
```

这时也许你可以更好的理解这个表达式的意思了。实际上类型转换和实例化的过程是很相似的。

我们可以利用isinstance方法判断前者是不是后者的实例、利用issubclass判断前者是不是后者的子类。

```python 3
print(isinstance(roy, Dog))
print(isinstance(roy, Animal))
print(isinstance(jo, Dog))
print(isinstance(jo, Bird))

print(issubclass(Dog, Animal))
print(issubclass(Bird, Dog))
——————————————————————————————
True True False True True False
```

上文我们说int、str都是类，那他们类型type（int）的类型是什么呢？

```python 3
print(type(int))
print(type(str))
——————————————————————————————
<class 'type'> 
<class 'type'>
```

通过代码可以发现*类型的类型还是类型*，听起来有些绕，换言之，所有类型(int,type)的类型(type(int))都是类型(type)，因此Python中的**类型之王是Type**，这是理解Python的一种方式。

而Python中所有对象的父类是什么呢？

```python 3
print(issubclass(int, object))
print(issubclass(str, object))
print(isinstance(jo, object))
print(isinstance(roy, object))
——————————————————————————————
True True True True
```

代码告诉我们，**Python中所有对象的父类都是object**，因此object被称为基对象类型。至此我们构建了理解Python的两个视角。

![[Pasted image 20221114230028.png|400]]

面对Alice，如果将其理解为str类型，那从类型的角度理解，进而str是type类型中的一个，type是*元类型*。如果将Alice作为str类的一个实例，则是从类的角度理解，str继承于object类，object是基对象类型。

## 练习

### 构建水果类

1.构建一个水果类（属性：名字，出产季节。抽象方法：print 味道描述）。
2.将你喜欢的水果（如西瓜）构建为子类，并实现抽象方法。
3.再实例化你喜欢水果的对象。



## 练习解析

```python 3
from abc import ABC, abstractmethod

class Fruit(ABC):
    def __init__(self, name, season):
        self.name = name
        self.season = season
        
    @abstractmethod
    def taste(self):
        pass

class Watermalon(Fruit):
    def __init__(self, name, season):
        super().__init__(name, season)
        
    def taste(self):
        
```