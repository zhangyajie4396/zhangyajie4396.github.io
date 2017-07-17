---
title: HTTP 406错误解决方法
tags: ["知识"]
---

* HTTP 406 错误意思为Not acceptable。翻译过来是“无法接受”。</br>

* 如果遇到406错误首先查看jackson包是否存在。

* 可以把返回值类型改成String.
* 查看请求url后缀是否为html类型，如果是html类型是会报406错的，可以在web.xml里再加一个其他类型（比如.do或.action等）。


