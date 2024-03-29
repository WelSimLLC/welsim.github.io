---
lang: en
layout: post
title:  "Create CAE simulation material data using scripts"
date:   2024-02-26
author: "[SimLet](https://twitter.com/getwelsim)"
---


For users conducting CAE analysis, material definition can be complex process. It is meticulous because the crucial material parameters require confirmation of their accuracy for each parameter. Furthermore, material definition can be laborious when dealing with numerous materials and diverse properties, as defining and editing attributes becomes a substantial task. An efficient method to define materials is to use scripts. The large-scale general simulation CAE software WELSIM supports script-defined materials through an automated testing system, facilitating the definition of a considerable material dataset using XML scripts.

This article uses examples to demonstrate the method of script-based creation of a large dataset of materials in WELSIM.

1) Build a single material data through GUI. (If familiar with XML syntax, you can also refer to existing XML test files and write your own). Then, click Record Test.
<p align="center">
  <img src="\assets\blog\20240226\welsim_mat_script_record_tests.png" alt="welsim_mat_script_record_tests" />
</p>


Create a new material object, naming it Mat001. Next, open the material editing panel and sequentially add density, isotropic elasticity, and bilinear isotropic hardening properties. These properties are commonly used in elastic-plastic models.
<p align="center">
  <img src="\assets\blog\20240226\welsim_mat_script_gui_macro.png" alt="welsim_mat_script_gui_macro" />
</p>


Input the relevant parameters. After completing the editing operations, the material properties should appear as follows:
<p align="center">
  <img src="\assets\blog\20240226\welsim_mat_script_data1.png" alt="welsim_mat_script_data1" />
</p>


2) Test a single material data file.

Click the stop recording button, and the macro command for graphical operations is recorded which generates the script. Open the recorded XML file with a text editor, make slight modifications, delete redundant lines, and obtain the script for a single material. In the figure below, the green-boxed part indicates the modifications for other materials, expanding to derive additional materials. These include the material object's position in the project tree window, material name, material object ID, and material property parameters.
<p align="center">
  <img src="\assets\blog\20240226\welsim_mat_script_data_xml.png" alt="welsim_mat_script_data_xml" />
</p>


3) Copy and paste a single material, making the necessary modifications.

Copy and paste the text from the figure, modifying the green-boxed parts to create a new material. This article creates a total of 21 materials. The parameters for material properties, all using bilinear isotropic hardening plasticity, are listed in the table below.
<p align="center">
  <img src="\assets\blog\20240226\welsim_mat_input_table.png" alt="welsim_mat_input_table" />
</p>


4) Complete the script, run, and debug.

With the script editing completed, it can be run and tested. After running it, proceed directly to the subsequent simulation analysis tasks. Alternatively, material data can be exported for use in other software. The materials exported from WELSIM can be opened in MatEditor, as shown in the figure below.
<p align="center">
  <img src="\assets\blog\20240226\welsim_mat_script_read_xml_mateditor.png" alt="welsim_mat_script_read_xml_mateditor" />
</p>


Video demonstration during script execution is provided.
[![Watch the video](https://img.youtube.com/vi/dTnd2hBRN8g/default.jpg)](https://youtu.be/dTnd2hBRN8g)



## Conclusion
The script file used in this example is open-source and saved in the WELSIM public test library under the filename *"06018_create_multiple_materials.xml"*. This example creates a total of 21 material datasets, each with similar properties but various numerical values. Furthermore, different material properties can be added in the script, supporting a more diverse material dataset.

Using scripts to effectively establish material datasets saves editing time, reduces errors, and is easy to maintain. Scripts can be easily modified for use in other material datasets, which displays strong adaptability. It is the ideal method for creating and maintaining large material datasets.

The script language for material definition may vary depending on the CAE software. In this example, XML is used. Other CAE software may use different languages, such as Python or JavaScript.



---
<small>
WELSIM is the #1 engineering simulation software for the open-source community.
</small>
