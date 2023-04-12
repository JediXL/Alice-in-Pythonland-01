# 数据湍流
![[Pasted image 20220913093638.png]]

## pip

在上一章的思考题中，要求读者输出emoji表情，许多新手玩家会有一种难以下手的感觉，于是去网络上进行搜索“如何用Python打印emoji”，通过对网络答案进行分析，我们会发现答案所给出的第一行几乎都是这样的代码：

```python 3
import emoji
```

回顾上一章内容，我们利用import导入了emoji这个包，而这个包就被我们称为“轮子”。但是很多读者会发现在执行这行代码时并没有import this那么顺利，而是弹出了报错信息：

>ModuleNotFoundError: No module named 'emoji'

在这里首先要声明的是在学习编程语言的过程中，与各种报错信息打交道是家常便饭的事，面对报错信息不要慌张，去分析报错信息反馈的内容并试图解决问题是提升编程能力的重要路径之一。大胆地犯错是我们学习编程语言的捷径之一。

这里的报错声明我们没有一个名叫‘emoji’的模块，这也说明了在Python程序语言中，有一部分“轮子”是自带的（如this），还有一部分轮子是外来的，需要我们安装的（如emoji），学会如何安装后者是我们在学习Python过程中必须掌握的技能。

pip就是最常见的*Python包安装器*，你可以使用pip从Python Package Index（PyPI, Python包索引）和其他索引中安装软件包。读者可以从如下网址学习如何安装和使用pip。

>https://pypi.org/project/pip/

安装完成后，读者可以通过在终端中输入‘pip’来查看pip的具体命令。pip install + \[package_name\]是最常见的包安装方式，但是由于源服务器位于国外，很有可能导致下载安装包时由于网络问题中断，读者可以通过指定服务器下载的方式保证成功率，具体操作方式如下所示。示例中以国内清华大学的源服务器为例。

![[Pasted image 20220913120700.png|500]]


```python 3
pip install emoji i https://pypi.tuna.tsinghua.edu.cn/simple
```

在安装好emoji包之后，我们即可利用该包中的方法进行相应操作，如输出文字对应的表情，同样也可以对表情进行反向输出。

```python 3
import emoji

print(emoji.emojize(":snake:"))
print(emoji.demojize("😭"))
print(emoji.emojize(':loudly_crying_face:'))

——————————————————————————————————————————————
🐍 
:loudly_crying_face: 
😭
```

## 变量的命名

就像给刚出生的小宝宝起名字一样，在日常编程过程中，也需要对我们创造出来的变量赋予**可理解的名称**。这里所谓的“可理解”其实呼应了上一章中提到的程序的**可读性**。一方面为了后续再修改时方便理解，另一方面也为了与他人合作时，他人能以更小成本理解代码含义。在编码圈有一个内部梗说：一个程序员给变量想名字的时间大于真正编写代码的时间。可见要使变量名称具有含义的同时满足规范不是一件容易的事，关于具体的命名规则本书后文还会提到，这里只告诉读者**什么样的命名不可以**。

请读者尝试以下代码：

```python 3
import = 6
```

程序不出意外地报错了，并且是一个非常通用的错误类型“invalid syntax”（语法错误），此处报错的含义是，我们的变量命名“踩雷”了。在Python内部，有许多关键字已经被占用了，如我们已经见到的import，而将这一类关键字作为变量的名称是不被允许的，那我们如何得知这些关键字有哪些呢？可以通过下述代码看到已经被占用的关键字有哪些。

```python 3
help("keywords")
```

同样，我们也可以判断我们所取的变量名是不是在上述关键字列表中，只需要如下实现即可（“in”的用法本书后续仍会介绍，这里只需要简单理解为*判断左侧内容是否在右侧内容中*）

```python 3
import keyword

print("import" in keyword.kwlist)
print("num_fish" in keyword.kwlist)
```

