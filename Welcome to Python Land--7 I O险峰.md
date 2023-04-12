# I/O险峰

![[Pasted image 20221115101942.png]]

探索完了对象荒原后，Alice面前出现了一座陡峭的山峰。

在学完了Python的基础语法和基础理念后，我们能想到最实用的就是利用Python做点什么，在漫天的Python广告中也经常提到“用Python处理文件，让同事对你刮目相看”，而本章所要翻越的高峰就是帮助你利用Python处理那些无聊的工作。

所谓I/O险峰，I指的是Input，我们在前面章节已经体验过Input函数，这是输入的一种。O指的是Output，目前最常用的output就是print。而在实际工作中，I/O大部分对应的是文件的读取和写入。本书之前也提到过，Python对于很多行业而言，其最大的用途就是数据处理和分析能力，而这些源数据往往储存在txt、xls、cls等文件中。因此，既然要利用Python处理这些无聊的工作，绕不开的就是利用Python读写文件。

## 文件路径

要对文件进行读写还有一个前提是：*知道文件在哪里*，要掌握这个本领就要学习**文件路径**这个概念，文件路径就是一个文件的位置。在日常工作中，各位读者所接触到的最常见的文件路径表现形式，可能是安装文件时通过节点选择或者图像化的方式来描述的。

![[Pasted image 20221121204739.png|300]]

我们也可以通过以“路径”的方式展示文件位置，我们把具体路径完全写出来，这种表现方式叫做**绝对路径**。绝对路径的描述方式可以类比我们日常购物的快递地址，这是一个从大到小的具体位置：中国重庆市xx区xx街道xx小区xx栋。上述图片中展示的路径就是：

```python 3
C:\Documents\file1.txt
C:\Documents\file2.txt
```

另外还有一种路径的表现形式叫做**相对路径**，相对路径类似于相对距离，当然前提是我们需要一个*参考系*，我们利用相对路径来*描述其他文件或文件夹和参考坐标之间的关系*。这是一种关系型描述，这个表达方式在日常生活中也经常用到，例如我对门，我楼上，我楼下这种表示。

![[Pasted image 20221121205104.png|300]]

具体来说，**.\\表示的是自身文件夹下**（当前文件夹为Documents），如：.\\file1.txt。**..\\表示的是父文件夹下（上级路径下）**，如：..\\win32。

在日常工作中笔者更推荐使用**相对路径**，绝对路径相当于把位置写固定了，在协同工作时，有可能存放文件的路径是有差异的，如果将文件位置写固定，协同者可能存在无法读取的情况。

在Python中我们通过字符串的方式来表示路径，当然如下的表示方式是绝对路径的表示方式：

```python 3
path = "C:\\Windows"
```

在Python中也可以利用相关方法获取当前路径，这里所指的当前路径指的是运行当前Python文件的所在路径。首先我们导入os这个包，这个包提供了Python与操作系统进行交互的接口，包含了丰富的处理文件和目录方法。

```python 3
import os

os.getcwd() # 获取当前路径
```

前文提示过不同的系统路径的描述方式不同，在Mac系统下可能是/Documents/test.txt，而在Win系统下就是\\Documents\\test.txt，这种情况下不论使用相对路径还是绝对路径都有可能报错，我们可以用os中提供的方法来避免这种意外情况。

```python 3
import os 

path_workspace = os.path.join('Users','teacher','Documents','Ing','Teaching', 'Code-for-Teaching', 'exp_files') # 根据系统，获取正确的路径

print(path_workspace)
```

我们利用os.path.join方法，把需要添加的路径节点告诉Python，他会根据当前系统自动组合路径。我们还可以利用os.path.abspath方法获取和添加*绝对路径*，同时就可以利用os.path.relpath将括号内的绝对路径转换为相对路径。

```python 3
print("1: ", os.path.abspath('.'))
print("2: ", os.path.abspath('./exp_files'))

print("3: ", os.path.relpath('/Users/ABC/Documents/file1.txt'))
```

在传统操作系统中，我们可以通过“点击右键-新建文件夹”的方式新建文件夹，在Python中我们也可以创建文件夹，当然就不能用右键的方式了，在创建方式的选择上同样可以选择相对路径创建方式和绝对路径创建方式：

