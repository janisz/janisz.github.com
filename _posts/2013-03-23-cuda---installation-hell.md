---
layout: post
title: "CUDA   installation hell"
description: "CUDA fo Fedora 17 installation guide"
category: "GNU/Linux" 
tags: [CUDA, gnu, linux, Fedora]
---
{% include JB/setup %} 	 


[CUDA](http://www.nvidia.pl/object/cuda_home_new_pl.html) will be definitely one of the most groundbreaking technology this decade. For few years it’s get thousands of followers. GPU computing ([GPGPU](http://en.wikipedia.org/wiki/GPGPU)) is involved nearly everywhere from OLAP cubes to medical imagining. Nowadays nearly every nVidia card support CUDA so it’s best time to try it.


But hold on. Does it support GNU/Linux? Yes and no. nVidia supports only main stream distributions and only in specified releases. I’m using [Fedora](http://fedoraproject.org/pl/) 17 but only Fedora 16 is supported by nVidia. So here is step by step instruction how to set up CUDA Toolkit on Fedora 16 but I believe it will works for latest releases too.


1. Check if your card supports CUDA

		sudo /sbin/lspci -v | grep -A 16 VGA

	or if you already have nVidia tools installed `nvidia-settings`

2. Install proprietary driver. CUDA will not working with any other driver. And what’s worst nVidia close source of their drivers so nobody know how it really works. IMO best comment on this is [Linus Torvalds](http://youtu.be/IVpOyKCNZYw?t=1m45s)

	To install proprietary driver you should go [here](http://www.geforce.com/drivers) and choose your card and system. Once you download it go to text mode `sudo init 2` and `sudo ` and reboot after installation.

3. Download [CUDA 5.0 Toolkit](https://developer.nvidia.com/cuda-downloads) and install it but without driver (you already did it). CUDA toolkit supports only GCC in 4.6 or lower so launch it with `-override compiler`

4. Afretinstallation change one assertion in `/usr/local/cuda-5.0/include/host_config.h` in line 80. Just fix

		#if __GNUC__ > 4 || (__GNUC__ == 4 && __GNUC_MINOR__ > 6)

	to proper GCC version	

5. It should be working right now however if you get following error

		error: identifier "__atomic_fetch_add" is undefined

	you might need to undefined two statements that GCC define

		#undef _GLIBCXX_ATOMIC_BUILTINS
		#undef _GLIBCXX_USE_INT128


	It should be put as a first line in all .cu file although you can put these lines in one  file and tell `nvcc` to include it at first scan `--pre-include /path/to/the/file.h`
