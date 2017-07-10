---
title: eclipse+iReport导出报表制作流程
tags: ["知识"]
---
### iReport介绍
* iReport是为JasperReports设计的强大的，直观的，易于使用的可视化报表设计器，为win32平台编写。允许用户可视化地编辑XML JasperDesign文件，可以和其它数据库进行JDBC通信。</br>

* 再设计模板时可以以HTML，PDF，XML方式预览，用它生成的文件有.jrxml和.jasper两种文件。

* jrxml：是可视化编辑的xml文件；

* jasper：经编译后生成的类文件，即报表模板文件。
### iReport的输出格式
* 其预览输出格式有：PDF，HTML，CSV。JAVA2D，EXCEL，纯文本，JRView。
### 报表的动态对象变量、参数、字段
* 字段Fields：是从数据库抽取出来的，在报表中出现的数据库内容。$F

* 参数Parameters：你写的应用需要提供给报表的入口。 $P

* 变量Variables：报表中一些逻辑运算的表现。 $V

* 每个对象的定义格式如下： $V{variablesName}
### 运行时需要.jasper文件；编译：把.jrxml->.jasper文件。
### 具体使用方法
* 安装iReport并打开。
* 新建模板：点击左上角【文件】-new-选择模版-点击open this Template-保存路径-完成。
![](http://osar4k97c.bkt.clouddn.com/1.jpg)
* 完成后会在对应路径生成一个.jrxml文件，点击如图所示按钮(编译)，会生成一个.jasper文件。把生成的.jrxml和.jasper文件放到项目对应的文件里即可(<font color=red>注：最后完成操作时要点击编译按钮才会更新最新的文件，不编译不奏效</font>)。<br/>
![](http://osar4k97c.bkt.clouddn.com/ireport/%E5%BE%AE%E4%BF%A1%E5%9B%BE%E7%89%87_20170703105905.png)
* 工作面板：我们一般用的有标题栏(Title)，详情(Detail1)，汇总栏(Summary)。在对应的栏点击右键-Delete Band即可删除不用的栏。
![](http://osar4k97c.bkt.clouddn.com/2.png)
* 点击【窗口】-【组件面板】显示组件面板，红色框内的为常用项，具体操作如图中标注所示
![](http://osar4k97c.bkt.clouddn.com/3.png)

* 静态字段需要自己手写，动态字段可以直接从实体类中获取。点击【工具】-【选项】弹出选项框，操作如下图所示，点击确定后会导入class文件。
![](http://osar4k97c.bkt.clouddn.com/4.png)
* 导入class文件后，操作如下(第4步到自己的eclipse中复制对应的类名即可)
![](http://osar4k97c.bkt.clouddn.com/5.png)
* 下图所示，即可获取后台字段。也可直接拖拽Fields中的属性到工作面板
![](http://osar4k97c.bkt.clouddn.com/ireport/6.png6.png)
* 获取属性中的list集合数据。拖动List到面板中会默认生成dataset1,再拖动会生成dataset2,以此类推，箭头所指的地方可以修改dataset。详细步骤如图所示
![](http://osar4k97c.bkt.clouddn.com/ireport7.png)

* 从后台获取list中的属性：右击dataset1-Edit Query，弹出框，操作如第6步（<font color=red>注：dataset1与上一步中箭头所指的dataset要一致</font>）
![](http://osar4k97c.bkt.clouddn.com/ireport/8.png)
* 添加边框如图所示。点击【窗口】-【属性】可以修改样式
![](http://osar4k97c.bkt.clouddn.com/ireport9.png)<br/>
![](http://osar4k97c.bkt.clouddn.com/ireport/10.png)<br/>
* $F所取的数据为Fields中的数据，$P所取的数据为Parameters中的数据。Fields如何添加属性上面已经做了介绍了，Parameter添加属性直接右键即可，Parameter中的属性与后台代码中的model.addAttribute("name",123)里的name保持一致。汇总栏(Summary)一般取的是Parameter里的数据。
![](http://osar4k97c.bkt.clouddn.com/ireport/11.png)<br/>
* 编译后先预览，如果预览成功再复制到eclipse中
![](http://osar4k97c.bkt.clouddn.com/ireport/12.png)
### iReport处理中文乱码
* 将亚洲语言包" iTextAsian.jar,"复制到iReport安装目录下的iReport-5.1.0\ireport\modules\ext下
* 将iTextAsian.jar添加到iReport的classpath中,在iReport中选择【工具】 【选项】菜单,点击出现如下界面，在Classpath中增加JAR包(iTextAsian.jar)即可。如图
![](http://osar4k97c.bkt.clouddn.com/ireport/13.png)
* 设置报表上各显示对象的相关属性,各属性设置说明如下: <br/>
    Font	name:    宋体 (中文字体) <br/>
    PDF font name:   STSong-Light <br/>
    PDF  Encoding:  UniGB-UCS2-H(Chinese Siplified) <br/>
    PDF   Embeded: √<br/>
![](http://osar4k97c.bkt.clouddn.com/ireport/14.png)<br/>
![](http://osar4k97c.bkt.clouddn.com/ireport/15.png)
