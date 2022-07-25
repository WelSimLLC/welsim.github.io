---
lang: en
layout: post
title:  "Install finite element analysis software WELSIM on your Linux OS"
date:   2018-03-30
author: "[SimLet](https://twitter.com/getwelsim)"
---

WELSIM has released the Linux version at the March of 2018, the first supported distributions are Ubuntu 16.04 and Fedora 27. Today I will show you how easy to install WELSIM on your Linux OS.

1.Download the latest copy of Linux version from the website of https://welsim.com, Open a terminal window and browse into the directory that contains the installer file, and type the command below. These two-line command is trying to make the installer file to be executable, and run the installer successively.
$ chmod +x WelSim15Setup.run
$ ./WelSim15Setup.run

2.Soon, you will see an installation wizard windows pops up.


<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*KQQmbbXYmt2rM29SBGw3yw.png"/>
</p>

3.Click the ”Next” button. You are asked to input the installation directory, you could just use the default path as shown in the text field.

<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*W8Yrk0o-CEqbHCNGFmzhdQ.png"/>
</p>

4.After clicking “Next” button, you will be asked to choose the modules to install. Here the “WELSIM” has been selected by default settings.

<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*YOz1NPnrnAKCpf25Iyo2kA.png"/>
</p>

5.After review the licensing agreement, you could simply click the “Next” button to proceed.

<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*y-0ruLSkJgq-uUI4vwRqYg.png"/>
</p>

Before installing the package, you will be asked to confirm the module and size of the installation.

<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*zfQvmUFlxI3nDTHrfXrgVw.png"/>
</p>

In a few seconds, the installation is completed.

<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*fG1ApIrmSS6WSZVl5S9IvA.png"/>
</p>

After installation, you could browse into the installation folder in the terminal window, and type in the commands below.
`$ chmod +x runWelSim.sh`
`$ ./runWelSim.sh`

Now you can see the graphical user interface of WELSIM, smoothly running on your Linux OS.

<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*HhCtKMR2x8fTgr4FUcdwLA.png"/>
</p>

It looks like installation WELSIM on a Linux OS is very easy and straightforward.