```python 3
path_new_dir_1 = os.path.join(os.getcwd(), 'exp_files', 'new_dir_1')

path_new_dir_2 = '/Users/ABC/Documents/new_dir_2'

os.makedirs(path_new_dir_1)
os.makedirs(path_new_dir_2)
```

第一种方法我们通过os.getcwd获取当前路径，然后通过添加节点的方式新建路径，第二种方式利用绝对路径指定了相应路径。但是上述代码存在隐患。潜在的问题是，如果是从0到1，也就是说这个文件夹之前没有那代码无误，但是如果已经存在这个文件夹，代码就会报错了。我们可以利用os.path.exists方法来判断可以判断该文件夹是不是已经存在了：

```python 3
path_new_dir_1 = os.path.join(os.getcwd(), 'exp_files', 'new_dir_1')

path_new_dir_2 = '/Users/ABC/Documents/new_dir_2'

if not os.path.exists(path_new_dir_1) and not os.path.exists(path_new_dir_2):
    os.makedirs(path_new_dir_1)
    os.makedirs(path_new_dir_2)
else:
    print("path already exits")
```

同时os中的isdir和isfile方法还可以判断我们的目标是否是一个文件夹或文件：

```python 3
print(os.path.isdir(path_new_dir_1))
print(os.path.isfile(path_new_dir_1))
```

这种方法的引入会避免由于文件夹和文件同名造成的误操作。


## 文件读写

要对指定文件进行读写，首先要获取文件路径，然后可以通过open方法打开文件进行**读取**：

```python 3
path_file_1 = os.path.join(os.getcwd(), 'exp_files', 'file1.txt')

file_1 = open(path_file_1)
file_1_content = file1.read()
file_1_content_line = file_1.readlines()

print(file_1_content)
print(file_1_content_line[0])
```

在上述代码中我们展示了两种读取方式，一种是整体读取，使用read方法，一种是逐行读取，使用readlines方法。读取完成后可以对相关文件进行**写入**，通过write方法即可实现写入。

```python 3
path_file_2 = os.path.join(os.getcwd(), 'exp_files', 'file2.txt')

file_2 = open(path_file_2, 'w')
file_2.write("Hello ! I'm Alice \n")

file_2.close()

file_2 = open(path_file_2, 'w')
file_2.write("Where am I ? \n")

file_2.close()
```

读者执行上述代码后可能会发现结果和预期不符，其中奥妙在于open中的'w'，这指的是在打开文件时执行**新建只写**任务，因此每次打开都会重新写入，每一次write都是重写，因此最终的结果只有最后一次的写入结果。我们可以通过改变文件的打开方式来避免这种问题。

```python 3
path_file_2 = os.path.join(os.getcwd(), 'exp_files', 'file2.txt')

file_2 = open(path_file_2, 'w')
file_2.write("Hello ! I'm Alice \n")

file_2.close()

file_2 = open(path_file_2, 'a')
file_2.write("Where am I ? \n")

file_2.close()
```

在这里，open中的'a'表示的是以**附加写**方式打开，可以理解为在现有文件后添加新内容。需要强调的是为了规范操作，在对文件进行写入操作后应该及时的使用close方法关闭文件。

#### 异常处理

笔者曾经长时间依靠摩托车通勤，每天大概往返36公里。在这段时间里，笔者多次修理摩托车，读者们可以猜测下修理最多的部件是什么？可能大部分读者会猜测刹车盘、车灯等部件，实际上修理最多的部件是脚撑。很多时候笔者上车发动一气呵成，直到转弯的时候，听到咔的一声，我就知道又要修理脚撑了。

作为摩托车设计者来说，摩托车的设计有问题么？显然是没有的，这是用户的个人操作问题，但是确实带来的用户体验并不好。

在那之后，笔者有次去海边旅游租了一辆摩托车，某日浏览完景色后准备出发，此时发现车子无法启动。最悲惨的是此时的位置距离租车地已有几十公里了。我脑子中已经浮现出推车回去的惨状。这时候有个帅哥过来问我是不是车坏了，我坦然承认了。帅哥说你发动给我看看，我一通操作后，帅哥提示我你应该先把脚撑收起来才能发动。我验证了之后果然车子顺利启动，第一时间我感觉到十分羞愧。第二反应是这个摩托车设计得太科学了。

