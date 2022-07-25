---
lang: en
layout: post
title:  "Export TECPLOT result file from WELSIM"
date:   2018-06-15
author: "[SimLet](https://twitter.com/getwelsim)"
---


Tecplot is a versatile data analysis and visualization software. Tecplot can display from 2D curves to complex 3D dynamic contours. It features a quick and easy conversion of large amounts of data into easy-to-understand images such as contours, vector maps, grids, sections, streamlines, and more. In the field of finite element analysis, Tecplot is widely applied for post-processing of various computing results. Due to its long history and rich features, Tecplot’s file format becomes almost an industrial standard for result data.

<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*iUzyeQUJPvkG4II09Xb1nQ.png"/>
</p>

In WELSIM v1.8, the user can output the result data to a file in Tecplot format. With this feature, the user can save the complex data into a file, but also implement more complex data post-processing. Let’s take a look at how to apply this feature.

In a project that has been solved, the user can display result contour in WELSIM. This analysis is a multi-body transient thermal analysis.

<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*vGqrbNa7cLug_le58wMJjg.png"/>
</p>

Note that the value of Set Number property in the result object at this time is 100, so the export result is based on the data of the number 100 set.

<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*g0_OMXvu5SNli5pRAdOMpQ.png"/>
</p>

Right-click on the result object and the Export Results option will be displayed in the pop-up menu.

<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*B5rn-STSQ_daEFh0h3DwbA.png"/>
</p>

Click Export Result to bring up the file saving dialog. In the saving dialog, select the Tecplot format (*.tec) and define the file name.

<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*1FzkW8_JrKrjPR_FIWC3Og.png"/>
</p>

The output file is opened as shown in the figure and can be recognized to be the finite element result format of Tecplot.

<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*5nzYbk8Hch3to7CojazOWg.png"/>
</p>

Since the output file is in Tecplot format, we strongly recommend you use Tecplot software to read the file. If your computer has not installed Tecplot yet, you can use the open source packages such as VisIt or ParaView to open the files.

Open and display this result file in the VisIt.

<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*AzUTVGQqkuJobYi2LOooNA.png"/>
</p>

Open and display this result file in the ParaView.

<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*1TEa1y-ILSfeoUWFM312cg.png"/>
</p>

Users can perform more complex operations and data extraction in these post-processing software programs, with the generated result files.

If you have any suggestion or comment for WELSIM, please visit [https://welsim.com](https://welsim.com) and leave a message.


