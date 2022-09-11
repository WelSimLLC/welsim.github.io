---
lang: en
layout: post
title:  "Explore the enterprise-grade open-source solver OpenRadioss II : build in Windows"
date:   2022-09-10
author: "[SimLet](https://twitter.com/getwelsim)"
---


After the publication of the last article about OpenRadioss, I got some constructive feedback in terms of the concept of the world’s first enterprise-grade open-source solver. One reader reported that Code_Aster is also an open-source solver from an enterprise, and it has been open-sourced for a long time, although it is essentially an implicit solver. This statement makes sense, so the author modifies the title slightly in this and the next articles. Regarding Code_Aster, the author will take you to explore if there is a chance in the future.

<p align="center">
  <img src="\assets\blog\20220910\windows_linux.png" alt="windows_linux" />
</p>

In the last article, the author demonstrated the whole process of building OpenRadioss in Linux Ubuntu 20.04 LTS and made some conclusions. In this article, the author shows the process of building OpenRadioss in Windows, and shares some experiences at the end.

On the official GitHub page of OpenRadioss, it is explained that OpenRadioss can be built in Windows by using WSL. Therefore, running OpenRadioss in Windows must be through the WSL as well. Fortunately, the file exchange between WSL and Windows is convenient, especially for the input scripts and result files, Windows user can save some efforts at file swapping using the Window build.

<p align="center">
  <img src="\assets\blog\20220910\win_openradioss_github.png" alt="win_openradioss_github" />
</p>


Since the Ubuntu 20.04 LTS is installed in the WSL, so author updates and downloads the required dependencies using the Ubuntu commands. Enter the following commands in the window of WSL.

```
apt-get update
apt-get upgrade
apt-get install build-essential, gfortran, cmake, perl, git-lfs, libapr1-dev
```

Check out the source code according to the method given in the official tutorial.

```
git lfs install
git clone git@github.com:OpenRadioss/OpenRadioss.git
```

If you cannot download the source code directly from the official trunk, try to fork the repository to your own account then download it from your own fork.

As the download is complete, enter the command in the *OpenRadioss/starter* directory to start building

```
./build_script.sh -arch=linux64_gf -nt 20
```

When it is built successfully, the display is as follows:

<p align="center">
  <img src="\assets\blog\20220910\win_openradioss_starter_built.png" alt="win_openradioss_starter_built" />
</p>


Test the executable file as below.

```
./starter_linux64_gf
```

<p align="center">
  <img src="\assets\blog\20220910\win_openradioss_starter_run.png" alt="win_openradioss_starter_run" />
</p>

It runs well as you can see the output information on the screen.

The next step is building the engine. Go to the OpenRadioss/engine directory and enter commands:

```
./build_script.sh -arch=linux64_gf -nt 20
```

After building successfully, you get the following messages

<p align="center">
  <img src="\assets\blog\20220910\win_openradioss_engine_built.png" alt="win_openradioss_engine_built" />
</p>

Test the generated executable file.

```
./engine_linux64_gf
```
<p align="center">
  <img src="\assets\blog\20220910\win_openradioss_engine_run.png" alt="win_openradioss_engine_run" />
</p>


The program *engine* works well.

At this point, the building of OpenRadioss in Windows is completed. The entire process is very smooth.

Completing the building process in Windows, the author feels :

1. Because of the use of the WSL, in general, there is no significant difference with the building in the native Linux. Parallel compilation can be enabled and gains speedup at building program.
2. Running the program starter_linux64_gf may prompt the error that the dynamic library libhm_reader_linux64.so cannot be found. This problem may also be encountered in Linux. You can set the link path to the file using the patchelf command.
3. Running starter_linux64_gf may prompt the error that the dynamic library libapr1.so.0 cannot be found. This problem may also be encountered in Linux. It can be solved by installing libapr1-dev or using the patchelf command.
4. WSL nominally solves the problem of building OpenRadioss in Windows, but it is not a native Windows build. It is user-friendly, but not very friendly to developers who are familiar with the Windows development environment. Because the powerful debugging features of Visual Studio cannot be applied when you need to understand the program or fix some things. The bright side is that users now can run simulation scripts in Windows, the author cannot wait to run some examples at this moment.

In the next article, the author will keep exploring OpenRadioss with you. What do you want to discuss? Leave a message in the comments section.

<small>
WelSim and the author are not affiliated with the Altair and OpenRadioss teams. Altair and OpenRadioss are used only as nominative references to the open-source project and software developed and released by the Altair and OpenRadioss teams.
</small>

******

<small>
WelSimulation LLC is an independent engineering simulation technology provider, located in Greater Pittsburgh, PA. Its flagship product WESLIM is a general-purpose engineering simulation software with an all-in-one graphical user interface and self-integrated features.
</small> 
