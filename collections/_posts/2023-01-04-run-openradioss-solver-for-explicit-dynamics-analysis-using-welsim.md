---
lang: en
layout: post
title:  "Run OpenRadioss solver for explicit dynamics analysis using WELSIM"
date:   2023-01-04
author: "[SimLet](https://twitter.com/getwelsim)"
---


OpenRadioss is an explicit dynamics solver based on the finite element method that was open-sourced by Altair Engineering Inc. (NASDAQ: ALTR) in September 2022. OpenRadioss has significantly rich features, accurate and reliable results, supports parallel computing of multi-core CPUs and clusters, and has released operating system versions including Windows and multiple Linux distributions. Certainly, OpenRadioss is the most complete open-source finite element solver.

<p align="center">
  <img src="\assets\blog\20230104\altair_openradioss.png" alt="altair_openradioss" />
</p>

Shortly after OpenRadioss was released, WelSim’s free material edition software MatEditor supported the generation of OpenRadioss format material scripts (for details, see “[Use MatEditor to generate OpenRadioss material data files](/2022/11/26/use-mateditor-to-generate-openradioss-material-data-files.html)”), MatEditor is the world’s first free software that supports OpenRadioss‘s materials, it provides a convenient and intuitive solution for OpenRadioss users to input model materials.

In addition to the material scripts, the general-purpose simulation software WELSIM recently supports OpenRadioss solver in the overall pre/post-processing aspects and integrates OpenRadioss as the default explicit dynamics solver. WELSIM is the world’s first third-party software that supports OpenRadioss with a general-purpose pre/post-processing role. Thanks to its ease of use and security, WELSIM contributes to the entire simulation community as it greatly reduces the learning curve of applying OpenRadioss. Since OpenRadioss uses the AGPL-3.0 protocol, the closed-source software WELSIM cannot include OpenRadioss in the installer package. Users need to configure OpenRadioss by themselves. **The configuration process is extremely simple, just unzip OpenRadioss to the installation directory of WELSIM**. The specific description is as follows:

1. Download the executable package from GitHub or OpenRadioss' official website.

<p align="center">
  <img src="\assets\blog\20230104\download_openradioss.png" alt="download_openradioss" />
</p>

Four downloadable packages are listed above. The first compressed package is the executable program of the Linux version, the second is the executables for Windows, the third and fourth compressed packages are the source code, and the difference is only about the compressed format. The current demonstration system is Windows, so we download the second compressed package OpenRadioss_win64.zip.

2. After decompression, a folder with the name of OpenRadioss is obtained as shown in the figure.

<p align="center">
  <img src="\assets\blog\20230104\downloaded_openradioss_folder.png" alt="downloaded_openradioss_folder" />
</p>

3. Copy the folder of OpenRadioss to the installation directory of WELSIM.

<p align="center">
  <img src="\assets\blog\20230104\openradioss_copied_to.png" alt="openradioss_copied_to" />
</p>

The configuration is now complete. You can directly call OpenRadioss to solve in WELSIM. Note that in the project definition, the project property needs to be set to explicit dynamics as shown below. When solving, WELSIM will automatically call OpenRadioss to solve the models.

<p align="center">
  <img src="\assets\blog\20230104\welsim_structural_transient_explicit.png" alt="welsim_structural_transient_explicit" />
</p>

## Call the OpenRadioss solver anywhere
By default, WELSIM will invoke the OpenRadioss solver from the installation directory. If the user prefers to place the OpenRadioss solver in any other directory, this can be easily done as well. You only need to modify the specified directory of OpenRadioss to the desired location in the preferences of WELSIM. As shown below.

<p align="center">
  <img src="\assets\blog\20230104\welsim_preference_solver.png" alt="welsim_preference_solver" />
</p>

## Generate OpenRadioss solver input files
WelSim also provides a convenient solution for those users who only need OpenRadioss input scripts and prefer to solve the models within the WELSIM framework. After the mesh generation is completed and various conditions are defined, you can select **Tools -> Export OpenRadioss Scripts** in the menu to generate the corresponding solver input scripts in the specified directory.

<p align="center">
  <img src="\assets\blog\20230104\welsim_export_openradioss.png" alt="welsim_export_openradioss" />
</p>

After selecting the output path, you will see the following files in the specified directory. Among them, *radioss_welsim_0000.rad* is the Starter file, *radioss_welsim_0001.rad* is the Engine file, and *mesh_radioss.inc* is the mesh file. Note that the generated files may vary slightly depending on the type of analysis.

<p align="center">
  <img src="\assets\blog\20230104\welsim_openradioss_scripts.png" alt="welsim_openradioss_scripts" />
</p>


## Behaviors and Limitations
1. The Windows development version of WELSIM 2023R1 already supports this function, and it will be continuously enhanced and improved in the 2023R1 official and later versions. The official 2023R1 Linux Ubuntu version will also support the OpenRadioss solver.
2. Only Tet4/10 and Tri3/6 mesh elements are supported at this moment.
3. Historical tables and curves of solution are not supported yet for OpenRadioss results. Currently, it is displayed with the value of 0.

******

<small>
WelSim and the author are not affiliated with the Altair or OpenRadioss team. OpenRadioss is used only as nominative references to the open-source project and software developed and released by the Altair and OpenRadioss teams.
</small>

<small>
WelSimulation LLC is an independent engineering simulation technology provider, located in Greater Pittsburgh, PA. Its flagship product WESLIM is a general-purpose engineering simulation software with an all-in-one graphical user interface and self-integrated features.
</small>

