---
layout: post
title: "Python: starting http server in one command"
date: 2013-07-28 22:21
comments: true
categories: Python
---

The idea is taken from it's own post on [habrahabr](http://habrahabr.ru/post/118460/).<!-- more --> 
We need to share 2GB file throw our local network
and the quickest and simpliest way by advice of our [Joda](http://www.linkedin.com/profile/view?id=98165358&authType=name&authToken=oGVS&goback=) was to start local http server with the help of Python. To do it simply type in console:
{% codeblock bash lang:bash%}
python -m CGIHTTPServer
{% endcodeblock %}
This will start http server on default 8000 port and after opening you browser on **[http://localhost:8000](http://localhost:8000)** you should see a list of files in directory you prompted command from. Copy link address of file you need to and share with other members of you network. Enjoy fast download speed with python!
