---
title: WebService简单教程
tags: ["WebService"]
---
### 什么是webService
* WebService，顾名思义就是基于Web的服务。它使用Web(HTTP)方式，接收和响应外部系统的某种请求。从而实现远程调用。</br>

* 从WebService的工作模式上理解的话，它跟普通的Web程序（比如ASP、JSP等）并没有本质的区别，都是基于HTTP传输协议的程序。

* WebService所使用的数据均是基于XML格式的。目前标准的WebService在数据格式上主要采用SOAP协议。SOAP协议实际上就是一种基于XML编码规范的文本协议。

### webService的技术支持
* Web Service平台需要一套协议来实现分布式应用程序的创建。任何平台都有它的数据表示方法和类型系统。要实现互操作性，Web Service平台必须提供一套标准的类型系统，用于沟通不同平台、编程语言和组件模型中的不同类型系统。目前这些协议有：
### XML和XSD
* 可扩展的标记语言XML　是Web Service平台中表示数据的基本格式。除了易于建立和易于分析外，XML主要的优点在于它既与平台无关，又与厂商无关。XML是由万维网协会(W3C)创建，W3C制定的XML SchemaXSD　定义了一套标准的数据类型，并给出了一种语言来扩展这套数据类型。

* Web Service平台是用XSD来作为数据类型系统的。当你用某种语言如VB. NET或C#　来构造一个Web Service时，为了符合Web Service标准，所有你使用的数据类型都必须被转换为XSD类型。如想让它使用在不同平台和不同软件的不同组织间传递，还需要用某种东西将它包装起来。这种东西就是一种协议，如 SOAP。
### SOAP
* SOAP即简单对象访问协议(Simple Object Access Protocal)，它是用于交换XML编码信息的轻量级协议。它有三个主要方面：XML-envelope为描述信息内容和如何处理内容定义了框架，将程序对象编码成为XML对象的规则，执行远程过程调用(RPC)的约定。SOAP可以运行在任何其他传输协议上。例如，你可以使用 SMTP，即因特网电子邮件协议来传递SOAP消息，这可是很有诱惑力的。在传输层之间的头是不同的，但XML有效负载保持相同。
* Web Service 希望实现不同的系统之间能够用“软件-软件对话”的方式相互调用，打破了软件应用、网站和各种设备之间的格格不入的状态，实现“基于Web无缝集成”的目标。
### WSDL
* Web Service描述语言WSDL　就是用机器能阅读的方式提供的一个正式描述文档而基于XML的语言，用于描述Web Service及其函数、参数和返回值。因为是基于XML的，所以WSDL既是机器可阅读的，又是人可阅读的。
### UDDI
* UDDI 的目的是为电子商务建立标准；UDDI是一套基于Web的、分布式的、为Web Service提供的、信息注册中心的实现标准规范，同时也包含一组使企业能将自身提供的Web Service注册，以使别的企业能够发现的访问协议的实现标准。 调用RPC与消息传递。
* Web Service本身其实是在实现应用程序间的通信。我们现在有两种应用程序通信的方法：RPC远程过程调用　和消息传递。使用RPC的时候，客户端的概念是调用服务器上的远程过程，通常方式为实例化一个远程对象并调用其方法和属性。RPC系统试图达到一种位置上的透明性：服务器暴露出远程对象的接口，而客户端就好像在本地使用的这些对象的接口一样，这样就隐藏了底层的信息，客户端也就根本不需要知道对象是在哪台机器上。
### 如何发布一个WebService？
* 第一个WebService服务
* 首先要准备jar包，这里就不多说了，自行下载。
* 创建一个接口HelloWorld：
```java
	package webService_cxf;

	public interface HelloWorld {
		String sayHi(String name);
	}
```
* 创建一个实现类HellowWorlds,使用@WebService修饰:
```java
package webService_cxf;

import java.util.Date;

import javax.jws.WebMethod;
import javax.jws.WebService;

@WebService
public class HellowWorlds implements HelloWorld {
	
	@WebMethod
	@Override
	public String sayHi(String name) {
		// TODO Auto-generated method stub
		return name+"你好，现在是北京时间："+new Date();
	}

}
```
* 暴露Web Service的函数，运行函数暴露Web Service：
```java
package webService_cxf;

import javax.xml.ws.Endpoint;

public class Server {
	public static void main(String[] args) {
		HelloWorld hw = new HellowWorlds();  
        //调用Endpoint的publish方法发布Web Service  
       Endpoint.publish("http://192.168.1.104/helloworld",hw);  
        System.out.println("Web Service暴露成功！");
	}
}
```
* 然后运行浏览器，输入：http://192.168.1.104/helloworld?wsdl 查看结果，如果成功生成如下wsdl文档则表示Web Service暴露成功
![](http://osar4k97c.bkt.clouddn.com/%E5%BE%AE%E4%BF%A1%E5%9B%BE%E7%89%87_20170704113518.png)
### 开发客户端
* 用wsimport工具。wsimport是jdk自带的,可以根据wsdl文档生成客户端调用代码的工具.当然,无论服务器端的WebService是用什么语言写的,都将在客户端生成Java代码.服务器端用什么写的并不重要。
* 任意打开一个盘，我在d盘新建一个文件夹(<font color=red>注：最好用英文，中文会出错</font>),并转到此目录下，打开cmd,输入命令wsimport –s . http://192.168.1.104/helloworld?wsdl 
* 参数说明:-s是指编译出源代码文件,后面的.(点)指将代码放到当前目录下。最后面的http….是指获取wsdl说明书的地址。
* 将生成.java文件和.class文件.(都包含原始包名).将代码Copy到你的项目中.(只拷贝java文件)
* 在新的项目中,新一个类,(可位于任意包下),对上面生成的代码进行调用：
```java
public class Test {
	public static void main(String[] args) {
		HellowWorlds h = new HellowWorldsService().getHellowWorldsPort();
		String s = h.sayHi("zhangyajie");
		System.out.println(s);
	}
}
```