第二种命名错误的典型是*以数字为开头数字作为变量名*，在下述代码中我们无法区分'3w'到底指代什么，到底是'3w'这个变量，还是3乘以'w'变量，还是3个'w'变量？为了避免这种歧义，Python规定不能以数字开头命名变量。

```python 3
3w = "bilibili.com"
w = 3
3w 
```

变量命名的规则可以总结为：**不能有歧义**。有歧义的命名即便不违反语法规则，也会使代码的可读性大打折扣。

## 变量类型

试着去回答“昨天的火锅好吃吗？”这样的问题，你会有什么答案？不同性格的人可能给出的答案各不相同，善于表达和描述的人可能会说“太安逸了，毛肚很新鲜”，比较理性的人可能会用评分来评价“8/10”，比较内敛的人可能会简单回应“好吃”或“不好吃”，这几种表达方式也就基本对应了Python程序设计中常见的数据类型。

>“太安逸了，毛肚很新鲜”——字符串型
>“8/10”——数值类型
>“嗯嗯”——布尔值型

其中数值类型包含了*整数型*和*浮点数型*，可简单通过是否有小数点区分。布尔值型是一个二元变量，只包含**True**和**False**两种情况。字符串类型需要有引号来作为引导。读者可以通过type()方法对自己程序中某一变量的类型进行查看和确认。

```python 3
# different types of variable

var_int = 5
var_float = 6.6
var_string = "What a nice day"
var_bool = True

print(type(var_int))
print(type(var_float))
print(type(var_string))
print(type(var_bool))

——————————————————————————————
<class 'int'>
<class 'float'> 
<class 'str'> 
<class 'bool'>
```

请读者格外注意“123”和123两种变量的区别，前者是可能带有数值含义的**字符串**，后者是**整数型**。

```python 3
a = "123"
b = 123

print(type(a))
print(type(b))
——————————————————————————————
<class 'str'> 
<class 'int'>
```

### 数值类型

我们首先对数值类型数据及其操作进行介绍。数值类型变量就是整数型变量和浮点型变量，而对数值类型变量的操作基本上是计算器上能完成的操作。我们以整数型（int）为例。

```python 3
x = 12
y = 7

z = x + y
print("x + y = ", z, type(z))

z = x - y
print("x - y = ", z, type(z))

z = x * y
print("x * y = ", z, type(z))

z = x / y
print("x / y = ", z, type(z))
```

以上为最基本的加减乘除操作，乘法操作以星号‘\*’表示，除法操作以‘\/’表示，在此例中不能整除，除法结果为小数，故除法结果为浮点型。

```python 3
x / y = 1.7142857142857142 <class 'float'>
```

那整除时除法结果的数据类型就是整型了么？

```python 3
x = 12
y = 6

z = x / y
print("x / y= ", z, type(z))

——————————————————————————————
x / y = 2.0 <class 'float'>
```

可见只要是除法操作，其结果一定是浮点数类型。

除此之外还有几种特殊的数值操作：

```python 3
x = 12
y = 7

z = x // y
print("x // y = ", z, type(z))

z = x % y
print("x % y = ", z, type(z))

z = x ** y
print("x ** y = ", z, type(z))

z = -x
print("-x = ", z, type(z))

————————————————————————————
x // y = 1 <class 'int'> 
x % y = 5 <class 'int'> 
x ** y = 35831808 <class 'int'> 
-x = -12 <class 'int'>
```

其中“//”操作为取商操作，“%”为取余操作，“\*\*”为乘方操作，“-”为取反操作。我们以整型为例介绍了集中常见的数值操作，浮点型与整型操作相同，只是变量类型上稍有区别。**对浮点型变量操作得到的一定是浮点型结果，对整型变量操作不一定得到整型结果**（上文所整型除法得到浮点型结果）。

在对数值类型变量进行操作时还有一些常见函数，能够超越基本计算器的功能：

