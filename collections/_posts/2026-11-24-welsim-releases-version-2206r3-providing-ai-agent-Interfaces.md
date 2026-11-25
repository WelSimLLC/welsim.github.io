---
lang: en
layout: post
title:  "WELSIM releases version 2026R3, providing AI agent interfaces"
date:   2026-11-24
author: "[SimLet](https://twitter.com/getwelsim)"
---

On November 24, 2026, WelSimulation LLC officially released WELSIM 2026R3 (internal build 3.4), the latest update to its general-purpose engineering simulation software. The new version equips engineers and researchers with streamlined mesh quality inspection tools, expanded solver compatibility, and—for the first time—scripting, a Python console, and Model Context Protocol (MCP) support, enabling external applications and AI agents to execute end-to-end simulation workflows from modeling and meshing to solving and post-processing.
<p align="center">
  <img src="\assets\blog\20261124\welsim_splash.png" alt="welsim_splash" />
</p>

## Simulation Automation and AI Agent Integration

WELSIM 2026R3 debuts a Python-based scripting automation kernel. All objects, commands, and properties are cataloged in a unified registry and exposed externally via RPC commands, an integrated Python console, and an MCP (Model Context Protocol) interface. Through these interfaces, scripts and AI agents can programmatically drive the entire simulation pipeline; they can create geometry, generate meshes, assign materials, submit solver jobs, and extract result data. Users can leverage AI agents to directly automate simulation analyses, or interact with models manually for validation and inspection.
<p align="center">
  <img src="\assets\blog\20261124\welsim_ai_agent_diagram.png" alt="welsim_ai_agent_diagram" />
</p>

## Mesh Quality Assessment

The update adds visual inspection tools for evaluating mesh quality across several key metrics, including aspect ratio, Jacobian ratio, maximum corner angle, skewness, and tetrahedral size. Users can inspect element quality directly within the 3D viewport, or view quality distribution bar charts in the table and graph window, to assess mesh integrity before solving. Additionally, element types and element IDs can now be displayed as 3D contour plots.
<p align="center">
  <img src="\assets\blog\20261124\welsim_mesh_quality_diagram.png" alt="welsim_mesh_quality_diagram" />
</p>

## Solver Pre- and Post-Processing

WELSIM 2026R3 significantly expands compatibility with multiple open-source solvers. For OpenRadioss, the release adds pre- and post-processing support for implicit transient analysis and the arc-length method. Support for the Elmer FEM electromagnetic module has also been enhanced, and there are now native capabilities to read Elmer FEM VTK, VTU, and PVTU result files, as well as CalculiX FRD result files. Furthermore, users can begin to launch external post-processing tools directly from the interface, opening result files in locally installed software such as ParaView or VisIt with a single click. The new version also accommodates reverse-importing solver input files from CalculiX and FrontISTR, allowing existing analysis models to convert into visual WELSIM projects.
<p align="center">
  <img src="\assets\blog\20261124\welsim_mesh_aspect_ratio_3d.png" alt="welsim_mesh_aspect_ratio_3d" />
</p>

## Geometry Modeling

The underlying geometry kernel, OpenCascade, has been upgraded from version 7.5 to 7.9.3. Boolean operation objects have been completely refactored so that input bodies appear as child nodes under the Boolean object with clearer naming conventions, there is full undo support for Boolean operations, and state restoration is accurate when saving and reloading projects. Other geometry enhancements include a new Fragment tool for mutually slicing multiple bodies, and native BRep format import and export to enable direct meshing of BRep files. Finally, numerous STEP import and export issues have been resolved, and importing assemblies now automatically combines component names for imported objects.

## General Performance and Usability Enhancements

Capping the release are broad improvements to performance and user experience, starting with faster application startup and shutdown times, and redesigned icons for the dark theme. Boundary conditions now support 3D visual indicators, such as pressure arrows and displacement or rotation markers—mesh node IDs can be displayed and selected directly. The unit system has also been synchronized across tables and charts, accompanied by a built-in unit conversion tool.

---

<small>WelSim and the author are not affiliated with, endorsed by, or connected to any of the organizations or development teams mentioned in this article. All names and trademarks are referenced strictly for technical blogging and software usage purposes.</small>


