---
layout: post
title: "Install Boost on Ubuntu"
description: "Short script to download and install Boost on Ubuntu"
category: programming
tags: [c++,boost,Ubuntu,Linux,GNU]
---
{% include JB/setup %}

Sometimes in your life is day when you need to compile lib from sources because you (or your coworker) need
to use this particular version of it. If everybody works on same OS and have similar configuration and
lib is not small and require more than `./configure && make && sudo make install` it might be useful to create
installation script instead of description in readme. In fact readme will look like script so why bother
to put in unreadable (from computer point of view) format like Markdown.

Here is short script to replace boost with version 1.54 with additional thread-pool. It's clean, short and fast but
it's not working on Ubuntu Server yet.


{% gist 7682585 %}


You can watch it in action [here](http://showterm.io/4cd49a7a140a13d04b1f0#fast) but it's not really interesting
better watch some conference when your computer will be busy with compiling stuff.