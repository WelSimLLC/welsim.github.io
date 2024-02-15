---
lang: en
layout: post
title:  "Batch processing of CAE simulation software"
date:   2024-02-14
author: "[SimLet](https://twitter.com/getwelsim)"
---


Modern CAE software not only possesses powerful analysis capabilities but also features excellent graphical user interfaces. However, there are occasions when it is necessary to perform a large number of repetitive calculations for a specific type of model, namely, batch processing computation that do not require user's intervention. This type of computing often involves making slight changes to a parameter, calculating the corresponding results, and obtaining optimal parameters, such as the geometric details, material parameters, or boundary condition values. Batch processing calculations enable quick conclusions, thereby enhancing the efficiency of CAE software users.
<p align="center">
  <img src="\assets\blog\20240214\welsim_batch_processing.png" alt="welsim_batch_processing" />
</p>


Batch processing requests higher demands on the functionality of CAE software. Currently, the general-purpose simulation software WELSIM provides two batch processing methods. Method 1 involves automatic computation through XML scripts. Method 2 allows for the creation of multiple analysis projects in the GUI and the execution of batch processing calculations. This article describes the both processes.


## Method 1: Script Batch Processing
Leading CAE software already supports script batch processing capabilities. Since automated testing and script batch processing share the same essential nature of data persistent macro commands, CAE software that supports automated testing will undoubtedly possess the capabilities of script batch processing.



Firstly, in the XML script, setup a WELSIM model workflow.

Clear the target folder.
```
<wsevent object="wsApp" command="cleanFolder" arguments="$WELSIM_DATA_ROOT/97_Exported/11018" />
```

Choose the unit system for the project; here, the *mm-kg-s unit* system is applied.
```
<wsevent object="mainWindow/Std_DlgUserPref/Std_DlgUserPref" command="activate" arguments="" />
<wsevent object="mainWindow/PrefDlg/pagesWidget/general/scrollArea/qt_scrollarea_viewport/contents/tabWidget/qt_tabwidget_tabbar" command="set_tab_with_text" arguments="Units" />
<wsevent object="mainWindow/PrefDlg/pagesWidget/general/scrollArea/qt_scrollarea_viewport/contents/tabWidget/qt_tabwidget_stackedwidget/tabUnits/groupBoxUnits/radioUnitsMMKS" command="set_boolean" arguments="true" />
<wsevent object="mainWindow/PrefDlg/btnOK" command="activate" arguments="" />
```

Add a new FEM project, and use the default static structural analysis settings.
```
<wsevent object="mainWindow/menuBar" command="activate" arguments="&amp;File" />
<wsevent object="mainWindow/menuBar/&amp;File" command="activate" arguments="Fem_NewDoc" />
```

Import a geometry from the test folder, with the filename *box_x20_y1_z2.step*, and set the material to *Structural Steel*.
```
<wsevent object="mainWindow/menuBar" command="activate" arguments="&amp;Geometry" />
<wsevent object="mainWindow/menuBar/&amp;Geometry" command="activate" arguments="Fem_ImportPart" />
<wsevent object="mainWindow/OpenDialog" command="filesSelected" arguments="$WELSIM_DATA_ROOT/01_ShapeData/box_goup/box_x20_y1_z2.step" />
<wsevent object="mainWindow/DockTreeDocking/TreeDocking/treeWidget" command="setCurrent" arguments="0.0.1.0.0.0.0.0" />
<wsevent object="mainWindow/DockPropDockingView/PropDockingView/PropView/tabWidget/qt_tabwidget_stackedwidget/propertyData" command="setCurrent" arguments="8.1" />
<wsevent object="mainWindow/DockPropDockingView/PropDockingView/PropView/tabWidget/qt_tabwidget_stackedwidget/propertyData/qt_scrollarea_viewport/11Material" command="activated" arguments="Structural Steel (ID:2)" />
```

Set the mesh density and generate mesh.
```
<wsevent object="mainWindow/DockTreeDocking/TreeDocking/treeWidget" command="setCurrent" arguments="0.0.1.0.1.0.0.0" />
<wsevent object="mainWindow/DockPropDockingView/PropDockingView/PropView/tabWidget/qt_tabwidget_stackedwidget/propertyData" command="setCurrent" arguments="4.1" />
<wsevent object="mainWindow/DockPropDockingView/PropDockingView/PropView/tabWidget/qt_tabwidget_stackedwidget/propertyData/qt_scrollarea_viewport/7MaximumSize" command="set_double" arguments="0.3" />
<wsevent object="mainWindow/Fem_MeshAll/Fem_MeshAll" command="activate" arguments="" />
```

