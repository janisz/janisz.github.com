---
layout: post
title: "FileZilla the best FTP client ever"
description: "Short description of FileZilla killer feature"
category: tools
tags: [FTP]
---
{% include JB/setup %}

<img style="float: left; margin-right: 10px; width: 17%; height: auto;" src="/assets/images/FileZilla_logo.svg" alt="FileZilla logo">

I'm using [FileZilla](https://filezilla-project.org/) since... I've never thought about it. It probably starts
somewhere in primary school. I get it with CD attached to magazine. I have an account on one of
biggest polish portal and keep there my first tries of HTML. As a kid I haven't appreciate this tool. I don't remember
but probably in earliest version it wasn't stable and hadn't got all that features that it has now. But do it's job and
do it well better than command line especially for noobs like me.

Over the time I found better ways of pushing stuff to server (I think SCP is the best) or even making serve automatically
pull updates. Nowadays FTP is endangered protocol it's nearly extinct in it's pure form (I don't count SFTP and FTPS).
Nevertheless sometimes you need to use FTP because some
[werewolf administrator](http://www.codinghorror.com/blog/2010/08/vampires-programmers-versus-werewolves-sysadmins.html)
want to make our life even harder than it have to be and set up FTP as an only _"gate"_ to production.

What's so great in FileZilla? First it's easy. Maybe for me because I used to it but I think it won't be problematic
for any IT related person. Second it's great community. Nearly any question that came up is solved on
[forum](https://forum.filezilla-project.org). Last but not least - highly configurable.

Some time ago I had to put bunch of DB dumps to W$ server to load them on database.
I cannot load them directly from my computer because I can't change DB setting to open for remote connections.
I tried to use RDP but files were to big and upload fails before one file was uploaded. What I did was to create
FTP on IIS (fortunately I've proper permissions) and upload files using FilleZilla. But it didn't went smooth.
I've a problem with connection. I didn't spent time on it since I need it only one and disable FTP on this server.
I goggled the error and immediately found solution on FileZilla forum - _"Turn on Passive Mode"_ (it was easier than
changing configuration).

Another story. I was asked to move PHP CMS - Moodle from one server to another. The problem was that this new server
is managed by really lazy admin, who didn't give me shell account so I'd use `rsync` or just `scp`
to move folders and DB directly from one server to another. Instead of this I have to download DB and files to my local
and upload them to the new server. Nightmare. And I can only use FTP and phpMyAdmin. Uploading DB take me some time.
I need to split dump to smaller files to prevent timeout. But when it goes to uploading files it was even worser.
There were thousands of files. It would take hours to upload them all. Firstly I tried FireFTP, FireFox FTP plug in.
It's nice for small task but this required something more powerful. And again FileZilla saved my skin.

When you go to `Edit` → `Settings` → `Transfers` and change configuration to use maximum simultaneous transfers your
upload get turbo. It really save time when you upload multiple small files.

