---
layout: post
title:  "How to install shadowsocks server on Centos7"
date:   2018-05-19 12:05:00 +0800
categories: notes
---

Cant be too easy.

First

	wget –no-check-certificate https://raw.githubusercontent.com/teddysun/shadowsocks_install/master/shadowsocks.sh  
	chmod +x shadowsocks.sh  
	./shadowsocks.sh 2>&1 | tee shadowsocks.log  

Then input the config

	Please input password for shadowsocks-python
	(Default password: teddysun.com):

	---------------------------
	password = teddysun.com
	---------------------------

	Please input port for shadowsocks-python [1-65535]
	(Default port: 8989):8989

	---------------------------
	port = 8989
	---------------------------

It will run automatically, if you want run manually:

	/bin/python /usr/bin/ssserver -c /etc/shadowsocks.json -d start

Enjoy.