Set fixed boundary conditions for the selected boundary entity, which is *Obj11_Face1*.
```
<wsevent object="mainWindow/Fem_BCFixed/Fem_BCFixed" command="activate" arguments="" />
<wsevent object="mainWindow/DockTreeDocking/TreeDocking/treeWidget" command="setCurrent" arguments="0.0.1.0.2.0.1.0" />
<wsevent object="mainWindow/DockPropDockingView/PropDockingView/PropView/tabWidget/qt_tabwidget_stackedwidget/propertyData" command="setCurrent" arguments="5.1" />
<wsevent object="mainWindow/DockPropDockingView/PropDockingView/PropView/tabWidget/qt_tabwidget_stackedwidget/propertyData/qt_scrollarea_viewport/12Geometry/12SelBtnOK" command="set_selection" arguments="Obj11_Face1" />
```

Set force boundary conditions with a direction in the Z-axis and a magnitude of *1000*. The selected surface is *Obj11_Face2*.
```
<wsevent object="mainWindow/Fem_BCForce/Fem_BCForce" command="activate" arguments="" />
<wsevent object="mainWindow/DockTreeDocking/TreeDocking/treeWidget" command="setCurrent" arguments="0.0.1.0.2.0.2.0" />
<wsevent object="mainWindow/DockPropDockingView/PropDockingView/PropView/tabWidget/qt_tabwidget_stackedwidget/propertyData" command="setCurrent" arguments="5.1" />
<wsevent object="mainWindow/DockPropDockingView/PropDockingView/PropView/tabWidget/qt_tabwidget_stackedwidget/propertyData/qt_scrollarea_viewport/13Geometry/13SelBtnOK" command="set_selection" arguments="Obj11_Face2" />
<wsevent object="mainWindow/DockPropDockingView/PropDockingView/PropView/tabWidget/qt_tabwidget_stackedwidget/propertyData" command="setCurrent" arguments="9.1" />
<wsevent object="mainWindow/DockPropDockingView/PropDockingView/PropView/tabWidget/qt_tabwidget_stackedwidget/propertyData/qt_scrollarea_viewport/13ForceZConstant/quantitySpinBox" command="set_double" arguments="1000" />
```

Solve and add a stress result object, with the type as the default *Von Mises stress*. Evaluate and display the stress result.
```
<wsevent object="mainWindow/Fem_Solve/Fem_Solve" command="activate" arguments="" />
<wsevent object="mainWindow/Fem_ResultStress/Fem_ResultStress" command="activate" arguments="" />
<wsevent object="mainWindow/DockTreeDocking/TreeDocking/treeWidget" command="setCurrent" arguments="0.0.1.0.3.0.0.0" />
<wsevent object="mainWindow/Fem_EvaluateResult/Fem_EvaluateResult" command="activate" arguments="" />
```

Save the project as *p1.wsdb*. Simultaneously, close the current project.
```
<wsevent object="mainWindow/menuBar" command="activate" arguments="&amp;File" />
<wsevent object="mainWindow/menuBar/&amp;File" command="activate" arguments="Std_SaveAs" />
<wsevent object="mainWindow/QFileDialog/fileNameEdit" command="set_string" arguments="$WELSIM_DATA_ROOT/97_Exported/11018/p1.wsdb" />
<wsevent object="mainWindow/QFileDialog/buttonBox/1QPushButton0" command="activate" arguments="" />
<wsevent object="mainWindow/menuBar/&amp;File" command="activate" arguments="Fem_CloseAllDocs" />
```

At this point, one cycle of computing setup is complete. When another new cycle of computation is needed, simply copy and paste the above code, modify the imported geometry name and the project file's name for export, and execute to achieve batch processing. The geometry of this test case is relatively uniform, with only slight differences in length, so there is no need to modify the names of surface entity in the boundary conditions. If there are significant differences in geometry, it is essential to ensure that the surface of boundary condition  settings refer to the correct face names.
The test script is named *11018_save_multi_structural_projects.xml* and is open source, saved as one of the WELSIM test cases on GitHub.


## Method 2: Graphical Project File Batch Processing
WELSIM supports the multiple FEM projects in the project tree. As shown in the figure below, three FEM projects have been created.
<p align="center">
  <img src="\assets\blog\20240214\welsim_create_multi_project.png" alt="welsim_create_multi_project" />
</p>


After setting all materials, contacts, boundary conditions, etc., you can click the *Mesh & Solve All* button in the menu to perform batch processing calculations for all projects. This feature automatically calculates the next project after one project's computation is completed, without user's intervention in between. For computationally intensive large models, this method effectively saves analysis personnel's time.
<p align="center">
  <img src="\assets\blog\20240214\welsim_mesh_solve_all.png" alt="welsim_mesh_solve_all" />
</p>


## Conclusion
This article introduces two commonly used batch processing methods in CAE software. Each method has its advantages. Script batch processing typically has a clear and easy-to-understand file structure that is convenient for saving and modifying. Script files are usually small and do not need a lot of storage space. On the other hand, project file batch processing can save the result data, but the files tend to be larger. Both batch processing methods can be used in combination, with script batch processing for initial parameter screening, narrowing down the range, and project batch processing for final computation and result keeping.

---
<small>
WELSIM is the #1 engineering simulation software for the open-source community.
</small>
