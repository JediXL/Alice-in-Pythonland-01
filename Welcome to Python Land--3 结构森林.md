# 结构森林
![[Pasted image 20221007092409.png]]

## 布尔类型

上一章中我们已经介绍了两种变量类型，字符串型和数值型。在步入结构之森的伊始，我们要先对上一章中遗留的最后一种变量类型——布尔型加以说明。首先是布尔型的定义，变量的类型是通过赋值决定的，要定义布尔变量，则给相应变量赋布尔值。布尔值有且仅有两个值，真和假，即True和False。由于Python是大小写敏感的编程语言，因此要注意布尔值的首字母大写问题。

```python 3
a = False
b = True

print("a = ", a, type(a))
print("b = ", b, type(b))
```

### 布尔类型逻辑运算

虽然布尔值只有两个，但也可以进行运算操作，只是布尔值的常见运算是**逻辑运算**，也就是and和or运算，对应与运算和或运算。和计算机基础的真值表相对应，与运算（and）中两个变量都为真时结果为真，或运算（or）中两个变量都为假时结果为假。

```python 3
a = False
b = True

c = a and b
d = a or b

print("c = ", c)
print("d = ", d)
```

需要注意的是，由于现实场景中存在多层的逻辑判断结构，因此and和or这样的逻辑运算也可以进行级联操作。在Python布尔运算过程中，and的优先级高于or的优先级，依此可以得到一个快速判断级联逻辑运算结果的小技巧。在判断一个级联逻辑运算时，可以以第一个or为分界线，若or前半部分为真，则整个逻辑表达式为真。若or前为假，则再判断or后部分。

```python 3
a = True
b = True
c = False

d = a and b and c
e = a and b or c

print("d = ", d)
print("e = ", e)
```

### 布尔类型的转换

布尔类型也可以和字符串型、数值类型（整型、浮点型）进行相互转换，转换规则可以总结为*虚无为假，实体为真*，也可以总结为*非零为真，非空为真*。

```python 3
a = 5
b = "hello"
c = 3.2
d = 0
e = ""

print("bool(a): ", bool(a))
print("bool(b): ", bool(b))
print("bool(c): ", bool(c))
print("bool(d): ", bool(d))
print("bool(e): ", bool(e))
```

由于True和False对应的是两种情况，也可以将他们对应为计算机中的0、1两值，因此将布尔型转换为整型是对应的就是0和1两个整数。

```python 3
a = False
b = True

print(int(a))
print(int(b))
```

既然布尔型可以转换为整型，那么也可以利用布尔型做一些常见的数值操作，不论是布尔型的单独的数值操作还是和数值型的混合操作，都可以直接将布尔型看作0和1。

```python 3
a = False + 2
b = True + 6
c = True + True + True + False
d = True * 15 - False + 2 * True

print("a = ", a)
print("b = ", b)
print("c = ", c)
print("d = ", d)
```

### 布尔型的比较操作 

布尔型最为常见的功能是用于*比较后的输出*，因此在Python结构之森中起着重要的作用。在比较操作中最常见的两个符号是“\=\=”和“\!\=”，前者代表判断是否相等，后者代表判断是否不相等。

```python 3
sky = 'blue'
print(sky == 'blue') #是否等于

a = 3
print(a > 4)
print(a >= 4)

c = 5
print(c < 6)
print(c <= 9)

d = 8
print(d == 8)
print(d != 7) #不等于
```

## 分支结构（判断结构）

分支结构或者称之为判断结构是我们在结构之森中遇到的第一种结构类型。

### if...else...

if-else分支结构就像火车轨道，**带有布尔值的判断条件**就像是控制火车轨道的道岔控制器，本质上是通过*布尔值来控制程序的运行方向*，可以简单理解为*如果xxx，否则xxx*，如下示例则为判断输入的年龄是否大于18岁。

```python 3
age = eval(input("your age ? :"))

if age >= 18:
    print("hey, you are an adult.")
else:
    print("don't worry, take it slow.")
```

在这里有的读者会疑问，为什么不每行都顶格写？为什么有的语句前有空格？到底要空多少格？这就涉及到了Python中的**缩进**规则。