在设计程序的过程中，或许我们的程序本身没有bug，但是可能依然会给用户带来不好的体验。在多年教学过程中，笔者也发现不论这个错误多么微不足道，只要弹出报错信息，同学们就十分慌张。

以上文提及选择路径打开文件为例，经常路径输错就会出现系统报错信息，而对于没有编程知识的用户来说，第一反应就是程序崩溃了不知所措，更不用说去阅读报错信息而修改了。作为设计程序的人，对于这种**可预见的错误**，我们可以不让程序崩溃，给用户一定的提示，这时的用户体验就会大大提升。具体怎样来实现呢？

要对可能的错误进行捕获我们就要利用try语句，具体结构如下：

![[Pasted image 20221203153208.png|300]]

整个结构由try和except构成，结构逻辑和分支结构类似。try层级下写*可能会出错的操作*；except后紧跟*预计会出现的错误*，在该层级下写*如果出错了怎么办*。以打开某文件为例，最容易出错的部分就是*打开这个文件*，出错的错误最常见的是*路径错误导致的文件找不到*，如果出错了我们要提醒用户*检查路径信息*，因此代码如下：

```python 3
path_file_try = os.path.join(os.getcwd(), 'exp_file', 'file_try.txt')

try:
    file_try = open(path_file_try, 'w')
except FileNotFoundError:
    print("-- Please check your path ---")
```

这时候我们就不会出现恐怖的报错信息，而是温馨提醒用户检查路径。但是需要注意的是上述代码中“**FileNotFoundError**”这一部分不是瞎编乱造的，而是的的确确存在的系统报错信息，当读者不知道要捕获的错误信息或不知道预计出现的报错信息到底是什么的时候，可以亲身实践，看具体的报错信息填入相关位置即可，如下所示红框即为*系统报错信息*。

![[Pasted image 20221203155034.png|300]]

从逻辑层面上我们还可以对上述结构进行补充，我们预想可能会出错，出错之后需要怎么办，但是如果没错呢？所以我们用else进行补充，else层级下写*如果没错则做什么*，具体结构如下：

![[Pasted image 20221122104937.png|300]]

仍以上例，若路径没错正常打开了文件，则向文件内写入Nice try后关闭文件。

```python 3
path_file_try = os.path.join(os.getcwd(), 'exp_file', 'file_try.txt')

try:
    file_try = open(path_file_try, 'w')
except FileNotFoundError:
    print("-- Please check your path ---")
else:
    file_try.write("Nice try \n")
    file_try.close()
```

在有的场景下，不管是否报错，程序如何运行我们都应该给用户一个提示，我们可以在finally层级下写*不管错没错最后做什么*。

![[Pasted image 20221203155343.png|300]]

仍以上例，最终使用finally提醒用户一切妥当。

```python 3
path_file_try = os.path.join(os.getcwd(), 'exp_file', 'file_try.txt')

try:
    file_try = open(path_file_try, 'w')
except FileNotFoundError:
    print("-- Please check your path ---")
else:
    file_try.write("Nice try \n")
    file_try.close()
finally:
    print("==== All Done ====")
```

### Excel读写操作

上文多次提及Python有较强的数据分析和处理能力，而在现实应用场景中很多数据都存储在在Excel文件中，我们需要把数据先拉取到Python文件中才能进一步处理。这里我们使用openpyxl包来对相关excel文件进行载入，需要说明的是实现打开和读取excel文件的包有很多，我们采取较为常用的openpyxl包。

```python 3
import openpyxl
```

需要做事先说明的是对excel文件中的数据进行定位时有几个关键维度。第一个维度是excel中有多个*表单*，称之为*sheet*。另外一个维度就是表单中的*单元格*，称之为*cell*，对于单元格的描述可以用excel中坐标描述法，比如A3、B5等，也可通过指定行列的方式进行描述。

```python 3
import openpyxl
  
book_path = os.path.join(os.getcwd(), 'exp_files', 'book.xlsx')
book = openpyxl.load_workbook(book_path)
print(book.sheetnames)
```

