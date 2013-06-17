---
layout: post
title: "Build Server Installation"
---

There is unfortunately no easy way to build firmwares and packages for the Link at this time. This section will, however, describe how
to do it the hard way (and the way KIPR does it internally). The Link is based off of a linux distribution system called *OpenEmbedded*
and its associated build system called *bitbake*. While these tools have improved dramatically in recent months and years, the Link's
build system has not been updated yet. As such, there will be little to no relevant documentation available to assist in the creation
of packages or firmwares, and most software available in OpenEmbedded's local repository will be outdated. Fortunately, KIPR has shed 
most of the tears of frustration on the reader's behalf. What follows is a guide on setting up a build server and modifying pieces of 
KIPR's software.

Prerequisites
=============

***These instructions require a good amount of experience with linux and distributed version control systems. If you haven't had
any experience with those, it is recommended you gain knowledge of them *before* rather than *during* this process.***

The following software and hardware is necessary for setting up a Link-compatible OpenEmbedded build server (herein referred to as *the host*):
	
	
- A computer or virtual machine running a *clean install* of the latest Ubuntu Linux. This computer or virtual machine must have:
	- At least 150 GB of free space (though 300 GB or more is preferred).
	- At least 4 GB of RAM. KIPR uses 16 GB of RAM.
	- At least a quad-core CPU. KIPR uses a six-core AMD CPU, but a newer Intel quad-core chip would probably be more performant.
	- A broadband internet connection.
- Knowledge of the `git` version control system.
- Fluent in basic and moderately complex linux terminal commands.

Once Ubuntu Linux has been installed on the host, install the necessary packages for OpenEmbedded: `sudo apt-get install git subversion binutils`


***Insert Clemens' instructions once they are ready***

Core Concepts in OpenEmbedded and `bitbake`
===========================================

OpenEmbedded organizes build *recipes* into "meta" *layers*.  ***Write More.***

Modifying an Existing Package
=============================

First, change the working directory to `oe` using `cd oe`. Once inside the `oe` directory, source in the build
environment using the command `. ~/.oe/environment-oecore`. This step must be done every time a new terminal is used.

To tell bitbake to pull new code from a given package's repository, the PR version of the package must be incremented. For example,
to increment the PR version of botui using vim, one could do the following:

`vim sources/meta-kipr/recipes-kovan/botui/botui_git.bb`
Then enter the characters: `?`, `P`, `R`, `[Return]`, `Ctrl-A`, `:`, `w`, `q`, `[Return]`.

Vim is an advanced text editor that can be used to modify files in a terminal. The first part of this command is `?PR[Enter]`.
This tells vim to find the first occurrence of the string "PR" in the text file and move the cursor to it. `Ctrl-A` tells vim to
find the next integer (in this case the PR number) and increment it by 1. Finally, `:wq[Return]` tells vim to write its changes to disk
and then quit.

Now, rebuild the package using `bitbake botui`.

If this command completes successfully or with only warnings, congratulations! An installable package file was created
and deposited in the `build/tmp-*/deploy/ipk/armv5te` directory! For installation instructions, see the section
documenting `opkg`.

A Custom Package
================

Debugging Bitbake Errors
========================
Bitbake will sometimes simply fail with a message containing the word "ERROR". Since there are thousands of things "ERROR" could
mean, this will often leave the developer scratching their heads in frustration. I have discovered, however, that most of these "ERROR"
messages with zero information are often the result of a syntax error in a `.bb` package file. As such, it is strongly recommended
that developers incrementally test changes to their `.bb` files. If that doesn't help, the developer will need to go through their
recently modified `.bb` files and temporally remove them from the repository to check if that file is indeed the problem. Once the
problematic file has been identified, comment out portions of the file to determine wherein the error lies.

Installing Packages and Building Firmwares
==========================================

OpenEmbedded will automatically generate package files that are installable on the Link using a flash drive and terminal. ***Write More.***