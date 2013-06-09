---
layout: page
title: Gulbuntu OS
comments: true
sharing: true
---
### Description

I wrote this basic operating system back in high school and it was honestly one of the most interesting and educational things I've ever written. I'm a much better programmer now, so I'm going to be revisiting this project soon in the hopes of making it into a fully functional OS and creating a tutorial on how to do it. For those of you who can't wait, you can find a lot of good information at OSDev. The OS functionality is very simple: there's no filesystem, and the only commands are help and cls (clear screen). Don't let that fool you though; taking a look at the code will assure you this was no easy project.

![OS Screenshot](/images/os-screenshot.png)

### How To Run

To run the OS, all you need is Qemu. Although there's no official Windows build of Qemu, there are many ports. The specific port I used is included in the download

Once you have Qemu installed, customize the emulate.sh file to use the correct paths for your system (I'm using a Bash script because I use a combination of Cygwin and Windows for development). If you're using the Qemu files I provided the paths should already be correct Run the bash file (./emulate.sh), and you should see GRUB pop up. Type kernel 200+2880 and hit enter (the explanation for this is on the OSDev Wiki), and then type boot. You can type help for a list of commands (there are only two).

### How To Build

In order to build this OS, you'll need NASM and a custom built GCC Compiler (don't worry if you find that part confusing; it took me a couple tries). There is also a simple python script that gets executed during the build process, so you either need to have python installed and in the system path, or you can port the python script to something else like Bash and then change the compile.sh file. Once that's done, simply download the source and run the compile.sh bash script. You may have to modify the script depending on your custom compiler; it's a pretty simple script, so don't worry.