#### 缩进

![[Pasted image 20220925133132.png|400]]

Alice在结构之森中遇到了一只猫，她们产生了如下对话：

>“I hate this,” said Alice.
>“What?” said the Cat.
>“Every time, every time I say something, there is a ‘said Alice’ after my words,” said Alice.
>“Well， then, we can just remove it if you don’t like it,” said the Cat.
>
>**“Let’s try”**
 **“Let’s try ”**
 **“Who am I ? ”**
 **“Who is Speaking?”**
>
 >“Stop,” said Alice.
> “Ha~ I suppose it does not work.” said the Cat.
  “Yes, I can’t know which sentence belongs to me.” Said Alice.

Alice她不愿意⾃⼰每说⼀句话，都在后⾯加⼀个"said Alice"，所以笑脸猫就建议她说我们直接把"said Alice"去掉。然后发现⼤家分不清楚到底谁在说话了。于是笑脸猫出了个主意

>“Maybe I got an idea,” the Cat went on, “We add some 'spaces' before our sentence, and each sentence should be under the name it belongs to.”
>
Alice:
&nbsp;&nbsp;&nbsp;&nbsp;All right.
Cat:
&nbsp;&nbsp;&nbsp;&nbsp;Feel better now?
Alice:
&nbsp;&nbsp;&nbsp;&nbsp;Yes.
&nbsp;&nbsp;&nbsp;&nbsp;Much much better.
Cat：
&nbsp;&nbsp;&nbsp;&nbsp;Glad to hear that.

笑脸猫出了⼀个主意，她说每个人说的话都跟在自己的名字下面，并且*在前面加上空格*，其实加空格的原因就是为了区分目前这句话到底属于谁。而Python中就采取了这样的规则来应用缩进，本质上**Python 通过缩进来表示层级**，因此缩进相同，就说明处于同一层级。比如这段代码中的if和else都是顶格的，那么说明这二者是“平等”的，是处于同一层级的。print语句前都有缩进，代表了他们属于if或else分支中的操作。

```python 3
age = eval(input("your age ? :"))

if age >= 18:
    print("Hey, you are an adult.")
else:
    print("Don't worry, take it slow.")
```

那缩进量是多少呢？一般来说每一个层级的缩进是**4个空格或1个tab** （不同系统或不同编译器中1个tab不一定等于4个空格，需要读者注意）。在一般编译环境下，当你本行以“\:”结尾时敲下回车，在下一行会进行自动缩进。

现在武器库已足够强大，我们可以解决上一章遗留的猜数字问题了。

```python 3
import random

r = random.randint(1, 10)
is_right = False

while not is_right:
    guess = eval(input("you guess is :"))
    if guess < r:
        print("low")
    if guess > r:
        print("high")
    if guess == r:
        print("Bingo !!!")
        is_right = True
```

### if...if...if

在前述示例中，只需要判断用户是否成年，假设我们要在用户恰好18岁时给相应的祝福，在这种情况下，我们不仅需要判断用户是否成年，还需要判断用户年龄是否恰好等于18岁，前文if-else的结构只能判断一个条件两种情况，因此我们需要对原本的结构进行改进，即**当我们在实际场景中需要进行多条件判断时，我们可以连续使用if**

```python 3
age = 18

if age < 18:
    print("You are a child")

if age >= 18:
    print("You are an adult")

if age == 18:
    print("Congratulations")
```

现在让我们用一个简单的练习来熟悉一下这种多条件判断场景，在Python Land游荡时，Alice发现了一个隐藏的洞穴，打开洞穴的门需要三个条件：*用户等级大于26；拥有门的钥匙；用户角色为战士*。当用户无法打开这扇门时，我们也要提醒用户是因为什么原因无法获得宝藏。

```python 3
if level > 26:
    if has_key:
        if role == 'warrior':
            print("Greeting, great warrior")
        else:
            print("Only warrior")
    else:
        print("You need the key to open this door")
else:
    print("Your level is too low for this room")
```

读者可以根据以上程序判断以下四种情况会分别输出什么内容：

