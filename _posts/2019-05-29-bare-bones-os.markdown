---
layout: post
title: Bare Bones OS
date: 2019-05-29 6:44:59 -0500
categories: Programming 
---

Upon completing my Systems Programming I & II courses (CSE 220 and CSE 320 at Stony Brook University respectively) this past academic year I have learned that I actually enjoy this field.
Although these two courses are notoriously known as the "hardest courses" in the entire major, with half decent time management skills, I felt that they were not as bad as people make it seem. 
But, I would be lying if there weren't parts of the courses that I absolutely dreaded (ALUs).
These two courses have inspired me to continue my education in systems programming which is why I started building my own operating system.
I will be following the Bare Bones tutorial on OSDev https://wiki.osdev.org/Bare_Bones 
<br>
# The Cross Compiling Nightmare
This was easily the most frustrating thing I have ever done.
In order to begin developing a custom OS, we need to build a cross compiler.
The purpose of this tool is to be able to compile files with the correct target platform.
A piece of code that gets compiled for x86_64 gets compiled differently than for i686.
Our target cpu will be i686-elf.
Initially, I followed this tutorial: https://wiki.osdev.org/GCC_Cross-Compiler
And My God. 
I ran into problem after problem whether it would be a verisoning issue, missing files, or this `cannot compute suffix of object files` error. 
In short, setting up my own gcc cross compiler kicked my ass and I decided to download a prebuilt one: http://newos.org/toolchains/i686-elf-4.9.1-Linux-x86_64.tar.xz
After untaring my brand new shiny cross compiler I set up a few aliases so that
running the executables were easier to type out.

# Booting the Kernel
The rest of the Bare Bones tutorial is very clear about what to do to get a minimal OS up and running.
By the end of the tutorial I had my operating system running: OculuS
![OS-OculuS]({{site.url}}/{{site.baseurl}}/assets/img/OS-OculuS.png)
