---
title: WebService
date: 2018-01-25 11:15:20
tags: WebService
categories: 杂谈
---
WebService是一种跨语言和跨平台的远程调用技术，就是一种部署在网络上的API, 算是一种规范。
它提供了一个标准和规范，来处理各个系统间的通信，以实现数据交互。
服务提供方根据WebService的标准来编写服务接口。
服务调用方使用WebService的接口进行调用，进行其业务方法。

RPC（远程过程调用）：调用远程计算机上的服务，就像调用本地服务一样。它只是一个概念，不是实际的技术或者协议规范，实现RPC的协议有很多，比如WebService的RPC风格，Java的RMI, Thrift, 甚至Rest API。RPC可以基于HTTP或者TCP协议。WebService是基于HTTP协议的RPC，虽然性能不如基于TCP协议的RPC，但是更安全，更被广泛使用，并且具有良好的跨平台性，

WebService的实现三大技术：
*XML+XSD*: 定义了一套标准的数据类型，给出了一种语言来扩展这套数据类型。当使用某种语言（java, C#）构造web service时，语言本身的数据类型要被转换为XSD数据类型。

*SOAP(Simlple Object Access Protocol)*: 
WebServcie通过http发送请求和接受响应时，内容都采用了XML格式封装，并增加了一些特定的HTTP header。 这些header和xml内容就是SOAP协议规范。
SOAP比一般的http请求的区别在于，它是用来传输对象的。

*WSDL(Web Service Description Language)*:
WebService描述语言，是一个xml文档，描述一个服务的输入，输出，网络地址，调用方式等信息。通常服务地址后面追加?wsdl即可查阅。