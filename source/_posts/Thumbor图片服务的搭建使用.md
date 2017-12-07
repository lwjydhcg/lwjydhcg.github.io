---
title: Thumbor图片服务器的搭建与使用
date: 2017-12-06 14:52:26
tags: thumbor
categories: Linux
---
#### 参考资料
[官方文档](http://thumbor.readthedocs.io/en/latest/index.html)
[青蛙小白-使用thumbor搭建图片处理服务](https://blog.frognew.com/2017/08/image-process-service-with-thumbor.html#thumbor安装)
## Thumbor简介
Thumbor是一个python编写的智能图片服务器，可用来代理互联网上的图片链接，并进行缓存，裁剪，甚至包含了头像识别等功能，当然也可以用来做本地图片的访问服务。目前我们主要用来代理爬虫抓过来的图片地址，爬虫过来的图片本地化太占存储，引用源网链接又可能被防盗链处理，使用thumbor则完美解决了这种问题。
## 搭建
目前只支持python2.x版本，pip install thumbor即可安装。
命令thumbor-config > /etc/thumbor/thumbor.conf生成一个默认的配置文件
命令thumbor --port=8888 --conf=/etc/thumbor/thumbor.conf即可启动。
配置文件简介：
	1.File Storage存储代理过来的图片缓存，默认保存一个月。
	2.Resulte Storage存储裁剪等操作处理过后的结果集，默认是永久保存
	3.File loader指定本地文件的根目录，做本地图片的服务。
	4.Security安全，配置SECURITY_KEY秘钥，和ALLOW_UNSAFE_URL=False使用，可防止其他人使用该服务。
## 使用
1.通用：like http://图片服务域名/unsafe/(源网链接)
2.裁剪：like http://图片服务域名/unsafe/300x200/(源网链接)
3.加密链接：
	{% codeblock lang:python %}
	img_url = urllib.quote(源网链接)
	signature = base64.urlsafe_b64encode(
        hmac.new(SECURITY_KEY, img_url, digestmod=hashlib.sha1).digest()
	)
	return domain + "/" + signature + "/" + img_url
	{% endcodeblock %}
### 相关配置
{% asset_link thumbor.conf thumbor.conf%}, {% asset_link thumbor.service thumbor.service%}