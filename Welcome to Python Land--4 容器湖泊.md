# 容器湖泊

![[Pasted image 20221004102144.png]]

当明晰了Python程序设计中的一些结构及其特性后，Alice开始探索下一个未知场景。

## 字符串作为容器

Alice徐徐向前，发现有个熟悉的身影坐在湖边的篝火处，她快步向前打起了招呼。

>Alice:
&nbsp;&nbsp;&nbsp;&nbsp;Str, glad to see you here.
???:
&nbsp;&nbsp;&nbsp;&nbsp;Str? Yes … that was what they used to call me，str as a type.
Alice:
&nbsp;&nbsp;&nbsp;&nbsp;Str?
str as a container:
&nbsp;&nbsp;&nbsp;&nbsp;I am **str the container**. And I come back to you now – at the container lake.

Alice遇到了老熟人str，但是貌似str阴阳怪气地告诉Alice自己已经不是从前那个自己了，欢迎Alice来到容器湖泊重新认识自己。

我们之前将字符串型(str)作为一种变量类型向各位读者进行介绍，而现在str竟“矢口否认”，我们看看为什么str将自己称为容器。

```python 3
a = 'Hello'

print(a[0])
print(a[1])
print(a[2])
print(a[3])
print(a[4])
```

通过这段代码的展示，读者可以发现字符串a和我们之前讲的变量稍有区别，前文提到变量就像一个箱子，而给变量赋值就像给纸盒子中装东西，但前文装的东西貌似都是一个整体，比如数字“123”。而在这里的字符串a竟然可以把里面的东西逐个取出来，取出来的东西为一个个的新字符串。这似乎是某种神秘的新特性。

而我们取出东西的方式是通过一个数字将它取出，这个数字就是所谓的**索引**，换言之字符串就像是一个大箱子，我们可以把箱子里的东西按照某种编号逐一取出。需要注意的是**Python语言中的索引号是从0开始计数的**，也就是这种编号是从0开始的。其实我们不光可以按需取出，还可以利用索引达成一个Python的经典操作——**切片**。在开篇我们提到Python有一个重要的特性是易于处理数据，而其体现出来的具体一条就是*易于对数据做切片操作*。

那么什么是切片呢，刚才我们通过索引的方式逐一地取出了容器中的内容，从代码上看*一个索引只能取出一个对应的内容*，但是切片操作可以取出容器中*一个范围对应的内容*。就像一个大西瓜经过切片处理后就可以得到我们想要的几瓣西瓜。让我们来看看如何实现切片操作：

```python 3
a = 'Python'

print(a[1:3])
print(a[1:])
print(a[::2])
print(a[1:4:2])

print(a[-1])
print(a[1:-2])
print(a[-1::-1])
print(a[3::-2])

————————————————————
yt 
ython 
Pto 
yh

n 
yth 
nohtyP 
hy
```

对字符串进行切片的基本操作是在字符串后加一个中括号，中括号中由数字和冒号填充，如a\[1:3\]。具体来说，中括号所表示的规则为：**\[start:stop:step\]**，所表示的基本含义是，在**左闭右开区间\[start, stop)，按照步长step进行切片**。默认情况（不填写的情况）下start为0，stop为空表示输出到最后一位为止，step默认为1。

举例来说，a\[1:3\]中只包含start和stop，分别赋值1和3，所表示含义是按照步长为1输出索引号为\[1, 3)的内容。索引号1代表的是y，索引号3代表的是h，因此输出的是从y（包含）到h（不包含）的所有内容，即“yt”。a\[1:\]中只表明start为1，则按照步长为1从索引号1开始输出到最后一位，即为“ython”。同理，a\[::2\]表示按照步长为2（隔一个输出一个）从第一位开始输出到最后，结果为“Pto”。

在上述代码中，读者会发现第二段代码中出现了大量的负数。在Python程序语言中，正序是从0开始的索引号，即0,1,2...，而**倒序的索引是从-1开始**，即-1,-2,-3...。我们以单词“Python”为例，展示两种方向的索引号变化。

![[Pasted image 20221008095308.png|300]]

具体分析上述代码，首先a\[-1\]表示的是a（Python）的最后一个元素（倒数第一个内容），即“n”。a\[1:-2\]表示按照步长为1输出从索引号1到索引号为-2的内容，即“yth”。如果在切片中发现**步长step为负，则代表反向输出**，step为-1代表反向挨个输出，step为-2代表反向隔一个输出一个。a\[-1: :-1\]代表从倒数第一个元素开始反向输出，这是在后续过程中都很常见的*逆序逐个输出*。a\[3: :-2\]表示的是从索引号为3的元素开始反向隔一个输出一个，结果为“hy”。

作为容器的字符串还有其他常见的操作，如简单的**相连**和**乘法**，相连用“+”体现，乘法以“\*”实现，这部分内容可以应用在第一章的练习题中。

```python 3
a = "Hello"
b = 'my friend'
c = a + b

print(c)

d = 'Nice Try'
e = d * 10

print(e)
```

