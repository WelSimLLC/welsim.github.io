---
lang: en
layout: post
title:  "Export the CAE simulation result files in WELSIM"
date:   2024-05-16
author: "[SimLet](https://twitter.com/getwelsim)"
---


Modern general-purpose CAE simulation software has a high degree of integration, especially since many commercial software no longer support the export of computational results. This creates some limitations for using result data in third-party software. Sometimes users wish to export result data or perform special processing on the results, such as coupling computation. The general-purpose CAE simulation software WELSIM provides a results export feature, allowing users to quickly and conveniently obtain result files.
<p align="center">
  <img src="\assets\blog\20240516\paraview_ex_car.PNG" alt="paraview_ex_car" />
</p>


Currently, there are two ways to export results: exporting all historical results or exporting the results at the current time step.

## Exporting All-Time History Results
For transient analysis, the results will contain data from multiple time steps. Users can export the results from all time steps at once. Supported formats include binary PVD and ASCII PVD. For detailed information about the PVD format, you can refer to the article "[ParaView Data (pvd) file format and writing
](https://welsim.com/2022/10/04/paraview-data-file-format-and-writing.html)".

The method to achieve this is to find the "Export All Results" command in the right-click context menu of the solution node and click it.
<p align="center">
  <img src="\assets\blog\20240516\welsim_export_all_results.png" alt="welsim_export_all_results" />
</p>


After selecting "Export All Results," a dialog box will prompt you to enter a file name, and you can choose to export in ASCII or binary format.
<p align="center">
  <img src="\assets\blog\20240516\welsim_export_all_results_ascii_bin.png" alt="welsim_export_all_results_ascii_bin" />
</p>


Afterward, you will be able to find the exported result files at the target path. As shown below, WelSim_Results.pvd is the entry file for the results set, which can be directly read by open-source post-processing software such as ParaView. Each folder corresponds to the result data at a specific time step.
<p align="center">
  <img src="\assets\blog\20240516\welsim_export_pvd_files.png" alt="welsim_export_pvd_files" />
</p>


## Exporting Current Time Step Results
Sometimes, we only need the result data at a certain time step, such as the final step result of a steady-state analysis. You can click the corresponding results object, set the "Set Number," and select "Export Result" from the right-click context menu to export the results at the current time step. Supported file formats include VTU, PVTU, classic VTK, Tecplot, and text. The exported result file will contain all types of results at the current time step.
<p align="center">
  <img src="\assets\blog\20240516\welsim_rmb_export_result.png" alt="welsim_rmb_export_result" />
</p>


After selecting "Export Result," you will be prompted to enter a file name, and you can choose the export format.
<p align="center">
  <img src="\assets\blog\20240516\welsim_export_result_types.png" alt="welsim_export_result_types" />
</p>

In this example, the PVTU format was chosen for export. Users can open this file in ParaView or VisIt software and engage in post-processing work in these third-party software.
<p align="center">
  <img src="\assets\blog\20240516\welsim_export_result_to_visit_paraview.png" alt="welsim_export_result_to_visit_paraview" />
</p>

For more details on saving files in VTU/VTK format, you can refer to the article "[Export result data in VTK format from WELSIM](https://welsim.com/2019/01/10/export-result-data-in-vtk-format-from-welsim.html)".

## Conclusion
WELSIM provides mainstream result file formats. For time-based transient analysis results, you can export the entire time history in PVD format. For steady-state results, you can export in VTU, PVTU, VTK, or Tecplot formats.


All exported files contain the mesh data of nodes and elements.

With the iteration and updates of versions, WELSIM will support more types of result files.

---
<small>
WELSIM and the author are not affiliated with ParaView, VTK, and TecPlot. ParaView, VTK, and TecPlot are used only as a nominative reference to the open-source projects and software developed and released by these teams or institutions.
</small>


