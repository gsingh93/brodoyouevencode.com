---
layout: post
title: STS Level 1
date: 2013-06-10 08:19
comments: true
categories: 
---
We start the level by SSHing into the STS IO server,

   ssh -p2224 level1@io.smashthestack.org

<!--more-->

The password is `level1`. We start off in the `/home/level1/` folder. If you read one of the README files (`less README`, `vi README`, or `cat README`), you can read about how the wargame works. In short, you start off on level 1 and try to exploit the applications in the `/levels` directory. If you can exploit them and get the password needed to run the application, you'll have an effective user id as the next level (this works using [setuid](http://en.wikipedia.org/wiki/Setuid) access rights; you can run `ls -l /levels` and see that the executable byte of the owner permissions is set to an 's' instead of an 'x'). With a higher effective user id, you can go to that users home directory and access the .pass file, which contains the password for the next level. Then you can SSH in as that user using this password.

There really aren't any tricks to level one. If you don't have prior experience with Linux or with these types of challenges you're out of luck. Start of by running the level01 application to see what happens,

	  level1@io:/levels$ ./level01
	  Usage: ./level01 <password>

To get the password, run the command

   level1@io:/levels$ strings level01

and look at the output. The string command outputs all of the printable characters from files, including executables. You'll see the obvious password, `omgpassword`. Now run the program again with this password,

	level1@io:/levels$ ./level01 omgpassword
	Win.
	sh-4.1$

You'll see a bash prompt. If you type `id` you can see that your effective user id is now level2. The next step is to increase your real user id. Go to /home/level2 and run `cat .pass`. I've put the password below
WE5aVWRwYPhX
