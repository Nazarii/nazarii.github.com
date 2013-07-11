---
layout: post
title: "Accessing ftp server with SSL/TSL enabled using python 2.6"
date: 2013-07-11 22:06
comments: true
categories: 
---

Just want to provide a solution of problem I've faced, maybe it will be usefull for someone.
Issue is next:
{% blockquote %}
We need to connect to remote ftp server, download and delete existing files.
{% endblockquote %}
<!-- more -->
Look's easy, let's use standard library [ftplib](http://docs.python.org/2/library/ftplib.html):
{% codeblock sublime-text lang:python%}
from ftplib import FTP
import os


def get_data(host, username, passwd, directory_path='/'):
    connection = FTP(host=host, user=username, passwd=passwd)
    filenames = connection.nlst()
    file_counter = 1
    for filename in filenames:
        file_path = os.path.join(directory_path, file_counter)  # Supposed you use Postfix os, on windows locations would be different
        with open(file_path, 'wb') as output_file:
            connection.retrbinary('RETR %s' % filename, lambda data: output_file.write(data))
            output_file.close()
            connection.delete(filename)
            counter += 1
    connection.quit()
    return True
{% endcodeblock %}

Code was working nicely untill one moment i get exception <i><font color="red">530 SSL required</font></i>.
The deal is because of user configuration on remote server, it is set to reguire [SSL/TLS](http://en.wikipedia.org/wiki/Transport_Layer_Security) encryption. But standard ftplib in my version of python 2.6.5 doesn't provide solution to connect with SSL/TLS, it was added in python 2.7. Version update looks bad, external libraries i also dont want to use. So i decided to get ftplib module from 2.7 version and use in my code.**(Download [2.7 version](http://www.python.org/download/releases/2.7/) and locate ftplib.py file)** After replacing standard ftplib file in you pythonpath with one frpm 2.7 out code looks like:
{% codeblock sublime-text lang:python%}
from ftplib import FTP_TLS
import os


def get_data(host, username, passwd, directory_path='/'):
    connection = FTP_TLS(host=config_obj.host, user=config_obj.username, passwd=config_obj.passwd)
    connection.prot_p()
    filenames = connection.nlst()
    file_counter = 1
    for filename in filenames:
        file_path = os.path.join(directory_path, file_counter)
        with open(file_path, 'wb') as output_file:
            output_file.close()
            connection.delete(filename)
            counter += 1
    connection.quit()
    return True
{% endcodeblock %}

*Also I want to notice if you do not want to break anything with further using ftplib library after replacing, my suggestion is to not replace files but to use file as separate module(e.g. if you run code from your own package copy downloaded file in it and include in **__init__.py**, the in code where you want to use it import like **from <your_module_name> import ftplib as ftplib2.7**).*