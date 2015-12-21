# 博客修改记录

## 2015年12月21日 10:00 主站调用子站

参考资料：[用jekyll生成json](http://yanping.me/cn/blog/2012/04/19/jekyll-with-json/)

### 子站
1. 给各子站根目录添加`recent.json`
2. recent.json 中增加摘要description，不知道能不能成功。

### 主站

1. 改根目录下的 index.html 
2. 已有 jquery ，不需要重复引入
3. 注释原来的：

    <article class="lotus-article">
        <!-- {% for rpost in paginator.posts limit:5 %}
            <h3><a href="{{ rpost.url }}" title="{{ rpost.title }}" rel="bookmark">{{ rpost.title }}</a></h3>
            <p itemprop="description">{{ rpost.description }}</p>
        {% endfor %} -->
    </article>

4. 改为：
    
    <article class="lotus-article">
        <div class="section" id="blog-read">
            <div class="loading">正在加载...</div>
        </div>  

        <div class="section" id="blog-write">
            <div class="loading">正在加载...</div>
        </div>  

        <div class="section" id="blog-think">
            <div class="loading">正在加载...</div>
        </div>  
    </article>
    
5. 末尾增加读取 json 的js

## 2015年12月20日 18:59:34  组织和多子站策略

### 一、组织、主站和子站

新建 ATio 组织。并建立一个主站（atio.github.io）和三个子站（read、write、think）

默认模版`default.html`中把页脚时间改为自动获取。

### 二、主站怎么改

1. 因为左侧侧边栏都在`_config.yml`文件里，所以这个不管是主站还是子站都很容易改。
    1. 暂时不管图标，先把链接给改过来。
2. `_config.yml`中的文章分类、归档、友链、书单怎么处理
    1. 最好是主站归档、主站分类
    2. 子站如果分类多，可以有自己的分类
    3. 书单删掉，只给 Read

首页输出的内容在站点根目录下`index.html`定义。

    {% for rpost in paginator.posts limit:5 %}
    <h3><a href="{{ rpost.url }}" title="{{ rpost.title }}" rel="bookmark">{{ rpost.title }}</a></h3>
    <p itemprop="description">{{ rpost.description }}</p>
    {% endfor %}

成不成，就看能不能把这一段改成输出子站的内容了……  
- 输出标题
- 链到子站

### 三、子站怎么改

#### 左侧

1. 左侧在`_config.yml`中修改。
2. 首页统一链接回主站
    1. Read：Write+Think+书单
    2. Write：Read+Think
    3. Think：Read+Write
    4. 不含自身，宁少勿超
3. 

#### 站点统计

`default.html`，cnzz

#### 面包屑导航

子站里的`首页 > 书单`、`首页 > 归档 > 两种 GitHub Pages 模式搭建博客`等面包屑导航是链接到主站的。  
感觉这个链接到子站更实用一些。因为我看完这篇文章，我点回首页，接着看这一个系列的文章更合理。

链接的事都好说，在模板里改成固定的，不要读取就行。关键是主站怎么做。

#### 站点基础配置

`_config.yml`里的“站点基础配置”里，设置站点域名。其中涉及到：
1. 博客名的链接
2. 存档链接
3. default模板中js的引用是{{ site.url }}形式的，相信其他页面也会是这样
4. 

要想区分主站子站：  
1. 要么这里设成主站域名，改其他的链接。
2. 要么这里设成二级域名，html 中改博客名的链接、存档链接等

以上暂时不改，使用一段时间后再看改哪个容易。  
目前这样子挺好的，子站文章是二级域名的形式。博客标题又是主站。文章归档有点问题，但是单个的问题可以在模板里改链接，或者考虑子站是否需要存档页。

## 2015年5月16日 15:04:55

首页设置了只显示最新的5篇文章（index.html 中 {% for rpost in paginator.posts limit:5 %}），为了照顾阅读体验，让访客更快的找到更多的文章的入口，把文章归档页加到首页当中来。替换下面这一条（5日修改记录）的最新文章。一箭双雕。

以上皆在index.html中修改。

## 2015年5月5日 20:47:56

恢复了首页的“最新文章”和“相关页面”。因为nav精简了，更多页面需要这个相关页面展示出来。但是最新文章不是必要的，并且现在显示的不对。这个以后改掉。

再改nav。去掉文章分类（icon: icon-folder-open），改为外链的Demo。

页脚添加cnzz统计代码。

## 2015年4月6日

### Contact WeChat QRcode

在联系页面增加微信二维码。

* contact.html 增加 html 代码
* style.css 增加相关css代码 `/* WeChat QRcode */`

## 2015年4月27日

### 导航nav

左侧导航在手机端只能显示最多4个，多的会被挤到下一行，错行了。故精简掉。

将“联系”整合到“关于”，隐藏links.html。页面都还在，只是不在导航上显示出来了。

contact.html 的 icon 是 icon-envelope-alt ，links.html 的 icon 为 icon-link。

### 多说评论系统

_layouts/post.html 中直接添加的多说代码。

## 补记

都忘了什么时候改的了，这在最开始应用这个模板的时候就做了吧：

_config.yml 中，nav：book 和 nav：goodbooks 为阅读书单 book.html 的条目。添加新单只需在此添加，无需编辑 book.html

# 待修改的地方

* 增加一个 page 模板。现在只有一个用于书单的模板。
* 做个推荐书单的模板，区别在开头有类似摘要的地方，以及已读未读的CSS代码要改。
* 正文缩进。现在用MD写作，不管是一级标题二级标题，后面的正文都没有缩进，光靠字体大小识别，整体感觉不好。不够鲜明。
* 计划复制link页做一个guest book，去掉每篇文章下的多说留言系统，在文章模版（_layouts/post.html）的最后加一句话，带上链接，需要的就去留言。