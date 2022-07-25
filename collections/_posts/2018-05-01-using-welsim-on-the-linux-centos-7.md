---
lang: en
layout: post
title:  "Using WELSIM on the Linux CentOS 7"
date:   2018-05-01
author: "[SimLet](https://twitter.com/getwelsim)"
---

WELSIM v1.7 recently announced the support of the CentOS 7 operating system, which is followed by the previously supported Ubuntu and Fedora Linux distributions. CentOS and RedHat users can use WELSIM directly for finite element analysis, while cloud computing users can quickly deploy WELSIM on the CentOS server in the cloud.

Now let’s see how to download, install, and use WELSIM on CentOS 7 for engineering simulation analysis.

Download the latest WELSIM CentOS 7 version from website https://welsim.com.


<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*evq9P5_WoS2ShBd5Fr4_BQ.png"/>
</p>


After the download is complete. In the folder where the downloaded file is located, right-click on the blank area and select Open in Terminal from the pop-up context menu.

<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*wbN_nwuzpFXl1DxBkyWkzQ.png"/>
</p>


At this time, the system will pop up the terminal window and the working path is the current directory. Enter the following command in the console
`$ chmod +x WelSim17SetupCentOS7.run`
`$ ./WelSim17SetupCentOS7.run`

As the picture shows:

<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*q7tpBDdz1tbYDytU4xAkiQ.png"/>
</p>

You will immediately see a graphical installation wizard window on your screen.

<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*Q0SkIcC2-aRpcieR3PQHxA.png"/>
</p>

Click Next, and you will be prompted to enter the installation path. You can use the default installation path.
<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*1_TIIFj_l0StKTxDR7-iaQ.png"/>
</p>


After clicking Next, you will be prompted to select the module. WELSIM is a complete CAE simulation solution framework. You can keep the default setting and click Next.
<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*OoZf_VfPmFxpW7W5qZqzpw.png"/>
</p>

At this time, the installation interface prompts that the installation will occupy 423.99M of hard disk space. If you confirm that the computer space is sufficient, click Install.
<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*S4rSzCONJu1nFTePWE8lyg.png"/>
</p>

After a few seconds, the installation is complete.
<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*eyH1IbKMuFTnZ0VbmNrddQ.png"/>
</p>


Click Next, and you will see the installation completion confirmation.
<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*bzVjubbfH9drLN3-dZYJbw.png"/>
</p>

Since WELSIM’s visualization module requires some dependent libraries such as libGL, libGLU, etc. At running WELSIM for the first time, you may need to install those libraries. The command below can install the necessary libraries to your system. 
`$ sudo yum update`
`$ sudo yum install mesa-libGLU mesa-libGL`

as the picture shows:

<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*3F3cubrVkqVvmshY36q21g.png"/>
</p>

Next, open the installation directory and select Open in Terminal from the context menu as shown in the figure below.

<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*tSjAlolYLP5Q5dbEA2F9TQ.png"/>
</p>

Type the command below to the terminal window:

`$ chmod +x runWelSim.sh (Only need at running for the first time)`
`$ ./runWelSim.sh`

<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*MDn0NQx4QrZ6A7N-g1TwUg.png"/>
</p>

At this time, the main interface of the software will start, as shown below.

<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*0i-60P4ygXU_9Q9YUfhT0A.png"/>
</p>

Now let’s set the analysis type to steady-state thermal analysis and import a geometric model. As the picture shows:

<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*_89SRfJ4yWmwAVq6twRLfw.png"/>
</p>

Set to use the quadratic element and implement the meshing. You can obtain the generated mesh as shown:

<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*C4-gPbDlqmYROrktm6R10w.png"/>
</p>

Define the relevant boundary conditions as shown below.

<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*kfTlhkPSTvHRteRuTvyMQg.png"/>
</p>

After calculation, you can evaluate the temperature result and plot the contour as shown in the figure.

<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*T_C70LCuF3j07jIsYKhmbQ.png"/>
</p>


The analysis is complete. Save the project as a *.wsdb file, which can be opened on this machine or other computers later. The *. wsdb files saved in the CentOS version can also be resumed in other Linux distributions or Windows versions.

More about using WELSIM on Linux, you can visit https://welsim.com/linux, or leave us a message.





