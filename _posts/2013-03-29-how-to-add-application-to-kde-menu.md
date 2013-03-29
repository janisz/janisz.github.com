---
layout: post
title: "How to add application to KDE Menu"
description: "Short tutorial about adding custom application to KDE Menu"
category: "GNU/Linux"
tags: [Fedora, linux,  Feodra, gnu]
---
{% include JB/setup %}

<img style="float: right; width: 22%; height: auto;" src="/assets/images/kde_menu.png" alt="KDE Menu">

Lots of java applications are not in repositories of popular GNU/Linux distros or the version are not up to date. You can install them just by unpacking in desired folder and sometimes setting some properties. How to make them accessible from KDE Menu?

I'll show how to achieve it on Fedora 16.


1. Go to `/usr/share/applications`
2. Create text file with name in format `[application_name].desktop`
3. Fill it with properties. Here is my example for [IntelliJ](http://www.jetbrains.com/idea/)


		[Desktop Entry]
		Type=Application
		Name=IntelliJ
		Comment=InelliJ IDEA CE
		Icon=/opt/idea-IC-123.123/bin/idea.png
		Exec=/opt/idea-IC-123.123/bin/idea.sh
		Terminal=false
		StartupNotify=true
		Categories=Development;IDE;Java;

Probably you might need superuser acces to add your custom entry to KDE Menu.