>Case 1: Level = 5；has_key = True；role =“warrior”
>Case 2: Level =27；has_key = False；role =“wizard”
>Case 3: Level =27；has_key = True；role =“wizard”
>Case 4: Level =27；has_key = True；role =“warrior


这个示例与上述示例稍有不同的是，几个if的层级并不相同，属于*嵌套关系*。

### if...elif...

要看elif如何使⽤，我们⾸先来找个场景。这个场景笔者很喜欢，笔者愿意称之为早餐难题。笔者⼤学刚毕业的时候，⼯作地点在⼀个园区。这个园区门口有一条很长的小巷。在冬天的早上，漫步在茫茫白雾中，摸着口袋中为数不多的预算，笔者经常需要纠结到底早餐吃什么。在这种情况下，就可以通过elif进行选择：

```python 3
budget = 12

if budget > 10:
    print("Eat noodle")

elif budget > 6:
    print("Eat pancake")

elif budget > 3:
    print("Eat steamed bun")

else:
    print("I'm not hungry")
```

有读者会怀疑以上的功能用之前的if不也能实现吗，为什么要使用elif呢？我们将上述代码换成if之后运行一下，来看有什么区别：

```python 3
budget = 12

if budget > 10:
    print("Eat noodle")

if budget > 6:
    print("Eat pancake")

if budget > 3:
    print("Eat steamed bun")

else:
    print("I'm not hungry")
```

当budget = 12时，如果使用elif结构，会输出：Eat noodle；如果使用if结构，会输出：Eat noodle Eat pancake Eat steamed bun。显然后者将所有满足的情况都输出了（并吃不下那么多早餐）。**读者可以将elif理解为做单选，一旦进入了某一个elif，则不会进入其他分支，反之每个if语句都会被判断**。

但是某些场景下if和elif时可以进行互通互换的。我们将刚才的探索宝藏问题换一种表达形式：

```python 3
if level > 26 and has_key and role == "warrior":
    print("Greeting, great warrior")

elif level <= 26:
    print("Your level is too low for this room")

elif not has_key:
    print("You need the key to open this door")

elif role != 'warrior'
    print("Only warrior")
```

虽然这个表达方式和上述示例实现的功能一致，但是前者锯齿感（缩进感）很强，会在阅读程序时造成困扰。同时在Python之禅中也有提示：*扁平胜于嵌套*，所以后者风格会提升代码的可读性，使⽤elif可以让我们代码更优美。如果一定要写具有“层次感”的代码，请注意*嵌套最好不要超过3层*。

我们再对之前的判断年龄问题进行回看，读者可以考虑示例是否存在漏洞。

```python 3
age = 18

if age < 18:
    print("You are a child")

if age > 18:
    print("You are an adult")

if age == 18:
    print("Congratulations")
```

```python 3
age = 18

if age < 18:
    print("You are a child")

elif age > 18:
    print("You are an adult")

elif age == 18:
    print("Congratulations")
```

这两段代码除去我们已经说明的if和elif的区别外，存在的最大漏洞是，如果当用户刻意输入一个负数时，仍然会输出“You are a child”，这种情况就显得不太合适。这里的本质问题是，在设计分支结构时*没有将所有可能的情况考虑完全*。

因此，在这里提醒读者们，在设计分支语句时应该*考虑“完备性”*，我们可以利用else来捕获这种可能存在的异常情况。

```python 3
age = 18

if 0< age < 18:
    print("You are a child")

elif age >= 18:
    print("You are an adult")

elif age == 18:
    print("Congratulations")

else:
    print("Age must be positive")
```

在Python中还可以利用if...else...构成**条件赋值语句**，具体形式如下：

```python 3
x = 5
y = 10
c = 'low' if x < y else 'high or equal'

print(c)
```

在这样的形式中，if...else...负责*条件*，\"=\"负责*赋值*。上述代码表示意思是当x<y时就给c赋值“low”，反之则赋值“high or equal”。这种表达形式将赋值和条件判断融为一行，看起来十分的简练高效，但同时也因为判断条件和赋值都被压缩，其实降低了代码的可读性。

