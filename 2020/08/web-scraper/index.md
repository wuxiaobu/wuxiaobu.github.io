# Web Scraper简易教程


#  Web Scraper简易教程

## 步骤一：下载 Web Scraper

Web Scraper 是 Chrome 浏览器上的一个插件，你需要**翻墙进入 Chrome 应用商店，下载 Web Scraper 插件**。

![img](http://image.woshipm.com/wp-files/2017/08/HT7gcdqxb49jK2WdEfAo.jpg)

## 步骤二：打开 Web Scraper

先打开一个你想爬数据的网页，比如我想爬今日头条上「吴晓波频道」这个账户的文章标题、时间、评论数，那我就先打开它，再一一进行操作。

然后**用快捷键 Ctrl + Shift + I / F12 打开 Web Scraper**。

![img](http://image.woshipm.com/wp-files/2017/08/lVJvOPFzwYKpDriRGlHZ.jpg)

## 步骤三：新建一个 Sitemap

**点击 Create New Sitemap**，里面有两个选项，import sitemap是指导入一个现成的 sitemap，咱小白一般没有现成的，所以一般不选这个，选create sitemap 就好。然后进行这两个操作：

![img](http://image.woshipm.com/wp-files/2017/08/na17iFQIjrwu7DyRB1jf.jpg)

- **Sitemap Name**：代表你这个 Sitemap 是适用于哪一个网页的，所以你可以根据网页来自命名，不过需要使用英文字母，比如我抓的是今日头条的数据，那我就用 toutiao 来命名；
- **Sitemap URL**：把网页链接复制到 Star URL 这一栏，比如图片里我把「吴晓波频道」的主页链接复制到了这一栏。

## 步骤四：设置这个 Sitemap

整个 Web Scraper 的抓取逻辑是这样：**设置一级 Selector，选定抓取范围；在一级 Selector 下设置二级 Selector，选定抓取字段，然后抓取**。

咱们换个接地气的例子，假如你要获取福建人的姓名、性别和年龄这三个要素，那么你得这么做：首先要定位到福建省，然后再在福建省里面去定位姓名、性别、年龄。

在这里，一级 Selector 表示你要在中国这个大的国家圈出福建省，二级Selector 表示你要在福建省的人口中圈定姓名、性别、年龄这三个要素。

对于文章而言，一级 Selector 就是你要把这一块文章的要素圈出来，这个要素可能包含了 标题、作者、发布时间、评论数等等，然后我们再在二级 Selector 中挑出我们要的要素，比如标题、作者、阅读数。

下面我们来拆解这个设置一级、二级 Selector 的工作流：

### **1. 点击 Add new selector 创建一级 Selector，按照以下步骤操作：**

![img](http://image.woshipm.com/wp-files/2017/08/Ewwz9S0Lr1hYY53OnVaP.jpg)

- **输入id**：id 代表你**抓取的整个范围**，比如这里是文章，我们可以命名为 wuxiaobo-articles；
- **选择Type**：type 代表你**抓取的这部分的类型**，比如元素／文本／链接，因为这个是整个文章要素范围选取，我们需要用 Element 来先整体选取（如果这个网页需要滑动加载更多，那就选 Element Scroll Down）；
- **勾选Multiple**：勾选 Multiple 前面的小框，因为你要选的是**多个元素**而不是单个元素，当我们勾选的时候，爬虫插件会帮助我们识别多篇同类的文章；
- **保留设置**：其余未提及部分保留默认设置。

### **2. 点击 select 选择范围，按照以下步骤操作：**

![img](http://image.woshipm.com/wp-files/2017/08/GKmOTp5r4mt20cl4FEBq.jpg)

- **选择范围**：用鼠标选择你**要爬取数据的范围**，绿色是待选区域，用鼠标点击后变为红色，才是选中了这块区域；
- **多选**：不要只选一个，**下面的也要选**，否则爬出来的数据也只有一行；
- **完成选择**： 记得点 Done Selecting；
- **保存**：点击 Save Selector。

### **3. 设置好了这个一级的 Selector 之后，点进去设置二级的 Selector，按照以下步骤操作：**

![img](http://image.woshipm.com/wp-files/2017/08/iBKr1HuyJiKJQZhbuCIu.jpg)

- **新建Selector**：点击 Add new selector ；
- **输入id**：id 代表你抓取的是哪个字段，所以可以取该字段的英文，比如我要选「作者」，我就写「writer」；
- **选择Type**：选 Text，因为你要抓取的是文本；
- **勿勾选Multiple**：不要勾选 Multiple 前面的小框，因为我们在这里要抓取的是单个元素；
- **保留设置**：其余未提及部分保留默认设置。

### **4. 点击 select，再点击你要爬取的字段，按照以下步骤操作：**

![img](http://image.woshipm.com/wp-files/2017/08/EhCE5hOXirTVz4EDk5rm.jpg)

- **选择字段**：这里爬取的**字段是单个的**，用鼠标点击该字段即可选定，比如要爬标题，那就用鼠标点击某篇文章的标题，当字段所在区域变红即为选中；
- **完成选择**：记得点 Done Selecting；
- **保存**：点击 Save Selector。

### **5. 重复以上操作，直到选完你想爬的字段。**

## 步骤五：爬取数据

之所以说 Web Scraper 是傻瓜式爬虫工具，就是因为只需要设置完所有的 Selector，就可以开始爬数据了，怎么样，是不是简单？

那么怎么开始爬数据呢？只需要一个简单的操作：**点击 Scrape，然后点Start Scraping**，会弹出一个小窗，然后辛勤的小爬虫就开始工作了。你会得到一个列表，上面有你想要的所有数据。

![img](http://image.woshipm.com/wp-files/2017/08/0oDTvTQmFrFm4jLq3YMg.jpg)

如果你希望把这些数据做一个排序，比如按照阅读量、赞数、作者等指标排序，让数据更一目了然，那么你可以**点击 Export Data as CSV，把它导入 Excel 表里**。

![img](http://image.woshipm.com/wp-files/2017/08/V2NW4fjl1qznrbqItMxj.jpg)

导入 Excel 表格之后，你就可以对数据进行筛选了。

![img](http://image.woshipm.com/wp-files/2017/08/0MRSz1ADvaSlaA9N3XHL.jpg)

以上就是快速上手 Web Scraper 的所有操作过程，连我这种懒癌 + 手残都能在 5 分钟之内搞定，相信你也可以指哪儿爬哪儿，完全 OK 的啦。
