---
layout: page
title: Compiler
comments: true
sharing: true
---
### Description

This is another project I started back in high school. It's essentially a Python port (from Pascal) of the compiler written by Jack Crenshaw in [this tutorial](http://compilers.iecc.com/crenshaw/). At the moment, the compiler understands basic programming constructs such as if statements and while loops. While I'm fairly proud of this project, I'm planning on writing a much better compiler in the future, and writing a tutorial for it as well.

### How To Run

While I developed the project using PyDev, a plugin for eclipse, you can run the compiler with just Python installed. You also need to install <a href="http://www.nasm.us/">NASM</a>, which assembles the assembly output from the compiler. The linker is included in the download.

Once you have everything installed, [download the source](http://www.mediafire.com/download.php?q1a5mdcxh23d414) and extract it. In command prompt (the linking script is a batch file), type `python compiler.py`. The compiler should run and it will display all the assembly code that's being output as it runs. It will ask you if you want to compile the source from a source file or the code you type. If you compile from a source file, the contents of `code.txt` are compiled and run. You should see the number 7 output in the prompt. Take a look at `code.txt` to see what code was compiled. By default, the value of the variable `x` is printed when the program is finished. The code for a print function is implemented (it's what's used to display the value of x), but there was a reason I didn't add a print keyword that I can't remember. If you chose to compile the code you type, then type something like `a=1`. This will create a variable called `a` with the value of 1. Type something like `x=a+2` and `x` will get set to 3. Type `end` and the code will compile and run. You should see 3 output to the screen.

Here's how the output should look for a simple example:


	   C:\Users\Gulshan\Desktop\Compiler\Compiler>python compiler.py
	   [list -]
	   %include 'win32n.inc'
	   [list +]

	   section .bss use32
	   section .data use32
	   section .code use32
       cpu 386
	   extern WriteFile
	   extern GetStdHandle
	   extern ExitProcess
	   import WriteFile kernel32.dll
	   import GetStdHandle kernel32.dll
	   import ExitProcess kernel32.dll

	   section .code

	   ..start:
	   push    STD_OUTPUT_HANDLE
	   call    [GetStdHandle]                  ;Get stdout
	   mov      [stdout_handle], eax     ;Save the handle

	   Input from file? (y/n): n
	   >>x=2
	   mov             eax, 2
	   mov             [X], eax
	   >>end
	   add             dword [X], 48

	   ;Write a message to stdout
	   push    dword 0
	   push    dword 0
	   push    dword textlen
	   push    dword X
	   push    dword [stdout_handle]
	   call    [WriteFile]
	   jmp             exit

	   exit:
	   push    dword 0                                 ;Point at error code
	   call    [ExitProcess]
	   jmp             exit                                    ;Should never reach here


	   section .data

	   stdout_handle   dd      0
	   string                  dd      0
	   textlen                 equ     $ - string
	   X                       dd 0

	   C:\Users\Gulshan\Desktop\Compiler\Compiler>
	   C:\Users\Gulshan\Desktop\Compiler\Compiler>PATH=C:\Python27\;C:\Python27\Scripts
	   \;C:\OpenCV2.2\bin\;C:\Program Files\Java\jre6\bin;C:\Windows\system32;C:\Progra
	   m Files\Java\jdk1.6.0_25/bin;C:\Users\Gulshan\AppData\Local\nasm;C:\Program File
	   s (x86)\Tesseract-OCR;C:\Program Files (x86)\ImageConverter Plus;C:\Program File
	   s (x86)\ImageConverter Plus\Microsoft.VC80.CRT;C:\Program Files (x86)\ImageConve
	   rter Plus\Microsoft.VC80.MFC;C:\Program Files (x86)\Google\google_appengine\;c:\
	   altera\11.1\modelsim_ase\win32aloem;C:\Motion-Twin\Haxe\;C:\Motion-Twin\neko;C:\
	   cygwin\bin;

	   C:\Users\Gulshan\Desktop\Compiler\Compiler>nasm -fobj output -l output.lst

	   C:\Users\Gulshan\Desktop\Compiler\Compiler>alink\alink.exe -c -oPE -subsys conso
	   le output
	   ALINK v1.6 (C) Copyright 1998-9 Anthony A.J. Williams.
	   All Rights Reserved

	   Loading file output.obj
	   matched Externs
	   matched ComDefs
	   Generating PE file output.exe

	   C:\Users\Gulshan\Desktop\Compiler\Compiler>output.exe
	   2
