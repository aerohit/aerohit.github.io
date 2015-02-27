---
layout: post
title:  Out of source linux kernel build
date:   2013-09-03
categories: linux
comments: true
---

I recently had to make a few changes to the kernel and do an out of source build of the same.
I had to read multiple articles to finally figure out the correct way. The steps are documented
here. I had tested this with version 3.2.50 of the kernel.

{% highlight bash %}
$ cd <kernel_source_directory>
$ make O=/tmp/custom_kernel menuconfig
$ make O=/tmp/custom_kernel -j5
$ make O=/tmp/custom_kernel INSTALL_MOD_PATH=/tmp/custom_kernel modules_install
$ sudo make O=/tmp/custom_kernel INSTALL_PATH=/tmp/custom_kernel install
{% endhighlight %}