```python 3
x = -3.2
print("x after abs(): ", abs(x))

x = 6
y = 4
print("divmod(x, y): ", divmod(x, y))

x = 2
y = 3
print('pow(x, y): ', pow(x, y))

x = 4.2384343
print('round(x, 2): ', round(x, 2))

x = 5
y = 6
z = 8.9

print("max(x, y, z): ", max(x, y, z))
print("min(x, y, z): ", min(x, y, z))
```

其中abs()函数会返回变量的绝对值，divmod()会同时返回除法的商和余数，pow()可以通过参数实现更为复杂的乘方操作（本书后文探讨），round(x,n)会*根据四舍五入原则，返回变量带有小数点后n位*，而max()/min()是比较常见的取最值操作。上述代码的输出如下：

```python 3
x after abs(): 3.2 
divmod(x, y): (1, 2) 
pow(x, y): 8 
round(x, 2): 4.24 
max(x, y, z): 8.9 
min(x, y, z): 5
```

#### 数值类型的转换

整数型和浮点型可以在一定程度上进行相互转换

```python 3
x = 16.8
print(x, type(x))

y = 8
print(y, type(y))

# --- convert ---

x = int(x)
print(x, type(x))

y = float(y)
print(y, type(y))


——————————————————————
16.8 <class 'float'> 
8 <class 'int'> 
16 <class 'int'> 
8.0 <class 'float'>
```

需要注意将浮点型转换为整型时会直接截断，将小数部分抛弃。前文提到了需要注意“123”和123两种变量类型的转换，前者这种*具有数字含义的字符串*也可以与数值类型进行转换.

```python 3
x = "123"
y = int(x)
z = float(x)

print(x, type(x))
print(y, type(y))
print(z, type(z))

——————————————————————
123 <class 'str'> 
123 <class 'int'> 
123.0 <class 'float'>
```

但是需要注意，**当具有数字含义的字符串是小数形式时，不能将其转换为整型**。如果一定要实现这样的转换，可以先将这种字符串转换成浮点型，再将浮点型转换为整型

```python 3
x = "123.4"
y = int(x)

print(y, type(y))

——————————————————————
invalid literal for int() with base 10: '123.4'
```

同样试图将不具有数字含义的字符串转换为数值类型时也会有相同类型的报错信息：

>invalid literal for int() with base 10: 'hello'
>invalid literal for float() with base 10: 'hello'


对数值变量赋值之后，再对其数值进行修改时可能会采用如下操作方式：

```python 3
x = 3
x = x + 2
```

在这种操作中还有一种更清晰明了的简便表示方法，该方法与上述表达等价，该广泛应用于循环结构等更为复杂的应用场景，本书后文也会详细介绍。

```python 3
x = 3
x += 2
```

Python同样支持对复数的操作，遵循复数的计算规则即可。

```python 3
x = 12.0 + 4j
y = 8 + 3j

print(x - y)
print(x * 1j)

————————————————
(4+1j)
(-4+12j)
```

#### 数值类型中的随机

随机数的概念是在生活中随时可见的，比如玩桌游的时候需要掷骰子，如果这个骰子是正常情况下，那么产生的点数就应该是随机的。但是前提是“正常情况”。在程序开发过程中也存在着大量的“随机”现象，主要包括两种：真随机和伪随机。

以骰子为例，只要不是骰子有问题，就算你相同的姿势，相同的⼒度，投出来的点数都应该是不⼀样的。因为在真实物理环境中影响结果的因素很复杂，比如空气湿度、气压、手上的汗量等等，这也就是所谓的真随机，真随机具有不可预测性的特点。因此我们想要获得真正的随机数，我们就需要采集真实世界的⼀些信息。

	海森堡原理保证了任何⼈不能因为知道得够多就能预测未来

显然在进行程序开发时要利用真实世界的信息设计出一个真随机数略显麻烦，我们可以通过伪随机数来实现类似的功能。伪随机数的生成实际是算法计算的结果。比如现在时间是10:59分，以9为输入，通过算法输出一个5，在你不知道的情况下，你就会认为这是随机过程，以下列简单小算法为例，就是实现了一个伪随机数的生成。

