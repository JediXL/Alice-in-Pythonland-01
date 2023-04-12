# 蜘蛛断崖

![[Pasted image 20221206102013.png]]

在前面的章节中我们介绍了利用Python处理各种文件内的数据，但是数据不仅仅存在于文件形式中，在本章中我们将利用Python处理存放在网页上的相关数据。

在诸多Python广告中有一个显眼的字眼——“**爬虫**”，爬虫就是将网络上的数据**自动化**地获取分析。Python并不是唯一能够实现爬虫的编程语言，甚至大多数语言都可以实现这一功能，那为什么一提到Python时很多人的第一感觉都是爬虫呢？实际上还是归结于Python擅长处理数据的特性，用Python进行爬虫顺便处理数据就是一件一气呵成的事情了。

但是获取和处理网络上数据的方式和之前介绍的方法稍有区别。excel的本质功能就是为了存储数据，而网络空间的本质功能是为了展示（特殊类型的网络功能除外，如网盘），因为面向的对象不同，所以获取数据和处理数据的手段也有差异。

在进行文件处理的时候，我们强调过要处理文件首先需要知道**文件的位置**。那在处理网络数据时，我们也需要知道网络数据所在的具体位置，而这个位置就是我们网络URL，也就是我们常说的**网址**。

当我们输入网址后敲下回车，你就可以看到网站的模样了，但这不是这个网站数据的真实面貌。在《黑客帝国》中当你服下红药，你就会看到虚拟世界的真相。而我们只需要开启浏览器的**开发者工具**就可以看到某个网页的真实数据面貌，右侧框里即为所谓的html代码。

![[Pasted image 20221219151733.png|500]]

所以当我们访问网址时，我们看到的页面实际上是由浏览器进行翻译过后展示给我们的，有时用不同的浏览器看到的同一网址有细微差距，其原因就是不同浏览器翻译出来的细节有所不同。

当然在这里我们并不需要看懂html代码，我们只需要在里面找到我们想要的内容就可以了。想要Python程序顺利地获取网站数据，**就要把Python程序打造地和浏览器类似**，也就是用Python来模仿浏览器。

浏览器是怎样获取数据的呢？浏览器和网站服务器之间的数据交互主要有两种方法。第一种是**GET**，即将数据从服务器上取下来。第二种是**POST**，主要应用于和服务器传输加密信息，如登录信息等。

![[Pasted image 20221219152618.png|500]]

同样利用浏览器的开发者工具，打开Bilibili，会发现浏览器就是通过GET方法和B站服务器之间进行数据交互的。当你点开B站的登陆界面时，利用同样方法，你会发现这时的交互方式是POST，并且其中内容是加密形式的。本章主要介绍的数据获取方法是GET。

除了数据获取方法，在上图中有一大块内容：**Response Headers**，我们称之为请求头，它可以让服务器知道我们的浏览器信息，比如之前是否登录过、系统语言、浏览器内核版本等基本信息。上图中还有一个关键因素**Status Code**（状态代码）等于200，200意味着请求成功，这或许对各位来说是一个相对陌生的代码，但提到另一个代码想必各位读者就很熟悉了，这就是常见的代码**404**。

由于代码200意味着请求成功，所以我们在利用Python获取网页数据时首要关注的就是状态代码，如果状态代码是200则代表我们请求成功，我们再继续后续操作。

我们再次强调，本章中利用Python获取网页数据的基本方法是：**将Python包装成浏览器模样，使用GET方法获取数据。**

那如何将Python包装成浏览器呢？本章中介绍的是**urllib包**中的request方法。

```python 3
import ssl
from urllib import request

url = 'https://www.bilibili.com/'
context = ssl._create_unverified_context() 
headers = {
'User-Agent':
'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/108.0.0.0 Safari/537.36'
} # 伪装成浏览器

req = request.Request(url, headers=headers, method='GET')
response = request.urlopen(req, context=context)
print(response.read().decode('utf-8'))
```

我们给定了一个url做为获取数据的对象。在包装过程中最重要的部分就是请求头中的“**User-Agent**”部分，将网页开发者工具的请求头部分下拉就可以看到这一部分内容。最后我们强调请求的方法是：method='GET'。