在数据分析中更为常见的操作是**取长度**，即我们需要知道容器里面的成员数量时，可以通过 **len()** 来实现。需要注意的是容器中的*空格是需要占位的*，若容器为空则长度为0。读者还应注意容器索引号和容器元素长度的关系（长度=最后索引号+1）。到这里，读者可以回顾第一章的最后一题，如何利用len()、相乘等来实现第一行和第三行长度相等。

```python 3
a = "Welcome"
print(len(a))

b = "Hey jude"
print(len(b))

c = ""
print(len(c))
```

当我们需要将⼀个容器⾥的所有元素过⼀遍时，我们可以采取**遍历**操作。遍历操作可以结合已经学过的while循环和海象操作符来实现。请读者注意条件控制变量i的始终值和变化情况。

```python 3
a = "Python"
i = -1
while (i := i + 1) < len(a):
    print(f"i = {i}, a[{i}] = {a[i]}")
```

## for 语句

除了利用while循环进行遍历之外，在容器操作中更为常见的遍历方法是**利用for语句实现遍历操作**。或许有读者在生活中或学习别的语言过程中听说过所谓“for循环”，在Python语言中所谓的for循环实质上是一种**遍历操作**，这也是Python与其他语言的区别之一。

```python 3
a = "Python"
for i in range(0, len(a)):
    print(f"i = {i}, a[{i}] = {a[i]}")
```

这是第一种用for语句表示遍历的办法，我们借助了几个常见的方法。首先in方法在前文也有所提及，表示的是如果i在这个范围内，则执行下列内容。第二个方法是**range**, 它表示一个范围range(start,stop)表示的仍然是**左闭右开区间\[start, stop)**。range的作用就像是体育考试站在场边数圈的老师，每过一圈就+1。所以上述for语句可以理解为i起始为0，运行一次for语句则+1，直到i=len(a)为止（需要注意i的结束条件）。按照这样的逻辑，结合输出语句，我们就可以按照a的索引号（a\[\]）进行遍历，将a逐个打印。注意这里的i是一个指示符，类似于while循环中的条件判断变量，因此对应换成其他字母也是可行的。这就是**结合for语句按照索引号进行遍历**的方法。

```python 3
a = "Python"
for s in a:
    print(s)
```

第二种利用for语句进行遍历的方式更为直接，我们直接判断s是不是a中的内容，如果是则打印。这里的s同样是指示作用，可以随意命名。这种较为直接的方法是**结合for语句按照内容进行遍历**的方法。

## Python常见容器

我们利用str这种容器展示了一些容器特性，让读者初步感知容器的概念，容器就像一个更大的箱子，可以包含其他数据类型或容器，我们也可以对容器中的对象进行操作。那我们为什么需要容器呢？

在前文我们提到容器比较容易对数据进行处理，而生活中我们提到数据，往往会说“数据流”，在直观的感受中，数据就像“水流”一般。那水又具有怎样的特性呢？

著名武术大师李小龙先生一直追寻“化为水”（Be Water）的人生哲学，他在接受美国电视采访时曾经表达过水的特性：
>A good martial artist is like water. Why? Because water is insubstantial. By that, you can't grab it, you can't punch and hurt it, so be soft like water and flexible. Empty your mind. Be formless, shapeless like water. **You put water in a cup, it becomes the cup. You put water in a bottle, it becomes the bottle. You put water in a teapot, it becomes the teapot.** Water can flow or crash. Be water, my friends!

李小龙先生说，我们把水放在什么容器中，水就会变成什么。和水类似的数据也有这样的特性，**我们将数据放到不同的容器中，就会呈现不一样的性质，从而利于不同维度的分析和挖掘**。

除了str之外，Python语言中还有四种常见容器，分别是：List, Tuple, Set, Dictionary。Alice将逐一探索。

### List（列表）

我们仍然可以利用“=”对一个列表进行定义和赋值。

```python 3
l = [1, 2, 3, 4, 5]
```

在探索容器湖泊的过程中，首先要注意的是**容器的呈现方式**。List容器是以**成对方括号（中括号）呈现**的，这是容器的形状。不同的容器形状不同，性质也不同。前文介绍道容器内可以包含其他类型数据或容器，但是str中只能包含str类型（容器），相比来说List就像便当盒一样，可以同时容纳不同类型的数据。

```python 3
l = [1, 'good', 'day', True, 5.4]
```

在上述List中不仅包括了整型、浮点型、布尔型数据，也包括了字符串型数据（容器）。与str类似的是，List作为容器也可以*相连、相乘和取长度*。

```python 3
l1 = [1, 2, 3, 4, 5]
l2 = [1, 'good', 'day', True, 5.4]
print(l1 + l2)

l3 = [0]
print(l3 * 5)

l4 = [1, 2, 3, 4, 5]
l5 = ['good', 'day', True, 5.4]
l6 = []

print(len(l4))
print(len(l5))
print(len(l6))
```

需要注意的是List通过“+”相连起来不是组合出两个List，而是将二者合成一个List。同理上述相乘不是产生5个列表，而是将列表内的元素重复5次生成一个新列表。取列表的长度就是输出列表内元素的个数，空列表的长度为0。

