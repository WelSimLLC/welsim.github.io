---
lang: en
layout: post
title:  "Explore OpenRadioss, the world's first enterprise-grade open-source explicit dynamics solver (I)"
date:   2022-09-10
author: "[SimLet](https://twitter.com/getwelsim)"
---


On September 9, 2022, Altair, an engineering simulation company listed on Nasdaq, open-sourced the explicit dynamics solver Radioss and named it OpenRadioss. Nowadays it is common for large tech companies to open source their projects, such as Google, Microsoft, Amazon, and other established tech companies have made a lot of contributions to the open source community. But in the field of engineering simulation, it is still rare to see a large enterprise open the source of core products. Altair takes the lead steps in breaking this ice and releases the OpenRadioss. It is of great significance to both the open source ecosystem and the simulation community.

<p align="center">
  <img src="\assets\blog\open_radioss_screen.png" alt="welsim_openradioss_web" />
</p>
<p align = "center">
The above picture is a screenshot from the OpenRadioss.org website
</p>


The above picture is a screenshot from the OpenRadioss.org websiteThe author is an active enthusiast of the open source community. Not long ago, he open-sourced WelSim's official website and may open source more products in the future. Thus for a large project like OpenRadioss, he has a great interest. Whenever we start to explore a large-scale source code, the first thing to do is compile the project right after reading the documents. The official OpenRadioss GitHub page gives a concise and clear tutorial on building the project.

<p align="center">
  <img src="\assets\blog\how_to_build_openradioss.PNG" alt="welsim_openradioss_github_build" />
</p>

In accordance with instructions, the author quickly compiled and generated the executable files. The experience is shared here with you. The author uses Ubuntu 20.04 LTS with the libraries installed as shown below

```
sudo apt update
sudo apt install build-esseitnal, gfortran, cmake, perl, git-lfs, openmpi-dev
```

OpenRadioss will generate two executable files, one is the starter and the other is the engine. The generated file name will be accompanied by the compiler name. If the given compiler name is linux64_gf, the generated files will be starter_linux64_gf and engine_linux64_gf respectively. At present, two official CMake compilers are provided, namely AMD's compiler linux64_AOCC and GNU's Fortran compiler linux64_gf. Users can also create new make files themselves to support different compilers. However, it can only support Linux-type operating systems in general, because the third-party library hm_reader is not open source, and only the Linux version of the dynamic library (libhm_reader_linux64.so) is officially available. Even for Windows, it is recommended to use WSL to build OpenRadioss.


First, compile the starter. In the directory OpenRadioss/starter, enter

```
./build_script.sh -arch=linux64_gf -nt 20
```

The type of compiler and number of threads are specified here. Depending on the type of CPU, 20 threads are applied here to speed up the building.

<p align="center">
  <img src="\assets\blog\20220909\open_radioss_build_starter.png" alt="open_radioss_build_starter" />
</p>

When the building is complete, an executable file is generated in the exec directory.

<p align="center">
  <img src="\assets\blog\20220909\open_radioss_starter_exec.png" alt="open_radioss_starter_exec" />
</p>

Try it out.

```
./starter_linux64_gf
```

<p align="center">
  <img src="\assets\blog\20220909\open_radioss_starter_run.png" alt="open_radioss_starter_run" />
</p>

It works well. For further testing, input scripts are required. We will do that in the future.

Now it is time to build the second executable file engine, the method and process are almost the same as the starter. In the OpenRadioss/engine directory, enter

```
./build_script.sh -arch=linux64_gf -nt 20
```


The flag **-openmpi** is not added here, because it is unnecessary as an initial tryout, and it may add extra work when encountering problems. In fact, the parallel based on the shared memory method such as OpenMP performs pretty well on the desktop.

<p align="center">
  <img src="\assets\blog\20220909\open_radioss_engine_built.png" alt="open_radioss_engine_built" />
</p>


After building, engine_linux64_gf64 will be generated in the exec folder.

Simply call the executable.

```
./engine_linux64_gf
```

It runs.

Overall my impression about OpenRadioss is:

1. As a public company, Altair's ambitions to open source a part of the core code ahead of other peers is commendable. Maybe it will bring an open source trend to the entire industry. A more open environment will undoubtedly promote the adaption of simulation technology and the progress of human civilization.
2. Compiling OpenRadioss in Ubuntu Linux is generally smooth. It should be noted that the git-lfs environment must be properly installed and configured, otherwise there may be some link problems at compiling.
3. The hm_reader library is still enclosed. This library should contain a large number of finite element mesh data structures and reading features.
4. At present, native compilation using VS+ifort under Windows is not supported, which may be troublesome for debugging. Software developer knows that debugging large code under Linux can be a challenge.
5. Although the AGPL license is not very friendly, it should be enough for personal study and research.

In the next article, the author will keep exploring OpenRadioss with you. What do you want to discuss? Leave a message in the comments section.

<small>
WelSim and the author are not affiliated with the Altair and OpenRadioss teams. Altair and OpenRadioss are used only as nominative references to the open-source project and software developed and released by the Altair and OpenRadioss teams.
</small>

******

<small>
WelSimulation LLC is an independent engineering simulation technology provider, located in Greater Pittsburgh, PA. Its flagship product WESLIM is a general-purpose engineering simulation software with an all-in-one graphical user interface and self-integrated features.
</small>
