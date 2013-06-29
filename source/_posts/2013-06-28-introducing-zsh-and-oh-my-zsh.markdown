---
layout: post
title: "Introducing ZSH."
date: 2013-06-28 14:28
comments: true
categories: [GIT, Linux]
---

Today I'd like to show you really usefull tool for working in command line I've discovered - <a href="http://www.zsh.org/">ZSH</a>.
The Z Shell (<a href="http://www.zsh.org/">zsh</a>) is a power shell that is not often used by many Linux users. The reason for this is that most Linux distributions install, and make default, the bash shell.<!--more--> zsh is packaged for virtually every Linux distribution and installation on Ubuntu is simple made by running

{% codeblock bash lang:bash%}
$sudo apt-get install zsh
{% endcodeblock %}

After installation main configuration file .zshrc is located in you'r home directory.
To make zsh as default shell run chsh command and include path to it's executable:

{% codeblock bash lang:bash%}
nazik@nazik-HP:~$ chsh
Password: 
Changing the login shell for nazik
Enter the new value, or press ENTER for the default
    Login Shell [/bin/bash]: /bin/zsh
{% endcodeblock %}

One of the great features of zsh is tab-completion; it also handles all the logistics of tab-completion and is extremely easy to implement, just by adding two lines to your ~/.zshrc file:

{% codeblock zsh lang:bash%}
autoload -U compinit
compinit
{% endcodeblock %}

The compinit function is what loads the tab-completion system by defining a shell function for every utility that zsh is able to tab-complete. By using autoload, you can optimize zsh by telling it to defer reading the definition of the function until it's actually used, which speeds up the zsh startup time and reduces memory usage.

Also there is awesome plugin <a href="https://github.com/robbyrussell/oh-my-zsh">oh-my-zsh</a> especially if you are often working with <a href="http://en.wikipedia.org/wiki/Git_(software)">GIT</a> repositories.
To install this one run:

{% codeblock zsh lang:bash%}
$wget --no-check-certificate https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh -O - | sh
{% endcodeblock %}

After installation you might need to reload you shell:

{% codeblock zsh lang:bash%}
source ~/.zshrc
{% endcodeblock %}

Each time you cd to you git repo it will show you branch you currently working on and whether you have uncommited local changes or not, if so it will show you gold sign:
{% img center /images/zsh_screen.png 950 650 'image' 'images' %}
Also there are a lot of themes for this plugin you can choose to use the other one then default "robbyrussell" theme. List of themes you can get at this <a href="https://github.com/robbyrussell/oh-my-zsh/wiki/themes">link</a>. To change to other one you need to edit you .zshrc file and reload shell.

You can also use aliases after adding it to your config file.
To add time of command prompting to the right side of terminal append following line to your config file:
{% codeblock vim %}
RPROMPT=$'%{\e[1;34m%}%T%{\e[0m%}'
{% endcodeblock %}.


