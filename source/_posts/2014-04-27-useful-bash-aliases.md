---
layout: post
title: "Useful Bash Aliases"
date: 2014-04-27 16:49:24 -0400
comments: true
published: true
tags: ['linux', 'bash', 'aliases']
---

Over the years I've accumulated a lot of useful aliases for my Bash shell. I rarely see others using many aliases, so I thought I'd share mine. This list can get somewhat long, so I recommend putting these in a `.bash_aliases` file and sourcing it from your `.bashrc` with:

``` bash
[[ -f ~/.bash_aliases ]] && . ~/.bash_aliases
```

Any content surrounded by angled brackets (`<>`) are machine/user specific, so don't forget to replace them with the correct values.

``` .bash_aliases
# ls aliases
alias ls='ls --color'
alias ll='ls -lh --color'
alias la='ls -lA --color'
alias l='ls'

# safe file management
alias cp='cp -iv'
alias rm='rm -i'
alias mv='mv -i'

# quick directory movement
alias ..='cd ..'
alias ...='cd ../..'
alias ....='cd ../../..'

# go to the last directory you were in
alias back='cd $OLDPWD'

# display numbers in a human readable format
alias df='df -h'
alias du='du -h'
alias free='free -h'

# copy the current working directory to the clipboard
alias cpwd='pwd | xclip -selection clipboard'

# quickly find files and directory
alias ff='find . -type f -name'
alias fd='find . -type d -name'

# get internet speed
alias speedtest='wget -O /dev/null http://speedtest.wdc01.softlayer.com/downloads/test500.zip'

# get external ip
alias extip='curl icanhazip.com'

# quickly source the .bashrc file
alias srcbash='. ~/.bashrc'

# tail any apache/php error files
alias tailall='tailf /var/log/httpd/<my-website>-error_log'

# git number aliases (https://github.com/holygeek/git-number)
alias gn='git number'
alias ga='git number add'

# change the current directory to the parent directory that contains the .git folder
alias git-root='cd "`git rev-parse --show-toplevel`"'

# print the path with each directory separated by a newline
alias path='echo -e ${PATH//:/\\n}'

# list the name of the process matched with pgrep
alias pgrep='pgrep -l'

# make less properly handle colored output
alias lessr='less -R'

# open any file in GNOME from the command line
alias gopen='gvfs-open'

# start programs quietly
alias gdb='gdb -q'
alias bc='bc -ql'

# adb logcat aliases
alias logcat-sys='adb logcat -s System.out:D'
alias logcat-e='adb logcat -s *:E'

# key management aliases: fingerprint a pubkey and retrieve pubkey from a private key
alias fingerprint='ssh-keygen -lf'
alias pubkey='ssh-keygen -y -f'

# display hexdump in canonical form
alias hd='hexdump -C'

# print the current time
alias now='date +%T'
```

Got any other good aliases to add? Let me know in the comments, and I'll add them to the list.
