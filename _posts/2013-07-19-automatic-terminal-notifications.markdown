---
layout: post
title:  Automatic terminal notifications
date:   2013-07-19
categories: terminal
comments: true
---

I spend most of my day staring at either vim or terminal. Often I have to execute some command that 
takes a few seconds. I quickly jump to my browser to see if there is some update on Hacker News 
(I have an OCD), only to realize a few minutes later that I was supposed to be working.

So I thought a healthy nudge (read notification) once this longish running command finishes, will be
a lot of help. So I basically added hooks to my zshrc, to time every command and send a notification
if it runs longer than a few seconds. Here it is:

{% highlight bash %}
# Giving initial value so that terminal doesn't cry on launch
start_time=$SECONDS

function timer_start {
  threshold_time=10
  start_time=$SECONDS
  cmd=$1
}

function timer_stop {
  execution_time=$(($SECONDS-$start_time))
  if [[ $execution_time -gt $threshold_time ]]; then
    send_notification
  fi
  start_time=$SECONDS
}

function send_notification {
  elapsed_time="${execution_time} secs"
  terminal-notifier -title "Finished" -subtitle "elapsed time ${elapsed_time}" -message "${cmd}"
}

# Load required functions.
autoload -Uz add-zsh-hook

add-zsh-hook preexec timer_start
add-zsh-hook precmd timer_stop
{% endhighlight %}