ssl是什么呢？读者们可能会注意到访问有些网站时网址的最前面有一把小锁。这个小锁代表的是一种加密认证，有些网站要求必须经过ssl方式才可访问。

![[Pasted image 20221219154459.png|400]]

urllib是一种比较原始简单的方法，我们也可以直接使用**request包**，这是一种更简单的获取方法。导入该包后给定一个访问的地址，做好相应的伪装就可以一行代码获取网站数据了。

```python 3
import requests
import os

url = 'https://www.bilibili.com/'
headers = {
'User-Agent':
'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/108.0.0.0 Safari/537.36'
} # 伪装成浏览器

req = requests.get(url, headers=headers)
req.text
```

### 第一个爬虫程序

我们爬取B站的番剧排行榜，并对其中内容做简单分析和处理。

```python 3
import requests

def req_BSite(url):
    try:
        response = requests.get(url)
        if response.status_code == 200:
            return response.text
    except requests.RequestException:
        return None

url = 'https://www.bilibili.com/v/popular/rank/bangumi/'
page = req_BSite(url)
```

首先声明番剧排行榜的网址，也就是我们要抓取的网址对象。其次，我们定义了一个函数，那这个函数存在的必要性是什么呢？实际上这既结合了上一章中Python异常处理的内容，也兼顾了状态代码的知识，本质功能是**判断请求是否成功**。

但是网页上的内容是非常的冗杂的，我们所关注的只有具体排行榜内容。那我们如何获取我们真正想要的数据呢？**我们首先定位想要的数据到底以何种方式存放在哪里，然后再将其取出**。同样是在开发者工具中，点击elements，通过左上角的小鼠标选中页面我们想提取的部分，会发现这一部分内容被打上了阴影同时右侧html代码也定位了它的位置。通过比较可以发现，排行榜的内容都被封装在了一个个列表中，列表中有他的id，rank等信息，而这些数据就是我们真正想要的。

![[Pasted image 20221219162706.png]]

再次对上图进行分析，我们会发现虽然排名有先后，id有不同，但是每一个排行榜内的番剧封装成的list都有一个共同属性，class="rank-item"，各位读者不必去理解这里的class到底代表什么，只需知道这是排行榜内容所共有的，而这个共性足以帮我们**定位到真正的排行榜部分**。

这时候就需要用到另一个库和方法，BeautifulSoup。bs是它的简写，4代表了版本号，这个库最主要的内容就是如何从网页抓取数据。

```python 3
from bs4 import BeautifulSoup

soup = BeautifulSoup(page, 'lxml')
items = soup.find_all("li", {"class": "rank-item"})
```

我们把获取到的页面输入，并且规定一个数据格式，就得到了一碗大杂烩汤。接下来我们就需要对汤里的内容进行筛选，我们要找的就是所有在li里且class为"rank-item"的数据，这时我们就取到了真正的排行榜内容。

观察结果我们会发现好像还是不尽如人意，因为每一个排行榜内容中还会显示该番剧的更新状态、播放量、点赞人数等。假如我们所关心的只是排名和番剧名，那这些数据也是多余的，因此我们还需要进一步进行**数据清洗**。

如果我们将刚才的items打印出来（仅打印第1个）会发现第一行是排名和番剧名，这正是我们所需要的，而后续内容我们都不关心，那我们数据清洗的目的就是保留第一行。

![[Pasted image 20221219173625.png|300]]

我们按照行对items中的内容进行切割，并且只取用第0行，随后将所有结果写入列表，最终将处理后的数据存入某个txt文件。

```python 3
res = []
for item in items:
    info = item.text.splitlines()[0]
    print(info)
    res.append(info)

path_res = os.path.join(os.getcwd(), 'exp_files', 'phb.txt')
file = open(path_res, 'a')
for r in res:
    file.write(r + '\n')
file.close()
```

## 练习

### 爬取B站音乐排行榜

尝试用 Python 爬取B站的音乐排行榜单，并将结果存储在txt文件中。