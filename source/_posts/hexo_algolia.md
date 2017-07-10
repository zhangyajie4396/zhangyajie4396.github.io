---
title: hexo+next添加algolia搜索
tags: ["知识"]
---
### 为什么添加algolia搜索
第一当然是可以方便的查找所需文章，第二点就是之前常用的swiftype插件不再免费。
### 开始添加
* 下载最新的next主题（5.1.0），因为最新版的已经集成了algolia搜索，可以省去很多配置和修改。
* 去[algolia](https://www.algolia.com/)官网注册账号（我直接使用的github的账号）
* 新建index<br/>
![](http://upload-images.jianshu.io/upload_images/3899681-c00f0825ef763c9e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
* 在Hexo工程目录的根目录下执行<br/>
<pre><code>npm install hexo-algolia -save
</pre></code>
* 打开API Keys页面，里面的信息等会需要写到hexo的配置文件中
![](http://upload-images.jianshu.io/upload_images/3899681-a3cfcd8a11518577.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
* 在根目录的站点配置文件_config.yml
中加入如下配置，参照上图的各种key值
<pre><code>algolia:
  appId: 'appid'
  apiKey: 'apiKey'
  adminApiKey: 'adminApiKey'
  indexName: '上面填写的index名'
  chunkSize: 5000
  fields:
    - title
    - slug
    - path
    - content:strip</pre></code>
* 在\themes\next下找到_config.yml，找到如下内容，将enable修改为true，labels修改为自己需要的
<pre><code>algolia_search:
  enable: true
  hits:
    per_page: 10
  labels:
    input_placeholder: 输入关键字
    hits_empty: "没有找到与 [${query}]相关的内容"
    hits_stats: "${hits}条相关记录，共耗时 ${time}秒"</pre></code>
* 在themes\next\layout_partials中找到header.swig，找到以下代码并修改
```html
<a href="javascript:;" class="popup-trigger">
<!-- 添加开始-->
{% elseif theme.algolia %}
<a href="javascript:;" class="popup-trigger">
<!-- 添加结束-->
{% elseif theme.algolia %}
```
* 将下面的图片放置于Hexo根目录下source文件夹下的images文件夹中，命名为algolia_logo.svg。<br/>
* ![](http://image.qn.jerkybible.com/blog/algolia/algolia_logo.svg)
* 运行hexo algolia显示如下说明成功
![](http://osar4k97c.bkt.clouddn.com/%E5%BE%AE%E4%BF%A1%E5%9B%BE%E7%89%87_20170630164621.png)<br/>
* 这样就完成了添加