```python

seed = int(input("Please input a number: "))
random_int = abs(seed * 23 - 2) % 9
print("hey, here is your random number: ", random_int)

```

当你知道这个算法的存在时，实际上输出的结果是可以理论上预测的，这和真随机的不可预测性有着本质的区别。当明白了“随机”意味着什么的时候，恐怕也对当下信息社会中很多的“随机现象”有了不一样的理解。

坚持“不重复制造轮子”的原则，Python为我们提供了实现随机算法的包，即**random**, 使用方法是直接import倒入，由于是自带包，也不需要通过pip进行安装。这一点和import this 类似。

```python
import random
```

如下列举了一下random的常见操作：

```python
import random

r = random.random() # in range [0.0, 1.0)
print("r = ", r)

r = random.randint(1, 3) # int from [a,b]
print("r = ", r)

r = random.randrange(0, 100, 2)
print("r = ", r)

r = random.uniform(1, 3) # float from [a,b]
print("r = ", r)

r = random.choice([1, 2, 3]) # choice one item
print("r = ", r)

r = random.sample([1, 2, 3, 4, 5], 2) # choice k items
print("r = ", r)

r = [1, 2, 3, 4, 5]
random.shuffle(r) # shuffle a sequence (list)
print("r = ", r)
```

最普遍用法是利用random.random()**生成一个范围在\[0,1)内的随机实数**，请注意区间的开闭情况。如果想**生成\[start, stop\]区间内的随机整数**，则通过random.randint(start, stop)实现。还可以通过random.randrange()方法调整随机区间内的递增基数，random.randrange(start, stop, step), step默认为1，**生成的区间是\[start,stop)**。如果要产生浮点数，可以利用random.uniform(start, stop)方法**生成\[start, stop\]区间内的浮点数**，其中start和stop可以不是整数。也可以**在指定的序列中随机选取一个元素**，通过random.choice()方法即可实现。为了**提取出k个不同元素的样本**来做进一步的操作可以使用random.sample(sequence, k)方法。如果**仅需对原列表进行打乱排序**，则可以使用random.shuffle(list)方法，需要注意的是该方法不会生成新的列表，只会把原列表打乱。

#### 数学

提到数学可能许多读者会觉得令人头大，但是在使用编程语言的过程中难免会需要解决数学问题，越是不喜欢数学，越应该学习如何使用Python工具来进行数字操作。就像越是容易计算出错，就越应该使用计算器一样。

通过Python自带的数学包（math），我们不需要知道关于计算的诸多细节，也不需要自己进行设计和计算，我们只需要知道我们的使用目的，就可以获得我们想要的结果。这个包的导入方式和我们最开始演示的一致。

```python
import math
```

首先我们观察一个比较有趣的例子，我们观察*浮点数直接加法*和*利用math.fsum做浮点数加法*的区别。

```python
import math


x = 0.1 + 0.2 + 0.3
print('x equals: ', x)

x = math.fsum([0.1 , 0.2, 0.3])
print('x equals: ', x)

————————————————————————————————
x equals: 0.6000000000000001 
x equals: 0.6
```

通过运行这个实例我们发现两者答案并不一致，这是由于Python本身基于IEEE 754标准（IEEE Standard for Floating-Point Arithmetic，IEEE 754)进行浮点数运算，这种标准的应用会导致较小的精度差。一般情况下，这种较小的精度差不影响计算结果，但是诸如金融、经济等应用场景中对精度要求极高，因此当我们对浮点运算的准确性有特殊要求时，我们可以采用math自带的求和方法。

针对相关应用场景，利用math方法虽然可以精准地返回结果，但是每次调用fsum方法都颇为麻烦，可以使用decimal包。decimal的算术规范描述中说“（decimal的）设计是基于考虑人类习惯的浮点数模型，并且因此具有以下最高指导原则 —— 计算机必须提供与人们在学校所学习的算术相一致的算术。”