同样也可以利用for语句对List进行遍历，同样是利用索引号进行遍历和直接对内容进行遍历两种方法。

```python 3
l = ['good', 'day', True, 5.4]
for i in range(0, len(l)): #利用索引号进行遍历
    print(l[i])

for item in l: #直接对内容进行遍历
    print(item)
```

#### 基本操作

掌握容器特性时除了要了解容器的呈现方式，还要关注容器的基本操作，即**增删改查**。列表的增加可以利用append方法直接增加对应元素，remove方法则执行相应的删除操作，这两个方法直接对*元素*进行操作。在对列表进行修改时，可以对索引号对应元素直接修改，这里的操作是对*索引号*进行操作。判断一个元素是否在列表内利用的是之前提到的in方法，会返回True或False。与in相对应，还可以通过not in判断一个元素是否不在列表中。

```python 3
l = [1, 2, 3]

l.append(4)
print("After append:", l)

l.remove(2)
print("After remove:", l)

l[-1] = 5
print("After update:", l)

print("4 in l ?", 4 in l)
print("1 in l ?", 1 in l)

l = ["dear", "whale", "copy", "python"]

print("dear" not in l)
print("sound" not in l)
```

列表也可以像字符串一样进行切片操作，基本的原理的操作过程都是类似的，读者可以回忆切片相关的操作，判断下列代码的输出结果。

```python 3
l = [1, 2, 3, 4, 5]

print(l[1:4])
print(l[::2])
print(l[-1::-1])
```

除却*增删改查*，尤其是列表内只包含数据类型时，所用到常用操作还包括**排序**。调用的方法是List.sort()，读者也能轻易从该方法的英文名称判断方法的功能，需要注意的是sort方法默认是*顺序排序*，即按照从小到大的顺序进行排序，若要进行逆序排序，则需要对sort方法内的关键字reverse赋值为True。

```python 3
l = [205, 8.2, 103, 95]

l.sort()
print(l)
————————————————————
[8.2, 95, 103, 205]

l.sort(reverse=True)
print(l)
————————————————————
[205, 103, 95, 8.2]
```

但是使用sort方法需要小心谨慎！因为sort方法会改变原列表。若不想对原列表进行更改，则需要使用sorted方法进行排序，读者注意比较两者之间的区别。

```python 3
l = [205, 8.2, 103, 95]

new_l = sorted(l)
print("l: ", l)
print("new_l: ", new_l)
————————————————————
l: [205, 8.2, 103, 95] 
new_l: [8.2, 95, 103, 205]
```

#### List Anything

上文提到List这种容器内可以包含其他类型数据，如同时包含数值型、布尔型、字符串型的情况，同时List这种容器内还可以再放一个List（即容器内包含容器），这种结构称之为*嵌套*。为了代码的可读性，一般这种嵌套不超过3层。

```python 3
l = [1, "hello", ["nice", "try"]]

print(l)
————————————————————
[1, 'hello', ['nice', 'try']]
```

如果这时想提取该列表中的'nice'应该怎样操作呢？结合上文提到的索引号，其实这种操作就和在真实世界中寻找地址很类似，我们要先框定大的范围，再选取小的范围。字符串l就像是小区名，l中的\['nice', 'try'\]就是楼栋数2（l内的索引2的位置），而'nice'就在这栋楼的第0层（\['nice', 'try'\]这个列表中索引0的位置），因此进行组合l\[2\]\[0\]即为'nice'的索引位置。我们同样可以利用这种方法，取得'try'这个单词的最后一个字母'y'，只不过是再加一层索引而已。再次向各位读者强调，Python中的**索引从0开始**，下列代码还用对比的方式呈现了索引中-1的妙用，请各位读者注意区分不同的-1代表哪个元素。

```python 3
l = [1, "hello", ["nice", "try"]]

print(l[2][0])
print(l[2][1][2])
print(l[2][1][-1])
print(l[2][-1][-1])
print(l[-1][-1][-1])
```

### Tuple

学习了str容器和List容器之后，在接下来对其他容器进行学习的过程中，主要关注呈现方式和特性的差异。

Tuple容器称为元组，是以**成对圆括号（小括号）呈现**的，元组容器内也可以同时容纳不同类型的数据。元组容器的切片操作与前者无异，需要注意player\[1:\]的返回类型仍为元组。除此之外，元组还可以执行**解包**操作，可以将元组内元素解包赋值给不同的变量，需要注意*解包变量的数量和元组内元素的数量应该相等*。

```python 3
player = ('Alice', 'warrior', '99')

print(player[0])
print(player[1])
print(player[2])
print(player[1:]) #('warrior', '99')

name, role, att_power = player
print(name, role, att_power)
——————————————————————————————
Alice warrior 99
```

上述规则主要是限制了解包变量的数量不大于元组内元素的数量，当我们不关注元组内的某个元素时，*对应地可以把相应变量名取为下划线*。举例来说，我们只关心玩家的姓名和攻击力，而不关心她的角色，则可以按如下方式实现。

```python 3
player = ('Alice', 'warrior', '99')

name, _, att_power = player
print(name, att_power)
——————————————————————————————
Alice 99
```

