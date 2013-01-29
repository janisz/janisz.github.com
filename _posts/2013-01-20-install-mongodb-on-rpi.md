---
layout: post
title: "Install MongoDB on rPI"
description: "Step by step instruction how to install MongoDB on raspberry pi"
category: 'RaspberryPi'
tags: [raspberry pi, raspberry, pi, MongoDB, c++]
---

I'm proud user of Raspberry PI. I had been waiting for it about 5 months
but at last I got it. If you don't know what Raspberry Pi is I can recommend
[this video](http://youtu.be/u4THiC5-JZo).
Leader of this project will tell you why and how it was build.
I haven't got time to play with it before, but for
me it's really amazing that for only $35 I got working machine that supports
HD films. I spent some time testing it and it works just great. Maybe it's not
so fast and require rather patient user but IMO it's great chance for popularize
free and open software, and show that programming could be fun.
From geeks perspectives rPI is just cheep computer that they can hack
without spending money on it. And as you probably see rPi is used everywhere.

Here are steps to install [MongoDB](http://www.mongodb.org/) on device

    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get install build-essential scons libpcre++-dev xulrunner-dev libboost-dev libboost-program-options-dev libboost-thread-dev libboost-filesystem-dev
    git clone https://github.com/skrabban/mongo-nonx86 --depth 1
    cd mongo-nonx86/
    scons &
    sudo scons --prefix=<where/you/want/install/it> install &
    sudo mkdir /data/db -p
    sudo <where/you/want/installed/it>/mongod --fork --logpath /var/log/mongodb.log

Compiling process could take couple hours so it might be reasonable to run `scons` in
using `nohup` or detach session with `screen`.

To check if it's running call `tail -f /var/log/mongodb.log`. You should see
similar line

    [initandlisten] MongoDB starting : pid=20182 port=27017 dbpath=/data/db/ 32-bit host=<hostname>
