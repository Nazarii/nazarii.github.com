---
layout: post
title: "Proxylocal - share your local web server via Internet"
date: 2014-10-09 23:33
comments: true
categories: Tools
---

[ProxyLocal](http://proxylocal.com/) is a tool that runs on the command line, It could proxy your local web-server and make it publicly available over the internet. Really usefull tool for showing demos with local access to the server.

Assume you are running your local web-server on port 8069. To make it publicly available run:
{% codeblock bash lang:bash%}
$ proxylocal 8069 --host demo32
Local server on port 8069 is now publicly available via:
http://demo32.t.proxylocal.com/
{% endcodeblock %}
<!-- more -->
##Installation
On any system with [ruby](http://www.ruby-lang.org/en/downloads/) and [rubygems](https://rubygems.org/pages/download) installed, open your terminal and type:

{% codeblock bash lang:bash%}
$ gem install proxylocal
{% endcodeblock %}