特别需要强调的是，**Tuple容器的元素不支持修改**，如果你进行如下操作，会得到报错信息。

```python 3
player = ('Alice', 'warrior', '99')
player[0] = 'Tom'
```

>TypeError: 'tuple' object does not support item assignment

这也就是说Tuple容器初始被定义成什么样就是什么样，这虽有不便之处，但是当我们不希望内容被修改时，Tuple容器就恰到好处。

### Set

Set容器称为集合，是以**成对花括号（大括号）呈现**的，集合容器内也可以同时容纳不同类型的数据。和前述容器不同的是，在Set容器内，**不包含任何重复元素**。同时Set内也不能包含List、Set这种“可变类型”，只能包含类似Tuple、str、number这样的“不可变类型”。

```python 3
Players = {'Alice_1', 'Alice_2', 'Alice_3', 'Alice_3'}

print(Players)
——————————————————————
{'Alice_1', 'Alice_2', 'Alice_3'}
```

在List容器中，我们放入什么则会返回什么，元素顺序也不会发生改变，但是在Set容器中却不尽相同。我们向Set容器内放入一组汽车品牌名，会发现输出结果并不是输入的顺序，也不是传统的按照字母顺序排序，这是Set容器的第一个特性，**无序性**。或者说我们在使用Set容器时*不要假定Set中的元素存在顺序*。sorted方法可以对所有可迭代的对象进行排序，因此利用已经学过的sorted方法可以对Set进行排序，但是需要注意*sorted返回的是一个以字母表顺序进行排序的列表*。

```python 3
s = {'BMW', 'BYD', 'Audi', 'Aston Martin'}

print(s)
————————————————————————————
{'Audi', 'BMW', 'Aston Martin', 'BYD'}

ss = sorted(s)
print(ss)
————————————————————————————
['Aston Martin', 'Audi', 'BMW', 'BYD']
```

当Set容器中存有数字时情况会稍有不同：

```python 3
s = {1, 2, 3, 4, 5}
print(s)
————————————————————————————
{1, 2, 3, 4, 5} 

ss = {6, 7, 8, 9}
print(ss)
————————————————————————————
{8, 9, 6, 7}

sss = {1, 2, 6, 7, 8, 9}
print(sss)
————————————————————————————
{1, 2, 6, 7, 8, 9}

ssss = {1, 5, 4, 3, 2}
print(ssss)
————————————————————————————
{1, 2, 3, 4, 5}
```

看起来Set内的数字排序时灵时不灵，这证明Set内元素顺序和哈希算法有关，而数字的排序取决于数字本身和哈希的关系。这也就意味着若集合以哈希为基础进行排序且哈希值没有发生“碰撞”的情况下（以小数字为例），看起来Set的数字是有序的。Set内元素的顺序问题是颇为复杂的，也远超出本书的范畴，在这里只想提醒各位读者在遇到Set容器时就把它想象为数学上的“集合”，*不要假定Set中的元素存在某种顺序*。

>https://stackoverflow.com/questions/45581901/are-sets-ordered-like-dicts-in-python3-6

既然作为数学意义上的“集合”，那Set也可以实现数学意义上的*交、并、差*等操作。利用\&操作符实现两个集合的交集，\|表示两个集合的并集，\-表示两个集合的差集，s1-s2表示的是s1有但s2没有的元素，反之亦然，利用\^就可以求得对等差分集合（所有只在两个集合其中之一的元素组成的集合）。

```python 3
s1 = {1, 2, 3, 4}
s2 = {1, 2, 3, 5}

s_inter = s1 & s2
s_un = s1 | s2
s_diff = s1 - s2
s_diff2 = s2 - s1
s_symdiff = s1 ^ s2

print(s_inter, s_un, s_diff, s_diff2, s_symdiff)
————————————————————————————
{1, 2, 3} {1, 2, 3, 4, 5} {4} {5} {4, 5}
```

上述功能同样还可以利用Python内置方法来实现。

```python 3
s1 = {1, 2, 3, 4}
s2 = {1, 2, 3, 5}

print(s1.intersection(s2))
print(s1.union(s2))
print(s1.difference(s2))
print(s2.difference(s1))
print(s1.symmetric_difference(s2))
————————————————————————————
{1, 2, 3} {1, 2, 3, 4, 5} {4} {5} {4, 5}
```

由于Set容器内不包含任何重复元素，因此Set容器应用最广泛的功能是：**利用Set去重**。假设有一个具有重复元素的列表，可以通过将列表转换为集合进行去重，然后再转换为列表即可。这其中也包含了类型的转换，读者应该较为熟悉，与前不同的是这里进行的是容器类型的转换。

```python 3
l = [1, 1, 1, 2, 4, 5, 9, 3, 3, 6]

l = list(set(l))
print(l)
————————————————————————————
[1, 2, 3, 4, 5, 6, 9]
```

我们同样可以对集合内的元素进行**增删改查**。add方法适用于添加单一元素，update方法适用于添加一组新的元素，remove则正如字面意思，删除相应的元素。

