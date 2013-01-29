---
layout: post
title: "k3b   auto mp3 converting"
description: "How to allow k3b convert mp3 files on Fedora"
category: ["GNU/Linux"]
tags: [k3b, feodra, linux, mp3]
---
{% include JB/setup %}

Have you ever face with k3b error "MP3 Audio Decoder plugin not found."
Here if simple solution for it:

	sudo yum install k3b-extras-freeworld libmad gstreamer-plugins-ugly audacious-plugins-freeworld-mp3 xmms-mp3

You probably need to install rpm fusion first

	rpm -Uvh http://download1.rpmfusion.org/free/fedora/rpmfusion-free-release-stable.noarch.rpm http://download1.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-stable.noarch.rpm