那是否还有更新潮的方式能将赋值与条件判断融为一体么？各位读者先来尝试用if...else...编写一个示例：一个小餐馆需要一个简易的订餐系统，用户输入用餐人数，当用餐人数大于10时系统告知用户“抱歉，人数过多”否则输出“谢谢”。

```python 3
people_num = int(input("Please input:"))
if people_num > 10:
    print(f"Sorry, {people_num} is too much")
else:
    print("Thanks")
```

在这个示例中，先利用input进行输入并对people_num赋值，然后对people_num进行条件判断。在Python3.8版本及以上，发布了一种名为**海象操作符**的赋值表达式，英文名是*walrus operator*。它由冒号\":\"和\"=\"构成，形如\":=\"，就像海象的眼睛和獠牙向右旋转了90度而因此得名。海象操作符的作用也是**将赋值与条件判断合为一体**，使代码简洁明了。我们对刚才的示例进行改写，利用海象操作符完成相应代码：

```python 3
if (people_num := int(input("Please input:"))) > 10:
    print(f"Sorry, {people_num} is too much")
else:
    print("Thanks")
```

在上述代码中仍然是先对people_num赋值，然后对people_num进行条件判断。从功能上来讲，海象操作符的出现会大量减少重复的赋值语句，在合适的场景中使用海象操作符不仅可以提升可读性，更重要的是可以降低程序的复杂性，减少调用次数从而提升程序效率，这一点将在后续内容中有所体现。

## 循环结构

接下来要介绍一种新的结构，叫循环结构。之前提起过Python的创造者由于是Python剧团的狂热粉丝，所以给这门语言取名Python，同时Python剧团在喜剧界的地位就如同甲壳⾍乐队在⾳乐界的地位，那么在介绍循环结构之前，先请各位读者欣赏甲壳虫乐队的代表作之一《Hey Jude》。

初听此歌的读者可能很快就发现这首歌的规律性很强，好像一直在重复某一部分，更有甚者给这首歌画了一个所谓的流程图。而这首歌中就蕴含了我们需要解释的循环结构，当然其中也包括了我们已经学习过的分支结构。接下来我们就开始探索循环结构。

![[Pasted image 20221002110400.png|500]]

### While 循环

在循环结构中遇到的第一种结构是 *while* 结构，while在英语⾥有很多解释，在程序开发⾥，我们取它 *during the time that* 这样的释义，翻译成中文就是*当……时*。

在《Hey Jude》这首歌的结尾，大家一直还在唱，只是声音越来越小，这种结尾手法称之为 *Fade out*，营造了一种意犹未尽的感觉。但是在程序世界，只要想听，我们可以通过while循环让这首歌一直“唱”下去。

```python 3
# use while to print "hey jude"
i = 0
while i < 3:
    print("Hey jude")
    print("Don't make it bad")
    print("Take a sad song and make it better")
    print("Remember to let her into your heart")
    print("then you can start to make it better")
    print("better better better better waaaaaa")
    print("na na na na na na na na na")
    i += 1
    print("========= one more time =========")
```

利用变量i对while循环进行控制，我们就可以控制程序循环的次数，也就可以控制歌曲重复的次数。while循环的使用方法是：**在while后附加一个布尔值的条件，当该条件为真时，则执行循环内容，直到条件不满足时不进入循环。** 与此同时，写while循环时一定要注意：*程序是否会运行到条件不满足的时候。* 如果读者写出了while Ture或者while 1这样的代码，则条件时刻满足，程序会一直执行下去，直到你或者你的电脑受不了的时候为止。

所以在上述情况下，如果确实需要用while Ture这样的判断方式，那就一定要配备两种让程序停车的办法：**break和continue**。

```python 3
i = 0
while True:
    print("Hey jude ... ")
    i += 1
    if i >= 3:
        break

————————————————————————————
Hey jude ... 
Hey jude ... 
Hey jude ...
```

```python 3
i = 0
while True:
    i += 1
    if i % 2 == 0:
        continue
    if i > 10:
        break
    print(f"Hey jude ... {i}")

————————————————————————————
Hey jude ... 1 
Hey jude ... 3 
Hey jude ... 5 
Hey jude ... 7 
Hey jude ... 9
```