>The decimal module provides support for fast correctly rounded decimal floating point arithmetic. It offers several advantages over the float datatype

```python
from decimal import Decimal
```

这里的导入方式和我们之前讲的稍有差别，但通过字面意思能够理解这种导入方式表达的是：*从xx包调用xx方法*。下文这段代码即为decimal的基本使用方式，本质上是**通过将数字以字符串的形式赋值，确保计算准确**。

```python
from decimal import Decimal

onion_price = Decimal('4.6')
beef_price = Decimal('56.7')
rice_price = Decimal('2.3')

sell_price = Decimal('88.5')
sold_num = Decimal('6.0')

print("Cost = : ", onion_price + beef_price + rice_price)
print("Profit = : ", sell_price - (onion_price + beef_price + rice_price))
print("Total Profit = : ", sold_num * (sell_price - (onion_price + beef_price + rice_price)))
```

此外，math中包含了比较常见的数学用值，比如圆周率$\pi$通过math.pi的方式可以直接呈现，同理可以直接呈现的还有自然对数e和无穷大∞。比较特殊的是可以通过math.nan方法产生一个浮点型的'nan'，这个值不是一个合法数字，后续也会利用这个方法判断某一个变量或值是不是合法数字。

math中还包含了一些常用的数学方法，比如前文提到过的求绝对值方法，fabs方法会返回绝对值并且保存为浮点型。ceil和floor方法与英文单词本身表达的意思一致，代表的是向上取整和向下取整。factorial代表数学中的阶乘方法，gcd表示求两个数的最大公约数。

```python
import math

print(math.pi) # 圆周率pi

print(math.e) # 自然对数 e 

print(math.inf) # 无穷大值 inf

print(math.nan) # Not a number 可以判断是否是一个数

print(math.fabs(-3)) # 绝对值且变成浮点型
print(math.ceil(10.2)) # 向上取整 11
print(math.floor(10.2)) # 向下取整 10
print(math.factorial(3)) # 阶乘
print(math.gcd(18, 9)) # 最大公约数
```

至此，我们在数据湍流的探索就结束了，让我们继续深入Python大陆。

## 练习

### 学费计算

问题描述：大学第一学期必选课程及其学分如下：

| Python | 高等数学 | 大学英语 | 大学体育 | 军事理论 | 哲学  |
|:------:|:--------:|:--------:|:--------:|:--------:|:-----:|
| 3学分  |  4学分   |  4学分   |  2学分   |  2学分   | 2学分 |

请计算并输出大一学期共修多少学分？输入每学分应缴纳的学费（整数，单位为元），计算并输出第一学期应缴纳多少学费？

输入
输入一个表示每学分应缴纳的学费的整数
输出
按示例格式分两行输出学分和学费

示例
```python 3
输入：
328
输出：
你本学期选修了17个学分
你应缴纳的学费为5576元
```

### 助学贷款计算

问题描述：大学第一学期必选课程及其学分如下：

| Python | 高等数学 | 大学英语 | 大学体育 | 军事理论 | 哲学  |
|:------:|:--------:|:--------:|:--------:|:--------:|:-----:|
| 3学分  |  4学分   |  4学分   |  2学分   |  2学分   | 2学分 |

大学生可以申请助学贷款，申请额度不超过学费和生活费总额的60%，分两行依次输入每学分应缴纳的学费（整数，单位为元）和你每个月的生活费（浮点数，单位为元），请计算你每个学期能够贷款多少元？（结果保留小数点后2位数字，每个学期按5个月算）

示例
```python 3
输入：
328
1600
输出：
本学期你能够贷款8145.6元
```

### 猜数字游戏

使用random生成一个1到10之间的随机整数，让玩家通过输入来猜这个数等于多少。若输入大于该随机数则提示high，输入小于该随机数则提示low。正确答案则显示bingo。


