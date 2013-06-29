---
layout: post
title: "Few SSH productivity tips for newbies."
date: 2013-06-29 18:22
comments: true
categories: Linux
---
[SSH](http://en.wikipedia.org/wiki/Secure_Shell) has many features which are helpful when working regularly with files on remote servers, together they can give a vast increase in productivity over the bare use of <a href="http://en.wikipedia.org/wiki/Secure_Shell">ssh</a>. If you regularly use <a href="http://en.wikipedia.org/wiki/Secure_Shell">ssh</a>, it’s worth spending a little time learning about these and configuring your environment to make your life easier.<!-- more -->
I'm working with ssh over a year and here are few tips to make this work easier when connecting to remote server.
## Too lazy to type password?
If currently you type a password when making an SSH connection, you can make connecting much more pleasant by setting up SSH keys. With keys you do get prompted for a pass phrase, but this happens only once per booting your computer, rather than on every connection. With OpenSSH generate yourself a private key with:

{% codeblock zsh lang:bash%}
$ ssh-keygen
{% endcodeblock %}

and follow the prompts. Do provide a pass phrase, so your private key is encrypted on disk. Then you need to copy the public part of your key to servers you wish to connect to. If your system has ssh-copy-id then it’s as simple as:
{% codeblock zsh lang:bash%}
$ ssh-copy-id username@example.org
{% endcodeblock %}
Otherwise you need to do it manually:

*1. Find the public key. The output of ssh-keygen should say where this is, probably ~/.ssh/id_rsa.pub.*

*2. On each of your remote servers insert the contents of that file into ~/.ssh/authorized_keys.*

*3. Make sure that only your user can write to both the directory and file.*

Then you can SSH to servers, copy files, and commit code all without being hassled for passwords.

## Too lazy to type full hostnames?
If you're tired of typing same username and server address follow these tips:
###Hostname Aliases

You can define hostname aliases in your SSH config, which is usually located in ~/.ssh/config though this can involve listing each hostname. For example:
{% codeblock vim lang:vim%}
Host dev
  HostName dev.example.com
  Port 1422
{% endcodeblock %}
You can even use wildcards to group similar hostnames, using %h in the fully qualified domain name:
{% codeblock vim lang:vim%}
Host dev intranet backup
  HostName %h.example.com

Host dev mail
  HostName %h.example.com
{% endcodeblock %}
Next time you type **ssh dev** it will connect to **dev.example.com**.

###Don’t Type Usernames

If your username on a remote server is different from your local username, and when you often connect with the same user specify this in your SSH config as well:

{% codeblock vim lang:vim%}
Host dev mail
  HostName %h.example.com
  User nazik
{% endcodeblock %}
Now even though my local username is nazarii, I can just do:

{% codeblock zsh lang:bash%}
$ ssh dev
{% endcodeblock %}
and SSH will connect to the nazik account on the server.