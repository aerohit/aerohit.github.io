---
layout: post
title:  Note taking with Vim and Dropbox
date:   2015-02-28
categories: vim
comments: true
---

I code on my personal machine, my work machine and on my DigitalOcean Droplet.
I wanted a way to take notes which met the following criteria:

+ Should be simple and non-distracting
+ Works on a local as well as a remote machine
+ Keeps the notes in sync, irrespective of where I take them
+ And it should be Vim

So here is my solution. Install the [vim-notes](https://github.com/xolox/vim-notes)
plugin for Vim. It's an incredibly good tool for taking notes. Create a directory
inside ~/Dropbox (or whatever location you use for your Dropbox) and specify
it as the location for storing notes.

{% highlight vim %}
" vim-notes
let g:notes_directories = ['~/Dropbox/Notes']
nnoremap <leader>on :tabnew<CR>:Note<Space>
{% endhighlight %}

I have also created a mapping for quickly accessing the notes.

To keep the notes in sync is easy on my machine, I only need to do a normal installation of Dropbox.
For the remote node, I did a [headless install](https://www.dropbox.com/install?os=lnx).
To make make sure that the Dropbox daemon starts on boot, I created a cron job:

{% highlight bash %}
$ crontab -e
{% endhighlight %}

and then put the following entry in it:

{% highlight bash %}
@reboot ~/dropbox-dist/dropboxd
{% endhighlight %}

And Voila, I can just hit `<leader>on` to access notes from anywhere, without
leaving my trusted mate, Vim.