上述代码就展示了如何打开一个excel文件，利用openpyxl中的load_workbook方法打开相应文件，利用sheetnames方法查询该文件内的表单名。在打开了一个表单后就可以对单元格进行操作，如上所述有两种操作方式，一种按照坐标，一种按照行列的方式。

```python 3
sheet = book['Sheet1']

print(sheet['A2'].value)
print(sheet['B2'].value)
print(sheet.cell(row=1, column=1).value)
```

当然就可以通过for遍历的方式打印某一个区域的所有单元格。

```python 3
data = tuple(sheet['A2':'B7'])

for row in data:
    for cell in row:
        print(cell.coordinate, cell.value)
    print("--- Row ---")
```

首先读者可以回顾思考此处是用什么容器装了excel中的数据，为什么选择这种容器？在这里我们选了元组来装excel数据，原因是元组内的数据不会被修改，这有利于对原始数据进行保护。coordinate方法显示单元格的坐标，value方法显示单元格内容。

倘若单元格中的数据是有关联的，我们也可以用字典的方式将他们串联起来，以周SP500价格为例：

![[Pasted image 20221203170724.png|300]]

```python 3
data = tuple(sheet['A2':'B7'])

data_raw = {}
for week, price in data:
    data_raw[week.value] = price.value
print(data_raw)
```

以上我们就利用Python读取了excel中的相关数据，接下来要进行相关处理，要进行数据处理离不开著名的pandas包，这里import A as B的方式就是以B代替A在下文的代码中出现，而将pandas缩写为pd属于“国际惯例”。

```python 3
import pandas as pd
```

我们利用pandas将刚才的字典型数据转换为pandas自带的序列型。序列型中首先导入了数据，随后将这个序列命名为“S&P 500”。

```python 3
import pandas as pd

week_price = pd.Series(data_raw, name='S&P 500')
week_price[3]
```

对于一个pandas序列型数据，有三个主要组成部分：名字（可选的）、索引（index）和值（value），需要注意的是，**这里的索引从1开始**。可以对序列型数据进行切片操作也可以利用索引直接取值。

接着我们就要对数据进行分析，最简单的就是**数据筛选**。假如我们把周价格大于4000的打印出来，把大于中位数的周价格打印出来，这种处理方式称之为“遮罩”（mask）处理方式。可以搞一个遮罩让想展示的展示，不想展示的隐藏，下图就彰显了对应关系，在遮罩中的value是用布尔值表示的。

![[Pasted image 20221203172536.png|400]]

```python 3
print(week_price[week_price > 4000])
print("========================")
print(week_price[week_price > week_price.median()])
```

但是实际工作数据中很有可能出现*数据缺失或不合规*的情况，这种数据类型一般为NaN，在进行数据分析前也要果断的将这些数据抛弃掉。

```python 3
week_price = week_price.dropna()
```

满足用户的基本需求后，我们不能直接将Python程序交付用户，而是要将处理后的数据重新写入excel文件中然后交付用户。

```python 3
book = openpyxl.load_workbook(book_path)
sheet = book['Sheet3']
sheet['A1'] = 'week'
sheet['B1'] = 'price'

for i in range (2, len(week_price.index) + 1):
    pos_a = 'A' + str(i)
    pos_b = 'B' + str(i)
    index = list(week_price.index)[i - 2]
    sheet[pos_a] = index
    sheet[pos_b] = week_price[list(week_price.index)[i - 2]]

book.save("./exp_files/resluts.xlsx")
```

在写入过程中我们打开文件后新建一个表单，然后写入表头，根据坐标可以将数据对应写入。当然读者们也可以考虑如果保存路径错了怎么办？当然可以使用try、except方法进行改进。最后对文件进行保存。

### 数据可视化

在大部分工作场景中，不仅需要对数据进行分析，而且大部分需求要求对数据和数据分析结果进行直观展示。这也就是常说的**数据可视化**操作，通过这样的操作也可以使别人更容易理解我们的数据分析结果。

如同pandas在数据分析中的作用，数据可视化中最常用的包是matplotlib，我们为它内置方法pyplot取一个小名plt，当然这也是约定俗成的。与pandas相同，这不是一个内在包，需要单独进行安装。 

