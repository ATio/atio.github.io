# 博客修改记录

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