所以continue和break都可以让程序跳出循环。但是这两种方法有区别，continue类似刹⻋，踩⼀下这次循环就不会继续，但是⼜会有新的循环出现。break更像是直接熄⽕，完全退出当前的循环。这两个重要的关键词在while True这种结构中（需要在循环内部控制循环走向）起关键作用，他们可以控制你的循环什么时候不往下执行（或继续往下执行），也可以控制你的循环什么时候退出。

同时while循环结构也可以进行嵌套操作。我们可以实现每重复一遍歌词就把“na na na na na na na na na”循环3遍。

```python 3
i = 0
while i < 3:
    j = 0
    print("Hey jude ....")
    while j < 3:
        print(f"na na na na na na na na na {j}")
        j += 1
    i += 1
    print(f"========= {i}=========")
```

在while循环的过程中读者会许会发现条件判断和赋值尤为重要，尤其是涉及**while循环内部对控制变量的赋值变化**，之前我们解锁过的海象操作符就可以大展身手了。我们以上文的利用while循环打印hey jude这首歌为示例，看看二者的有哪些区别。

```python 3
# use while to print "hey jude"
i = 0
while i < 3:
    print("Hey jude")
    print("Don't make it bad")
    print("Take a sad song and make it better")
    print("Remember to let her into your heart")
    print("then you can start to make it better")
    print("better better better better waaaaaa")
    print("na na na na na na na na na")
    i += 1
    print("========= one more time =========")
```

```python 3
i = 0

while (i := i + 1) < 4:
    print("Hey jude")
    print("Don't make it bad")
    print("Take a sad song and make it better")
    print("Remember to let her into your heart")
    print("then you can start to make it better")
    print("better better better better waaaaaa")
    print("na na na na na na na na na")
    print("========= one more time =========")
```

读者们可以发现，我们通过海象操作符的方法将while循环内部的i += 1“转移”到了条件判断处，这样的操作使得while内部不再赋值，提升了代码的统一性和可读性，同时由于代码过程中减少了重复赋值的语句，也提升了代码的效率。

需要注意的是由于赋值顺序有所改变，判断条件也要相应改变。在前者中*先判断再赋值*（i < 3, i += 1），所以输出三遍的条件是（i < 3，实际循环过程中i分别等于0,1,2），而后者利用海象操作符是*先赋值再判断*，所以所以输出三遍的条件是（i < 4，实际循环过程中i分别等于1,2,3）。这也是在实际设计循环结构是需要注意的细节问题之一。

有了以上分支、循环结构的加持，以及在*新手沙滩*和*数据湍流*所获取的趁手武器，读者们不妨尝试利用现有的武器库设计一个**文字冒险类**游戏来检验自己的阶段性学习成果。**游戏描述如下**：Alice在Python Land中探险，遇到了一只怪物，然后会展开一系列互动。Alice首先选择自⼰的⾏动（由玩家自己输入），然后怪物随机选择⾃⼰的⾏动。其中Alice⾎量100，攻击力15，怪物⾎量150，攻击⼒20。当Alice或者怪物其中⼀个⾎量<=0的时候，游戏结束。如果Alice逃跑成功，游戏也结束。

![[Pasted image 20221002113541.png|500]]