```python 3
import matplotlib.pyplot as plt
```

在对数据进行分析处理时，numpy包也不可或缺，尤其是做多维数据处理和矩阵运算。

```python 3
import numpy as np
```

要进行数据可视化，我们首先得有需要绘制的数据。在这里我们利用numpy中的random方法随机产生10个数作为需要绘制的数据。

```python 3
data = np.random.random(10)
print(data)

plt.plot(data)
plt.show()
```

![[Pasted image 20221203174616.png|300]]

plot即为最常用的画图方法，意味着**将y与x绘制线条与（或）标记**，可见默认的是*蓝色折线*图。一般来说，plot有三个参数：**横轴、纵轴和格式化**，在上述数据中，x轴为数据的索引，y为具体的数值，也可以单独指定x和y分别为什么。格式化可以对绘图样式进行定制，一般由三部分构成：**颜色、标记、连线样式**。

```python 3
data_x = np.arange(10)
data_y = np.random.random(10)

print(data_x, data_y)
plt.plot(data_x, data_y, 'bo-')
plt.show()
```

一般来说plot在上述代码中，我们指定x为0到9，10个数字，y为随机生成的10个数字，此处的format为“bo-”，意味着“**b**lue colored d**o**ts with solid line (**-**)”，所以展示出来的是*蓝色线图，数据点标记为小圆点*。

![[Pasted image 20221203175438.png|300]]

当只指定标记样式而不指定线段样式时，就可以利用plot绘制散点图，其中rD代表red、Diamond。

```python 3
data_x = np.arange(10)
data_y = np.random.random(10)

print(data_x, data_y)
plt.plot(data_x, data_y, 'rD') 
plt.show()
```

![[Pasted image 20221203175615.png|300]]

在实际应用场景中，不光需要对数据进行可视化处理，同时需要利用可视化对数据进行对比，因此有在一张图上画多组数据的需求。当对数据进行对比时，数据一定有共同点，我们假设两组数据共用x轴，调用两次plot绘制两组数据，且两组数据的表现形式应给予区分。一组为蓝色圆点直线，一组为绿色宝石虚线。

```python 3
data_x = np.arange(10)
data_y1 = np.random.random(10)
data_y2 = np.random.random(10)

plt.plot(data_x, data_y1, 'bo-')
plt.plot(data_x, data_y2, 'gD--')
plt.show()
```

![[Pasted image 20221203175931.png|300]]

为了增强数据的可读性，在做数据可视化时还应对数据、x轴、y轴进行命名，同时也要告诉读者该图表示的是什么。下述代码中*xlabel*和*ylabel*分别为坐标轴的名称，*title*为图的名称，plot中的*label*代表数据的标签，*legend*即为绘图后图例的位置，此处的loc='best'意味着自动选择最佳位置放置图例。

```python 3
data_x = np.arange(10)
data_y1 = np.random.random(10)
data_y2 = np.random.random(10)

plt.plot(data_x, data_y1, 'bo-', label='Blue')
plt.plot(data_x, data_y2, 'gD--', label='Green')
plt.xlabel("X")
plt.ylabel("Y")
plt.title("Fig 1")
plt.legend(loc='best')
plt.show()
```

![[Pasted image 20221203180242.png|300]]

读者还可以利用figsize自定义画幅的大小，这个大小即为图片的原始比例。

```python 3
plt.figure(figsize=(10, 6)) # width = 10, height = 6
```

![[Pasted image 20221129113601.png|400]]

我们利用plot画的图组成部分有两个独立的坐标轴Axis，两个坐标轴统称为Axes，整个图为Figure。前文我们将多组数据放在了同一张图中进行对比，但是当数据过多时密密麻麻不利于对比。同时，上文的数据具有一个共同部分，即共用x轴，当我们有多套坐标轴进行对比上述方法就不太方便了，这时我们需要利用**子图绘制**实现上述功能。