```python 3
s = {1, 2, 3}

s.add(4)
print("after add():", s)

s.update({4, 5, 6})
print("after update():", s)

s.remove(1)
print("after remove:", s)
```

当使用remove方法删除集合内本就没有的元素时会产生如下错误信息。当集合内元素较多时我们如果要先判断元素是否在集合内再删除就略显繁琐，这时我们可以使用discard方法，该方法的功能是若有则删除，若无则无（不会报错）。

```python 3
s.remove(7)
————————————————————————————————————————
KeyError Traceback (most recent call last)
KeyError: 7

s.discard(7)
print("after discard 7:", s)

s.discard(3)
print("after discard 3:", s)
————————————————————————————————————————
after discard 7: {2, 3, 4, 5, 6} 
after discard 3: {2, 4, 5, 6}
```

### Dictionary

字典Dictionary是Python常见容器中的最后一种，同样是以**成对花括号（大括号）呈现**的。但是字典内包含的是一组一组的**键值对（key:value）**。键值本质上提供了一种新的定位方式，在前述列表中我们通过索引号来取值，但是字典中可以*通过key取对应的value值*。

```python 3
Alice = {
	'name' : 'Alice',
	'attPower' : 15,
	'defense' : 6,
	'magic' : 20
}

print(Alice)
——————————————————————————
{'name': 'Alice', 'attPower': 15, 'defense': 6, 'magic': 20}

print(f"{Alice['name']}'s attack power is: {Alice['attPower']}")
——————————————————————————
Alice's attack power is: 15
```

有的读者会疑问，为什么Set和Dictionary共享了同一种呈现方式呢。首先，Set容器的表示方式是在Python2.7之后才更换为花括号的，严格的来说是Set占用了Dictionary的表示方式。其次，如果读者细心会发现在集合中利用remove删除不存在的元素报错信息是“KeyError”，也就是说所寻找的*Key*不存在，这也就揭示了集合和字典之间的关系——集合就像是没有值的字典（A set is like a dict with keys but no values）。所以二者用同一种呈现方式也就不奇怪了。

由于二者使用了同一种呈现方式，各位读者需要注意使用\{\}创建新容器时会获得一个**空字典**，若要创建一个空集合，则需要用set()方法。当然也可以利用该方法创建非空集合。

```python 3
d = {}
print("The type of d is:", type(d))
  
s = set()
print("The type of s is:", type(s))
————————————————————————————————————
The type of d is: <class 'dict'> 
The type of s is: <class 'set'>

s_ne = set('happy day')
print("s_ne is:", s_ne)
print("The type of s_ne is:", type(s_ne))
————————————————————————————————————
s_ne is: {'d', 'a', 'h', 'p', 'y', ' '} 
The type of s_ne is: <class 'set'>
```

由于字典中的每个项目（item）都包含键值两个指标，因此在字典内对元素进行遍历时要同时对key和value进行遍历。读者需要注意这里for语句的差别，首先前面是两个变量，分别代表key和value（k,v的命名可任意更改，但为了代码的可读性，一般约定俗成使用k，v）,其次遍历的对象是Alice.items()，即“字典名.items()”。

```python 3
Alice = {'name': 'Alice', 'attPower': 15, 'defense': 6, 'magic': 20}

for k, v in Alice.items():
	print('Key:', k, '|','Value:', v)
```

若想单独对字典内的键或值进行遍历，只需将遍历的变量更改为1个，同时约定遍历的范围即可。这里约定的范围就变成了Alice.keys()或Alice.values()。

```python 3
Alice = {'name': 'Alice', 'attPower': 15, 'defense': 6, 'magic': 20}

for k in Alice.keys():
    print('Key:', k)

for v in Alice.values():
    print('Value:', v)
```

同时，判断某元素是否在字典内时也应该规定寻找的范围，否则会得到与预期不符的结果。

```python 3
Alice = {'name': 'Alice', 'attPower': 15, 'defense': 6, 'magic': 20}

print('name' in Alice.keys())
print('age' in Alice.keys())

print(15 in Alice.values())
print(100 in Alice.values())
```

如果读者去直接调用字典内没有的元素，则会同样报错KeyError，就像经常出现于肥皂剧中的“我的字典里没有xx”。当字典内项目过多，想取得某个元素但又不想在没有的时候报错则可以使用*get*方法，get方法实现的功能即为：有则取，无则返回设定值。

```python 3
Alice = {'name': 'Alice', 'attPower': 15, 'defense': 6, 'magic': 20}

print(Alice.get('age', 18))
————————————————————————————
18

Alice = {'name': 'Alice', 'attPower': 15, 'defense': 6, 'magic': 20, 'age': 19}

print(Alice.get('age', 18))
————————————————————————————
19
```

对字典进行增删改的方法都很直观，只需要利用键对相应值进行修改，若字典中无该键，则会对应增加该键值对。

