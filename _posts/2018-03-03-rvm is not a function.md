---
layout: post
title: "ruby_rvm is not a function"
date: 2018-03-03
description: "ruby_rvm is not a function"
tag: Ruby
--- 
### 错误信息

```
RVM is not a function, selecting rubies with 'rvm use ...' will not work.

You need to change your terminal emulator preferences to allow login shell.
Sometimes it is required to use `/bin/bash --login` as the command.
Please visit https://rvm.io/integration/gnome-terminal/ for a example.
```


```
$ source ~/.rvm/scripts/rvm
$ type rvm | head -n 1

```


参考链接：[https://stackoverflow.com/questions/14289217/im-getting-rvm-is-not-a-function-error-on-mac-os-x-and-no-posted-solutions-w](https://stackoverflow.com/questions/14289217/im-getting-rvm-is-not-a-function-error-on-mac-os-x-and-no-posted-solutions-w)
