---
lang: en
layout: post
title:  "Running OpenGL-based applications in a sandbox/virtual machine"
date:   2025-06-28
author: "[SimLet](https://twitter.com/getwelsim)"
---


Windows Sandbox is a built-in virtual machine in the Windows operating system that allows users to test and run uncertain applications. The sandbox is seperate from the host OS, so applications can run safely in isolation. It is temporary; once closed, all software, files, and states within the sandbox are deleted. Each time the sandbox is launched, a brand-new instance is created. Unlike other virtual machines like VirtualBox, launching Windows Sandbox doesn't require installing or purchasing a separate OS, which is a significant advantage. However, the sandbox is only available on Windows Professional or Enterprise editions.

When running OpenGL-based software in the sandbox, display issues may arise. This is because Windows Sandbox does not natively support OpenGL. If an application depends on OpenGL but does not include the necessary OpenGL libraries, issues can occur such as a missing main interface. For example, MatEditor, a free engineering simulation material editor from the WelSim suite, may not display its main window the first time it is opened in the sandbox. This is because the required OpenGL libraries in the sandboxed OS are absent.

<p align="center">
  <img src="\assets\blog\20250701\welsim_sandbox_mateditor_blank_gui.png" alt="welsim_sandbox_mateditor_blank_gui" />
</p>


The fix is straightforward—simply add the OpenGL libraries to MatEditor.

1.Download the Mesa OpenGL library from GitHub. The project name is mesa-dist-win.
<p align="center">
  <img src="\assets\blog\20250701\welsim_sandbox_mesa_win_dist.png" alt="welsim_sandbox_mesa_win_dist" />
</p>

2.Choose the appropriate version for your operating system and build type. In this case, the release-msvc version is selected.
<p align="center">
  <img src="\assets\blog\20250701\welsim_sandbox_mesa_download.png" alt="welsim_sandbox_mesa_download" />
</p>

3.Extract the files, open the extracted directory, and type cmd in the address bar to open a command prompt. Then, run the *perappdeploy.bat* file.
<p align="center">
  <img src="\assets\blog\20250701\welsim_sandbox_run_cmd.png" alt="welsim_sandbox_run_cmd" />
</p>

4.The command line will launch and display relevant information. Press any key to continue.
<p align="center">
  <img src="\assets\blog\20250701\welsim_sandbox_mesa_run1.png" alt="welsim_sandbox_mesa_run1" />
</p>


5.Follow the prompts by inputting the executable file folder: *C:\Program Files\WELSIM\MatEditor*, the executable file name: *runMatEditor.exe*, and selecting the processor architecture: *x64*.
<p align="center">
  <img src="\assets\blog\20250701\welsim_sandbox_mesa_run3.png" alt="welsim_sandbox_mesa_run3" />
</p>

6.The OpenGL library is now added to MatEditor. You can re-run the application, and the main window should now display correctly.
<p align="center">
  <img src="\assets\blog\20250701\welsim_sandbox_mesa_applied_mateditor.png" alt="welsim_sandbox_mesa_applied_mateditor" />
</p>


## Conclusion
This article uses MatEditor as an example to demonstrate how to resolve OpenGL library dependency issues in Windows Sandbox. The same method applies to other environments lacking OpenGL support, such as Windows systems running in VirtualBox. Besides MatEditor, other WelSim products such as the general simulation software WELSIM and the free curve fitting tool CurveFitter are also based on OpenGL and will require similar configuration when used in the sandbox.


---
<small>
WelSim and its developers are not directly affiliated with OpenGL, Windows, Linux, VirtualBox, or Sandbox. References to these technologies are solely for technical blog purposes and software usage guidance.
</small>
