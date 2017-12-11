---
title: SSH秘钥登录
date: 2017-12-07 17:14:27
tags: SSH
categories: Linux
---
## SSH秘钥登录
	1.ssh-keygen -t rsa命令，生成一对rsa加密的秘钥对。
	2.将生成的.ssh/目录下的公钥id_rsa.pub追加到服务端的.ssh/authorized_keys
	3.ssh 服务器IP，即可链接
## 注意
	Xshell的秘钥登录，也是这个原理，指定私钥文件，而服务端的authorized_keys加入私钥对应的公钥。