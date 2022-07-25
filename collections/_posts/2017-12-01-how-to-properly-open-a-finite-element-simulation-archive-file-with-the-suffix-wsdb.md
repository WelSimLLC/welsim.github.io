---
lang: en
layout: post
title:  "How to properly open a finite element simulation archive file with the suffix “wsdb”"
date:   2017-12-01
author: "[SimLet](https://twitter.com/getwelsim)"
---

The workload of finite element analysis is relatively large. Engineers will add many settings and variables in the analysis process. If these settings are not saved, such as a sudden power outage, then a lot of content is gone, and engineers have to reset all the analysis steps and details. Therefore, it is very important to archive and load simulation files. At the same time, the well-established simulation analysis work is preserved, and later it can be opened for analysis or review, which can save a lot of time and improve our work efficiency.

The file with the suffix “wsdb” is the archive file of the general-purpose simulation software WELSIM. It is the acronym for the full name WelSim DataBase. The user can save all simulation settings in the file and open the file later to restore all previous analysis settings and steps. Enable engineers to reduce a lot of repetitive operations.

At the same time, wsdb files can be opened in different hardware and WELSIM versions, and can also be read under different operating systems. It can be said to be truly portable. Let us now understand how to open the wsdb file.

After opening the main interface of WESLIM software, we can see that there is an open file icon in the toolbar.

<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*DwcG7UTmFtWHWZDrn3gS5w.png"/>
</p>

Or you can see the “Open” menu option in the menu bar

<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*EbFpHiqMTO0HdPOVDKl88g.png"/>
</p>

Click on the option or icon, the system will pop up a dialog to select the wsdb file, as follows:

<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*Ml5p417jqeQUBay0PTCAtw.png"/>
</p>

Select the file to open, for example here we select the archive file named “structural_static_stand_v16_01.wsdb”.

Soon, the system will automatically read the contents of the document and generate the corresponding analysis settings, and the geometry is automatically imported. As shown below:

<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*9cwPPLgXIso1cjh3qmuqrA.png"/>
</p>

If the archive file was already set up before, then just click the solver button (yellow lightning) to quickly calculate and get the result. For example, the calculation result of this file is as follows:

<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*xZd0SQq33fTcjVdWq_Az2w.png"/>
</p>

<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*PYqdtZxZdCXtqq-VX9qP0A.png"/>
</p>

Is it convenient and quick to read the wsdb file? Next we look at how the wsdb file is saved. Saving file is also very simple, just click on the “Save” button on the toolbar, or the “Save” option on the menu bar, you can save all essential contents to the file.

<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*J307pnGZm-mKCCmTJT5LRQ.png"/>
</p>

<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*X0J7rqU2gUZ2XiaD8fWGbw.png"/>
</p>

Now with the feature of saving and reading the archives, do you still concern about power failure when using WELSIM?

