---
title: hexo+next添加友言评论
tags: ["知识"]
---
### 为什么添加友言评论
因为诸如disqus之类的在国外，不翻墙是不能用的。<font color=red>注意：友言在本地是不能用的，必须布署到远程而且必须绑定域名才能使用。</font>
### 第一步，注册友言，添加新的站点
* 打开[友言](http://www.uyan.cc//) 的官网，注册新用户，并登录。
![](http://osar4k97c.bkt.clouddn.com/%E5%BE%AE%E4%BF%A1%E5%9B%BE%E7%89%87_20170630161538.png)
* 获取代码
![](http://osar4k97c.bkt.clouddn.com/%E5%BE%AE%E4%BF%A1%E5%9B%BE%E7%89%87_20170630161809.png)
* 复制红框内的uid
![](http://osar4k97c.bkt.clouddn.com/%E5%BE%AE%E4%BF%A1%E5%9B%BE%E7%89%87_20170630161944.png)
* 在thems/next/_config.yml添加uid
```
# ---------------------------------------------------------------
# Third Party Services Settings
# ---------------------------------------------------------------

# Duoshuo ShortName
#duoshuo_shortname:

# youyan
youyan_uid: 你的UID
```
* 这样就完成了添加