```python 3
import random

Alice_max_health = 100
Alice_health = 100
Alice_power = 15
Alice_Rest = 40
Alice_run_rate = 0.3

Monster_health = 150
Monster_power = 20
is_Monster_guard = False

Alice_emoji = '👧'
Monster_emoji = '👹'
sword_emoji = '🗡️'
run_emoji = '🏃‍♀️'
guard_emoji = '🛡️'
rest_emoji = '💊'

  
while Monster_health > 0 and Alice_health > 0:
    print("=============== Fighting ===============")
    print(f"{Alice_emoji}: {Alice_health} | {Monster_emoji}: {Monster_health}")
    print("========================================")
    
    alice_action = input("chose Alice's action: Attack | Rest | Run : ")
    is_Monster_guard = False
    monster_action = random.choice(["Attack", "Guard"])
    
    if alice_action == "Attack":
        if monster_action == "Guard":
            is_Monster_guard = True
            Monster_health = Monster_health - Alice_power + is_Monster_guard * Alice_power / 2
        else:
            Monster_health = Monster_health - Alice_power
        print(f"{Alice_emoji} {sword_emoji} ---> Monster health : {Monster_health}")
    elif alice_action == "Rest":
        Alice_health = min(Alice_max_health, Alice_health + Alice_Rest)
        print(f"{Alice_emoji} {rest_emoji} ---> Alice health: {Alice_health}")
    elif alice_action == "Run":
        dice = random.random()
        if dice <= Alice_run_rate:
            print(f"{Alice_emoji} {run_emoji}. dice:{dice}")
            break
        else:
            print(f"{run_emoji} Failed. dice:{dice}")
    else:
        print("only giving actions can be chosed")
        continue
    
    print(f"---Monster choses to {monster_action}---")
    if monster_action == "Attack":
        Alice_health -= Monster_power
        print(f"{Monster_emoji} {sword_emoji} ---> Alice_health: {Alice_health}.")
    else:
        print(f"{Monster_emoji} {guard_emoji}")

if Alice_health > 0:
    print("Congratulation Alice !!!")
else:
    print("Oh, on. Monster wins the battle.")
```


## 练习

### 鸡兔同笼问题

请编写一个程序，用户在同一行输入两个整数，代表头和脚的数量，编程计算笼中各有多少只鸡和兔。如无解则输出“Data Error！”

#### 输入格式
输入为一行，以空格分割的两个整数h f,分别代表鸡兔的总头数和总脚数

#### 输出格式
使用输入值进行计算，如有解，则输出：有m只鸡，n只兔；如无解则输出“Data Error！”

#### 示例1
>输入: 35 94
 输出：有23只鸡，12只兔

#### 示例2
>输入: -24 12
 输出：Data Error！

#### 示例3
>输入: 12 35
 输出：Data Error！

### 个税计算问题

请按照累进个人所得税税率表和所得税计算公式，编写个人所得税计算器，用户输入应发工资薪金所得、五险一金金额和个税免征额，输出应缴税款和实发工资，结果保留小数点后2位，当输入应发工资小于或等于0时输出"Error"。

所得税计算公式：
应纳税额 = （应发工资薪金所得 - 五险一金金额 - 个税免征额）\* 适用税率 - 速算扣除数
实发工资 = 应发工资薪金所得 - 五险一金金额 - 应纳税额

|    全月应纳税所得额    | 税率 | 速算扣除数 |
|:----------------------:|:----:|:----------:|
|      不超过3000元      |  3%  |     0      |
| 超过3000至12000元部分  | 10%  |    210     |
| 超过12000至25000元部分 | 20%  |    1410    |
| 超过25000至35000元部分 | 25%  |    2660    |
| 超过35000至55000元部分 | 30%  |    4410    |
| 超过55000至80000元部分 | 35%  |    7160    |
|    超过80000元部分     | 45%  |   15160    |

要求使用以下输入语句：

```python 3
salary = float(input())
five_one_insuance_fund = float(input())
exemption = float(input())
```

#### 输入格式
输入为三行，每一行都是一个浮点数，分别代表应发工资、五险一金、个税起征点

#### 输出格式
输出为一行，形如：应缴税款490.00元，实发工资11510.00元

#### 示例
>输入: 
>5400
>412
>5000
>输出：
>应缴税款0.00元，实发工资4988.00元


## 练习解析

**对于鸡兔同笼问题**，笔者提供三种方法，分别对应了三种思路供读者品味。

第一种方法是**假设法**，是一种基于推理的解法。我们假设笼⼦⾥所有的动物都是兔⼦，那*应该有*的脚的数量就是头的数量x4，用它减去实际脚的数量，就是多出来的脚的数量，而这些多出来的脚都来自于本不应该是兔子的鸡，因此将它除以2之后，就能得到鸡的数量。但是我们需要对这个数进行判断，判断它的合理性，主要是两种情况：这个数量是否是负数；这个数量是否非整数。

