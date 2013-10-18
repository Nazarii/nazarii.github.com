---
layout: post
title: "Moving Virtual Box machine to another computer"
date: 2013-10-18 15:58
comments: true
categories: VirtualBox
---

From time to time I'm using [VirtualBox](https://www.virtualbox.org/) to launch Windows machines and here is a simple way of taking existing VM copy and restore it on another instance from command line:<!-- more -->
{% codeblock bash lang:bash%}
$ VBoxManage export <VM name> -o ~/exp.ova
{% endcodeblock %}

Copy newly created exp.ova file to another instance and to restore it run:
{% codeblock bash lang:bash%}
$ VBoxManage import ~/exp.ovf
{% endcodeblock %}

