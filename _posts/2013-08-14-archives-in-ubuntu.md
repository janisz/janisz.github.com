---
layout: post
title: "Archives in Ubuntu"
description: "How to install necessary stuff to deal with Windows archive in Ubuntu"
category: Linux
tags: [linux, Ubuntu]
---
{% include JB/setup %}
I know that Ubuntu is an old African word that means "I can't install Debian", but I was nearly forced to install it. Why? Because it's just working and also good looking. Maybe it's not as fast as my old Fedora but it's usable.

Today I ran in to problem. 

<img style="display: block; margin-left: auto; margin-right: auto; width: 50%; height: auto;" src="/assets/images/could_not_display_archive.png" alt="could not display archive">

Oh, it's not a big deal. But in this particular case ubuntu GUI just failed. I tried to open `7z` and `RAR` archive. Ubuntu told me that it cannot open this files but it can find software that will do it for me. Great, I don't event need to manually install packages, only tow clicks and all required stuff will be on my machine.

But it was not working like that. It tried to download something. And than just break and show error prompt. Sollution was quite easy and I know it before Ubuntu acted (years with Fedora and SSH learns me how to deal with files in shell). I need to install `unrar` and `unzip`.

<iframe src="http://showterm.io/ce6668c7246966d5ba030" width="640" height="400"> </iframe> 



OK, it's not so hard. Why Ubuntu GUI faild - no idea. Why I waste my time to write about it. The main reason to write this post is to test [showterm](https://showterm.herokuapp.com/).