```python 3
Alice = {'name': 'Alice', 'attPower': 15, 'defense': 6, 'magic': 20}

Alice['magic'] = 25
print(Alice)

Alice['age'] = 20
print(Alice)

del Alice['age']
print(Alice)
——————————————————————
{'name': 'Alice', 'attPower': 15, 'defense': 6, 'magic': 25} 
{'name': 'Alice', 'attPower': 15, 'defense': 6, 'magic': 25, 'age': 20} 
{'name': 'Alice', 'attPower': 15, 'defense': 6, 'magic': 25}
```

在这里我们使用一个小实例体现字典中键值对和其他容器的差异性。读者需要利用字典对以下句子中的字母（不区分大小写）出现频次进行统计：

>And so with the sunshine and the great bursts of leaves growing on the trees, just as things grow in fast movies, I had that familiar conviction that life was beginning over again with the summer.

读者们自然会想到利用字典的键值对，一个字母(key)就对应一个数字（value：出现的频次），通过对该语句的遍历即可完成该任务。

```python 3
sentence = "And so with the sunshine and the great bursts of leaves growing on the trees, just as things grow in fast movies, I had that familiar conviction that life was beginning over again with the summer."

sentence = sentence.lower() 
count = {}
for s in sentence:
    count[s] = count[s] + 1
print(count)
```

由于不区分大小写，所以先将整个句子都转换为小写字母，然后创建了一个空字典，随后对句子内的每个字母进行遍历，并且出现一次就给对应的value+1。这样的设计意图可谓毫无破绽，但是在实际执行过程中会发现代码无情地报错了，原因是字典中空无一物，当你第一次发现某个字母想给value+1的时候系统会发现压根没有这个键值，所以报错，类型为“KeyError”。因此，可以利用学过的*分支结构*进行改进，若是第一次出现就以该字母为key，value赋值为1，若后续再次出现则对应的value+1即可。

```python 3
sentence = "And so with the sunshine and the great bursts of leaves growing on the trees, just as things grow in fast movies, I had that familiar conviction that life was beginning over again with the summer."

sentence = sentence.lower() 
count = {}
for s in sentence:
    if s not in [',', '.',' ']:
        if s in count.keys():
            count[s] = count[s] + 1
        else:
            count[s] = 1
print(count)
```

但是！本着能偷懒绝不多写一行的原则，怎么能在不要如上的分支结构情况下完成这个任务呢？这时候又要借助成熟的“轮子”了，此处要借用的是
defaultdict方法，从名字也可以看出它一定和字典有某种联系，这个方法称为“自定义字典”，它提供和字典几乎相同的功能，但是使用该方法**不会引发“KeyError”**，因为该方法为*不存在的键提供了默认值*，此处defaultdict(int)指的是创建的自定义词典的value默认为整数型，括号内可供选择的选项有list、set和int。

```python 3
sentence = "And so with the sunshine and the great bursts of leaves growing on the trees, just as things grow in fast movies, I had that familiar conviction that life was beginning over again with the summer."

from collections import defaultdict


sentence = sentence.lower()
count = defaultdict(int)

for s in sentence:
    if s not in [',', '.',' ']:
        count[s] = count[s] + 1
print(count)
```

### 深浅拷贝

首先请读者比较一下两段代码的输出差别，输出结果是否和你预想的有所不同？其中第一段代码是第一章的练习题

```python 3
x = 1
y = x
y = 4

print("x = ", x)
print("y = ", y)
```

```python 3
x = [1, 2, 3]
y = x
y[0] = 999

print(x)
print(y)
```

看似很简单的两段代码，都是对某个变量进行了（部分）修改，但是输出的结果可能出乎了读者的预料。在第一段代码中，将1赋值给x，然后将x赋值给y，然后再将4赋值给y，通过输出可以发现y此时为4，x为1，这应该是在大部分读者意料之内的。

第二段代码中，将\[1, 2, 3\]这个列表赋值给x，随后将x赋值给y，此时y也是个列表，将y列表中索引号为0的元素修改为999，输出后惊奇地发现x中索引号为0的元素竟然也同步修改了！

这种现象称之为**浅拷贝**，在Python程序语言中，当我们将某个变量赋值给另一个变量时，若双方都是容器，则只做浅拷贝，意味着这两个变量实质都指向的是一个容器，就像同一个人对应了多个外号一样。这种方式能够有效节省内存，但是带来的问题是修改一个变量的时候，指向该容器的其他变量也会同步修改。

如果想赋值之后，每一个变量对应不同容器，则需要采用**深拷贝**方法。此时需要导入copy包，利用copy.deepcopy()方法来实现。

```python 3
import copy


x = [1, 2, 3]
y = copy.deepcopy(x)
y[0] = 999

print(x)
print(y)
————————————————————
[1, 2, 3] 
[999, 2, 3]
```

### 列表推导式

在本章的最后，我们介绍一个Python的大杀器，首先请大家考虑这样一个任务：生成一个包含所有扑克牌的列表。

当然我们可以使用穷举法将每一张牌逐个添加到列表内，但是这种方法稍显原始。我们首先分析扑克牌的特性，每副扑克牌除大小王之外有*四种花色*，每种花色都有2-10和J、Q、K、A十三张牌，因此我们首先可以定义牌的花色和每种花色中的13张牌。

