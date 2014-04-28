---
layout: post
title: "Useful Git Tips"
date: 2014-04-27 17:46:22 -0400
comments: true
published: false
tags: ['git']
---

I've noticed that when it comes to Git tutorials, there's only the "Intro to Git" or the "Here's how you do X with Git", but there aren't any tutorials that take you from a Git beginner to a Git master. This post is supposed to be a starting point for that. It will provide some useful tips and concepts that I use everyday, which allows me to use Git to the fullest extent. For anyone who's interested in learning more, definitely check out the [Pro Git](http://git-scm.com/book) that's freely available online. I've read that book from beginning to end and I've found it very interesting and educational.

Note that this tutorial requires basic knowledge of Git. That is, you should know what Git is, how to add, commit, and push changes, and the very basics of branches and merging.

## Git Number

The first tip I'd recommend is to get [Git Number](https://github.com/holygeek/git-number). Git Number saves a ton of time when doing anything with Git. Instead of typing `git status`, try typing `git number status`, type `git number status`. You'll see the same output you'd normally see but with numbers in front. Now to perform any operation on a file, you just need to use it's corresponding number. So instead of typing `git add the/path/to/this/file/is/so/long.txt`, you'll just be able to type `git number add 1`. Note that this works on any git command that requires a file name, so it'll work with commands like `git rm` and `git checkout` too. Where git number really shines is it's ability to do operations on ranges. For example, you could run the command `git number add 1-3,5,8` to add the files 1, 2, 3, 5, and 8, but leave all other files unmodified.

If you've read my [useful Bash aliases](/posts/useful-bash-aliases) post, you'll see I have two aliases for `git number` that you might find useful:

alias gn='git number'
alias ga='git number add'

## .gitconfig and Aliases

Git allows you to have aliases apart from Bash aliases. These aliases can be added in your `.gitconfig` file which should be located in your home directory (go ahead and make one if it's not there for some reason). You can also set colors in your `.gitconfig` which makes the output of `git status` or `git diff` more readable. Here's my full `.gitconfig` file:

``` ini .gitconfig
[user]
	name = Gulshan Singh
	email = gulshan@umich.edu
[color]
	diff = auto
	status = auto
	branch = auto
	interactive = auto
	ui = true
	pager = true
[color "status"]
	added = yellow
	changed = green
	untracked = red
[core]
	pager = less -FRSX
	whitespace=fix,-indent-with-non-tab,trailing-space,cr-at-eol
	editor = /usr/bin/emacs
[alias]
	st = status
	ci = commit
	co = checkout
	w = whatchanged
	amend = commit --amend --no-edit
[push]
	default = upstream
```

The config is for the most part self explanatory. If you haven't used the `whatchanged` or `amend` commands, I'd recommend looking them up. They're useful commands to know and we won't be covering them here. You also might be interested in looking up the options for the `push.default` setting. Giving this setting a value of `upstream` will push all branches that exist both on your local git repo and on the remote git repo (these branches are known as "tracked" branches). This means that you can type `git push` instead of `git push origin master`.

## git log

I hope that you have encountered `git log` by now, because it's a necessary command to use Git effectively.

* gitk
* git stash
* rebasing vs merging vs fetching
* git reflog
* git checkout vs reset
* git log
* git cherry-pick
