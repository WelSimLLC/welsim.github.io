---
lang: en
layout: post
title:  "Export result data in VTK format from WELSIM"
date:   2018-07-01
author: "[SimLet](https://twitter.com/getwelsim)"
---

VTK (Visualization Toolkit) is an open source and object-oriented software system for computer graphics, image processing, visualization. It includes hundreds of algorithms in the field of graphic images and visualization, which can be used across platforms. VTK library allows users to easily create stand-alone large applications by integrating the VTK libraries. Besides, VTK also provides a data format suitable for finite element analysis results.

<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*NGwEv0Sw7bAT8z9yQzeETw.png"/>
</p>

In the WELSIM v1.8 version, the user can output the solved result data as a VTK format file. With this feature, the user can save the complex data into a file, but also implement more complex data post-processing. Let’s take a look at how to apply this feature.

In a project that has been solved, the user can successfully display the resulting contour in WELSIM. This model contains 128,710 nodes and 72,125 Tet10 elements. The result data is relatively large.

<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*OasEOlMHekxtE_j9LN3usQ.png"/>
</p>

Right-click on the result node and the option Export Results will be displayed in the pop-up menu. Clicking on the export result will bring up the file save dialog. The export result is based on the data of Set Number 1.

<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*qJk06eaB3gXel7HDCktGfg.png"/>
</p>

In the save dialog, select the VTK format (*.pvtu) format and give the file name.

<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*hSZljQU5_rW9Zmuv_tRYdA.png"/>
</p>

Two files are output at this time, one file with the suffix *.pvtu and another with suffix *.vtu. Open those files using a text editor, we can tell that the *.pvtu file has a general data description, the *.vtu file contains the specific data.

The *.pvtu file contains a description of the data.

<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*_Txk1Oj0cj_5FarkzUMXwA.png"/>
</p>

The *.vtu file contains the bulk data.

<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*1z2RjaDT_fl8jUucctgnlQ.png"/>
</p>

The VTK format file can be read by the most of post-processing software. Paraview and Visit are free and open source, those two software applications are demonstrated to read the generated result file here.

Open and display this result file in the ParaView.

<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*QNqF26QjEKzvaMn3TL8Q5Q.png"/>
</p>

Open and display this result file in the VisIt.

<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*YspfKGl7pxutqW6_diASrg.png"/>
</p>

If you have any question or comment about WELSIM, please visit [https://welsim.com](https://welsim.com) or leave us a message.