```python 3
decor = ["♥", "♠", "♦", "♣"]
card_class = [str(i) for i in range(2, 11)] + ["A", "J", "Q", "K"]
```

读者会发现在第二个列表，也就是牌的种类创建时，列表内部竟然有一个for语句进行遍历，这就是Python的大杀器——**列表推导式**。本质上这个绝招的功能是通过*将for语句写入列表而简明扼要地创建列表*。我们定义了花色和牌型，加上这个绝招，我们可以较为轻易地创建一副扑克牌列表。

```python 3
cards = [a + b for a in decor for b in card_class] + ["Bjoker", "Rjoker"]

print(cards)
```

其中a就是花色，b是牌型，我们再次利用列表推导式完成了列表的生成，不要忘记最后还要把大小王加入牌堆。

学会了这个绝招后，Alice继续向Python Land深处探索。

## 练习

### 3位水仙花数计算

“3位水仙花数”是指一个三位整数，其各位数字的3次方和等于该数本身。例如：ABC是一个“3位水仙花数”，则$$A^3 + B^3 + C^3 = ABC $$
请按照从小到大的顺序输出所有的3位的水仙花数，请用一个“逗号+空格”分割输出结果。**请注意输出格式要严格一致，最后一位水仙花数后没有逗号。**

#### 输入格式
无

#### 输出格式
示例：123, 234, 345
(这几个数字并不是水仙花数，只是用来表示输出格式)

### 打印爱心

给定如图左的列表，请打印如图右的爱心形状
![[Pasted image 20221015210910.png|400]]

```python 3
spe = "@"

l = [['.', '.', '.', '.', '.', '.'],
['.', spe, spe, '.', '.', '.'],
[spe, spe, spe, spe, '.', '.'],
[spe, spe, spe, spe, spe, '.'],
['.', spe, spe, spe, spe, spe],
[spe, spe, spe, spe, spe, '.'],
[spe, spe, spe, spe, '.', '.'],
['.', spe, spe, '.', '.', '.'],
['.', '.', '.', '.', '.', '.']]
```

### 井字棋

根据井字棋规则设计小游戏，具体要求如下：
1、游戏开始时两位玩家依次输入姓名
2、由随机一位玩家开始，两位玩家依次行棋
3、每次行棋后打印当前棋盘
4、一方获胜或平局游戏结束
5、输出游戏结果

## 练习解析

**3位水仙花数**计算题目有两个关键点。本题的第一个关键点是对**三位数进行分解和提取**。第一种提取方式是**数学方法**，首先对某三位数除以100求商提取*百位数字*，然后用该数字减去百位数字\*100之后除以10求商提取*十位数字*，最后用该数减去（百位数字\*100 + 十位数字\*10）之后提取*个位数字*（个位数字还有其他的数学方法进行提取，请各位读者思考）。

第二种提取方法则运用了**容器特性**。首先将范围内的数字转换为字符串，利用**字符串及其切片操作**（根据索引号）即可快速分离三位数字（此时这三个元素的类型是字符串）。但需要注意的是，后续还需进行数学运算进行判断是否是水仙花数，因此需要把字符串类型转换回数字类型进行计算。这里就体现了为什么需要容器，我们希望放进容器的数据具有一些我们所希望的特性，因此我们也可以选用不同的容器来满足某种特性。

本题的第二个关键点是格式要求，即**每个数字之间应该有逗号，且最后一位水仙花数后没有逗号**。因此要对储存的结果进行判断，判断当前输出的数字是不是最后一个水仙花数。利用list的遍历操作即可进行判断并添加逗号。

```python 3
#solution 1
res = []
for i in range(100, 1000):
    h = i // 100
    t = (i - h * 100) // 10
    s = i - h * 100 - t * 10
    if h**3 + t**3 + s**3 == i:
        res.append(int(i))
answer = ""
for r in res:
    answer += str(r)
    if r != res[-1]:
        answer += ', '
print(answer)


#solution 2
res = []
for i in range(100, 1000):
    s = str(i)
    if int(s[0])**3 + int(s[1])**3 + int(s[2])**3 == i:
        res.append(s)
answer = ""
for r in res:
    answer += r
    if r != res[-1]:
        answer += ', '
print(answer)
```

**打印爱心**主要考查对容器内元素的查找和操作。题目要求是要按列进行打印，因此首先获取列的长度。在列的遍历内打印每一行的当前列，由于要打印两个爱心，要注意打印出来的每一行应该乘2。

```python 3
spe = "@"

l = [['.', '.', '.', '.', '.', '.'],
['.', spe, spe, '.', '.', '.'],
[spe, spe, spe, spe, '.', '.'],
[spe, spe, spe, spe, spe, '.'],
['.', spe, spe, spe, spe, spe],
[spe, spe, spe, spe, spe, '.'],
[spe, spe, spe, spe, '.', '.'],
['.', spe, spe, '.', '.', '.'],
['.', '.', '.', '.', '.', '.']]


for i in range(0, len(l[0])):
    row = ''
    for item in l:
        row += item[i]
    row = row * 2
    print(row)
```

