---
layout: post
title: "SSH tricks"
description: "Adavnced tricks on SSH"
category: Linux
tags: [ssh,Linux,tunnel]
---
{% include JB/setup %}

Today I have a problem with SSH. I get access to two new servers (let's call them *Obelix* and *Idefix*)
and I want to set up key based login on my local machine (*Panoramix*). It wasn't so easy, because that new server
accept only connections from one server (let's call it *Asterix*) that I also have login account. I wasn't
able to connect to this new server from *Panoramix*. I need to log in to *Asterix* and then to *Obelix* or *Idefix*.

First of all. I try to log from *Panoramix*. OK, it works but with password. I do my usual routine of pushing
public key to remote server


	cat ~/.ssh/id_rsa.pub | ssh janisz@panoramix "mkdir ~/.ssh; cat >> ~/.ssh/authorized_keys"


but still I wasn't able to connect without password. I try to use `ssh-add id_rsa`  but it returns following error
> Could not open a connection to your authentication agent.
you need to run `ssh-agent bash` and then `ssh-add id_rsa`

Basically my `ssh-agent` didn't know which shell should use. I just told it to use `bash` with `ssh-agent bash`
then I was able to `ssh-add id_rsa` and login without password. Only one thing that was wrong every time I log into
*Asterix* I need to call this 2 lines before I can login on *Idefix* or *Obelix*. For me that was unacceptable.

To solve this problem I could add above 2 instructions to `bash.profile` but I didn't go that way. Instead of this
I use technique of creating SSH Config file. In this file you can specify
your remote host address, port, user name and I believe all other required information including identification
file path. I create configuration file `~/.ssh/config` and fill it with following content

	Host obelix
		HostName obelix.domain.pl
		User janisz
		IdentityFile ~/.ssh/id_rsa
	Host idefix
		HostName idefix.domain.pl
		User janisz
		IdentityFile ~/.ssh/id_rsa

This solution is nice because I can log in with simple `ssh obelix` and also it allow me to easy manage my
keys and use different for every server.

But this was not the finial step. I was able to log on *Obelix* without password but I need to log on *Asterix* and
from it log on *Obelix*. Not good enough for me. To allow me use one line connection I create SSH tunnel between my
 local *Panoramix* and *Asterix* using

	ssh -f -L 2022:obelix.domain.pl:22 asterix -N
	ssh -f -L 2023:idefix.domain.pl:22 asterix -N

What that magic lines do? They just connect localhost port 2022 with port 22 on *Obelix* but
connection is bypassed by *Asterix*. I put these 2 lines in `/etc/rc.local` to create tunnel on system startup.
Now I can log on *Obelix* from my local machine with `ssh janisz@localhost -p 2022`. Next steps are already
described above. I pushed keys to *Obelix* and *Idefix* and add SSH configuration. This time including port

	Host Obelix
		HostName localhost
		User janisz
		Port 2022
	Host Idefix
		HostName localhost
		User janisz
		Port 2023

And that's all. Now I can log using simple `ssh Obelix` on my local machine.

To help you understand the process here is small glossary
* *Panoramix* - my local machine
* *Asterix* - remote server trusted by Idefix and Obelix
* *Idefix*, *Obelix* - new servers that allows connection only from Asterix

In other words *Obelix* and *Idefix* can talk only with *Asterix* who can talk with anybody (e.g *Panoramix*)