第二种方法是**试验法**，是一种较为直观的解法。我们先假设只有⼀只鸡，其他的都是兔⼦，然后计算这种情况的脚数量加起来是否正确，如果不对则假设2只鸡，直到所有动物全是鸡的情况。在这种情况下不需要判断数量是否合理，因为挨个试验的数量都是大于零的整数。

第三种方法是**方程法**，是一种利用数学思维和工具的解法。在这个方法中我们需要利用numpy包来求解线性方程，同时使用math.modf方法来分离整数和小数部分。

看起来第二种方法考虑地更简单，显得更为直观，但是第二种方法需要挨个去试验，程序运行的复杂度完全取决于输入的数字大小。因此，在实际运行场景中，考虑程序运行的效率时第一种利用推理的方法是显然优于第二种的，当然第三种方法的实际效率也比较优秀。

```python 3
# solution 1 复杂度O(1)
heads, feet = map(int, input("请输入头和脚的数量,以逗号分隔:").split(','))

ChickenNum = (heads * 4 - feet) / 2
RabbitNum = heads - ChickenNum

is_ChickenReasonable = ChickenNum >= 0 and ChickenNum == int(ChickenNum)
is_RabbitReasonable = RabbitNum >= 0 and RabbitNum == int(RabbitNum)

if is_ChickenReasonable and is_RabbitReasonable:
    print("有{}只鸡,{}只兔".format(int(ChickenNum), int(RabbitNum)))
else:
    print("Data Error!")


# solution 2 复杂度O(heads)

heads, feet = map(int, input("请输入头和脚的数量,以逗号分隔:").split(','))
has_solution = False

for ChickenNum in range(0, heads + 1): 
    RabbitNum = heads - ChickenNum
        if ChickenNum * 2 + RabbitNum * 4 == feet:
            print("有{}只鸡,{}只兔".format(int(ChickenNum), int(RabbitNum)))
            has_solution = True
            break
if not has_solution:
    print("Data Error!")


# solution 3 复杂度O(1)

import numpy as np
import math

heads, feet = map(int, input("请输入头和脚的数量,以逗号分隔:").split(','))
mat_feet_head = np.mat('1, 1; 2, 4')
inputs = str(heads) + ',' + str(feet)

mat_inputs = np.mat(inputs).T # 行变列
res = np.linalg.solve(mat_feet_head, mat_inputs)
ChickenNum = res[0,0]
RabbitNum = res[1,0]

ChickenDecimal, ChickenNum = math.modf(ChickenNum)
RabbitDecimal, RabbitNum = math.modf(RabbitNum)
is_not_reasonabe = ChickenDecimal != 0 or RabbitDecimal != 0 or ChickenNum < 0 or RabbitNum < 0

if is_not_reasonabe:
    print("Data Error!")
else:
    print("有{}只鸡,{}只兔".format(int(ChickenNum), int(RabbitNum)))
```

**对于个税计算问题**，主要考察的是多条件判断时能否正确应用分支结构，需要注意的是*判断哪个指标在表中所列区间*

```python 3
salary = float(input())
five_one_insuance_fund = float(input())
exemption = float(input())

tax = 0
real_salary = 0
exceed = salary - five_one_insuance_fund - exemption

if 0 < exceed < 3000:
    tax = exceed * 0.03 - 0
elif 3000 <= exceed < 12000:
    tax = exceed * 0.10 - 210
elif 12000 <= exceed < 25000:
    tax = exceed * 0.20 - 1410
elif 25000 <= exceed < 35000:
    tax = exceed * 0.25 - 2660
elif 35000 <= exceed < 55000:
    tax = exceed * 0.30 - 4410
elif 55000 <= exceed < 80000:
    tax = exceed * 0.35 - 7160
elif exceed >= 80000:
    tax = exceed * 0.45 - 15160

real_salary = salary - five_one_insuance_fund - tax
if salary <= 0:
    print('Error')
else:
    print("应缴纳税款{:.2f}, 实发工资{:.2f}元.".format(tax,real_salary))
```
