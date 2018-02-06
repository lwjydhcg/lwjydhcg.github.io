---
title: Celery之Routing Task
date: 2018-01-18 17:20:01
tags: 
- Celery
- AMQP
- RabbitMQ
categories: Python
---

# Celery简介
框架名中文译作芹菜，是一个python异步任务分布式处理框架。
![流程图](http://img.blog.csdn.net/20170415031435992?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQveHNqX2Jsb2c=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
简单来讲，就是将任务即时返回，不影响主线程的后续操作。异步的任务则通过broker分发给不同的队列。celery worker则后台等待队列的任务并执行，完成任务后删除队列中任务消息。
最大的困惑在于配置任务进入指定队列。

# 配置queue和route

由于刚深入接触其Routing Task路由任务，对配置诸多不解，研究了好久终于有所得。
一个任务带着Exchange, 传输给MQ后，mq对比routing key，路由到匹配的队列中。注意：redis是没有exchange的，只需要指定queue即可。

{% asset_img celery.png %}
CELERY_QUEUES主要是配置队列信息，第一个参数是队列中的key名称，第二个参数Exchange是交换器极其类型（默认direct=直接），第三个参数routing_key是绑定在exchange上的。

CELERY_ROUTES主要是配置路由信息，第一个参数是app.task注册的任务名称，queue表示指定哪个队列（只在没有指定exchange时有意义），而exchange和routing_key则是用来对标上面QUEUES的exchange，使queue的exchange按照规则分发任务到队列。

### RabbitMQ中的Exchange列表

{% asset_img exchange_list.png %}

### Ex_clean的绑定信息

{% asset_img exchange_detail.png%}

### Queues详情

{% asset_img queues.png%}

# 参考资料
[Celery消息队列](http://blog.csdn.net/xsj_blog/article/details/70181984)
[Celery Routing Task AMQP Primer](http://docs.celeryproject.org/en/latest/userguide/routing.html?#amqp-primer)
