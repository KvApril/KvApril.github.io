---
layout: post
title: "Git_Mac tab自动补全git命令"
date: 2018-03-03
description: "Git_Mac tab自动补全git命令"
tag: Git
--- 

### 下载git-completion

```
curl https://raw.githubusercontent.com/git/git/master/contrib/completion/git-completion.bash -o ~/.git-completion.bash
```

### 编辑~/.bash_profile 
```
if [ -f ~/.git-completion.bash ]; then
  . ~/.git-completion.bash
fi
```

### 重启~/.bash_profile

```
source ~/.bash_profile
```