**井字棋题**是本书目前为止较难的习题之一。本题有几个关键要素：既然要下棋，除了知道井字棋的规则之外，首先得**设计棋盘**，对于这样一个平面棋局，棋盘具有两个属性，一个是棋盘的位置或者说行子的位置，另一个就是棋盘上面的东西，对于井字棋来说就是这个位置上的符号是什么。既然有两个维度且二者之间有关联，那读者应该可以想到用*字典*对棋盘进行刻画。棋盘的位置有9个，所以我们需要9个键值对，初始化都是空的。

第二个关键要素是**下棋的用户**，首先让玩家分别输入名字，我们要保证用户名不重复，因此第二个用户若输入相同的名字则提示改名。为了保证用户轮流行棋，我们还需要判定用户上一轮是否已经行棋。同时我们还要给用户分配对应的符号，用户的相关属性和设定我们仍然用*字典*来实现。

第三个关键要素是*行棋过程*，主要是判定行棋位置。第一不能下重复位置，第二不能下非法位置。为了让棋手下棋更为直观，我们在行棋的每一步后都应该打印棋盘显示当前情况。

第四个关键要素是*棋局的判定*，主要是如何判断胜负手的问题。井字棋极易出现平局，其在数学上也可证明不用完棋的情况下某些棋局必为平局，本题对该判定方法不做要求，只需判定若棋盘走完还未决出胜负即为平局。剩下的赢棋方式可以统分为：*行获胜、列获胜、对角线获胜*三种情况。行列获胜可以通过定义行列列表，遍历每行（列）查询行（列）内行棋形状是否一致即可。由于只有两条对角线，因此对角线获胜利用列表内的相关位置进行判断即可。

```python 3
import random

  
Board = {
'A1': ' ',
'A2': ' ',
'A3': ' ',
'B1': ' ',
'B2': ' ',
'B3': ' ',
'C1': ' ',
'C2': ' ',
'C3': ' '
}

name1 = input("Please input your name: ")
name2 = input("Please input your name: ")

while name1 == name2:
    name2 = input("Your name was taken by another player, try another name: ")

player1 = {'name': name1, 'lastR': False, 'sp': 'X'}
player2 = {'name': name2, 'lastR': False, 'sp': 'O'}
players = [player1, player2]

not_end = True
first_round = True
while not_end:
    # show the board
    print(' ' + '1' + ' ' + '2' + ' ' + '3')
    print()
    
    print('A ' + Board["A1"] + '|' + Board["A2"] + '|' + Board["A3"])
    print(' -+-+-')
    print('B ' + Board["B1"] + '|' + Board["B2"] + '|' + Board["B3"])
    print(' -+-+-')
    print('C ' + Board["C1"] + '|' + Board["C2"] + '|' + Board["C3"])
    
    # Which player
    if first_round:
        player = random.choice(players)
        player['lastR'] = True
        first_round = False
    else:
        for p in players:
            if p['lastR'] and True:
                p['lastR'] = False
            else:
                player = p
                player['lastR'] = True
    
    # Chose Action
    print(f"--------------player {player['name']}'s Round--------------")
    
    while True:
        loc = input("select one action: A1-A3,B1-B3,C1-C3: ")
        if loc in Board.keys():
            if Board[loc] == ' ':
                Board[loc] = player['sp']
                break
            else:
                print("loc is is occupied")
                continue
        else:
            print("No such loc")
            continue
            
    # Check results
    rows = ['A', 'B', 'C']
    cols = ['1', '2', '3']
    
    # case 1 : one row
    for r in rows:
        if Board[r + '1'] == Board[r + '2'] == Board[r + '3'] != ' ':
            for p in players:
                if p['sp'] == Board[r + '1']:
                    print('=' * 10)
                    print(f"{p['name']} win")
                    not_end = False
    
    # case 2: one col
    for c in cols:
        if Board['A' + c] == Board['B' + c] == Board['C' + c] != ' ':
            for p in players:
                if p['sp'] == Board['A1']:
                    print('=' * 10)
                    print(f"{p['name']} win")
                    not_end = False
    
    # case 3: diagonal
    if Board['A1'] == Board['B2'] == Board['C3'] != ' ':
        for p in players:
            if p['sp'] == Board['A1']:
                print('=' * 10)
                print(f"{p['name']} win")
                not_end = False
    
    if Board['C1'] == Board['B2'] == Board['A3'] != ' ':
        for p in players:
            if p['sp'] == Board['A3']:
                print('=' * 10)
                print(f"{p['name']} win")
                not_end = False
    
    # case 4: no winer
    else:
        has_empty = False
        for v in Board.values():
            if v == ' ':
                has_empty = True
        if not has_empty:
            print('=' * 10)
            print("No winner")
            not_end = False


print(' ' + '1' + ' ' + '2' + ' ' + '3')
print()
print('A ' + Board["A1"] + '|' + Board["A2"] + '|' + Board["A3"])
print(' -+-+-')
print('B ' + Board["B1"] + '|' + Board["B2"] + '|' + Board["B3"])
print(' -+-+-')
print('C ' + Board["C1"] + '|' + Board["C2"] + '|' + Board["C3"])
```