```python 3
data_x = np.arange(10)
data_y1 = np.random.random(10)
data_y2 = np.random.random(10)

fig, (ax1, ax2) = plt.subplots(1, 2, figsize=(10,4), sharey=True, dpi=300) 

# draw
ax1.plot(data_x, data_y1, 'bo-', label='Blue')
ax2.plot(data_x, data_y2, 'gD--', label='Green')

ax1.set_title("Blue")
ax2.set_title("Green")

ax1.set_xlabel("X")
ax2.set_xlabel("X")

ax1.set_ylabel("Y")
ax2.set_ylabel("Y")

plt.show()
```

我们将一个figure拆分为两个子图，subplots方法中的前两个参数(1,2)代表的是子图的构型为*1行2列*，sharey=True代表*共用y轴的坐标刻度*，dpi代表了*单位面积的像素点*，数值越大图像越清晰。同时利用上文提到的方法对图像进行了标注和解释。

![[Pasted image 20221203181308.png|300]]

除了上文提及的画**散点图**的方式，matplotlib中有专门的绘制散点图方式，该方法为scatter。scatter的参数除了输入数据外，s代表*点的大小*，此处s=data_y\*1000意味着数据越大点的大小越大，c表示*颜色*，alpha表示*透明度*，此处alpha=data_y意味着数据越大颜色越深。

```python 3
data_x = np.arange(100)
data_y = np.random.random(100)

plt.figure(figsize=(10, 6), dpi=300) 
plt.scatter(data_x, data_y, s=data_y*1000, c='green', alpha=data_y)
```

![[Pasted image 20221203181704.png|300]]

当然还可以更专业一点，对数据颜色进行更深入的设置。为了将数据控制在一个范围内，我们首先可以利用Normalize方法对数据进行标准化处理。除了使用透明度和大小来区分数据，可以引入颜色区分数据，为颜色c赋样本对应的标准化值（0到1之间），此处的cmap可以理解为一个*调色盘*，c得到数值后就可以去调色盘上找对应的颜色。同时使用colorbar方法将颜色对应数据的图例进行展示。

```python 3
data_x = np.arange(100)
data_y = np.random.random(100)
cmap = plt.get_cmap('rainbow')
plt.figure(figsize=(10, 6), dpi=300)

norm = plt.Normalize(vmin=min(data_y), vmax=max(data_y))
plt.scatter(data_x, data_y, s=data_y * 1000, c=data_y, cmap=cmap, norm=norm, alpha=data_y)

plt.colorbar()
plt.show()
```

![[Pasted image 20221203182238.png|300]]

## 练习

### 读写文件

1.读取file1.txt和file2.txt内容
2.将两个内容合并写入到新的file3.txt中

### 改进除法

1.设计一个除法函数（参数为x,y）
2.在try中计算结果
3.捕获除数等于0的错误
4.如果没有错误提示“No errors”
5.用finally提示计算结束

### 画图练习

1.随机生成10个0到1之间的数，画出折线图
2.随机生成10个0到1之间的数，画出散点图
3.随机生成100个0到1之间的数，前50个数用折线图画到子图1，后50个数用散点图画到子图2

## 练习解析

练习的代码比较简单，但是读者们需要注意的是代码中的路径并不一定适用于你的环境，请根据你的环境自适应修改。

```python 3
path_file_1 = os.path.join(os.getcwd(), 'exp_files', 'file1.txt')
path_file_2 = os.path.join(os.getcwd(), 'exp_files', 'file2.txt')

file_1 = open(path_file_1)
file_1_content = file_1.readlines()
file_1.close()

file_2 = open(path_file_2)
file_2_content = file_2.readlines()
file_2.close()

path_file_3 = os.path.join(os.getcwd(), 'exp_files', 'file3.txt')

file_3 = open(path_file_3, 'w')
contents = file_1_content + ['\n' * 2] + file_2_content
for line in contents:
    file_3_content = file_3.write(line)

file_3.close()
```

在第二题除法运算中，最容易出现问题的地方是*计算部分*，因此将这部分放在try层级中。如果出现了除数为0的报错*ZeroDivisionError*，则提示用户确保除数不为0。需要提示的是，若只期待一种异常，except后不写也可以，但若有多个预期异常则需要提前写明白。

```python 3
def div(x, y):
    try:
        res = x / y
        print(res)
    except ZeroDivisionError:
        print("Make sure y != 0")
    else:
        print("No erros.")
    finally:
        print("=== Done ===")

div(10, 0)
```

