---
lang: en
layout: post
title:  "Automated Testing for General-Purpose Engineering Simulation CAE Software"
date:   2024-01-30
author: "[SimLet](https://twitter.com/getwelsim)"
---


The automated testing system is an essential facility for modern large-scale software. Due to the complex functionality, long term maintenance, and high requirements for computational results of general-purpose CAE simulation software, it is necessary to have an automated testing system to maintain the robustness and accuracy of the product. In addition to the testing system, a vast number of test cases are also crucial intelligent assets that require a significant investment of development resources. The author has previously shared the detailed information on the automated testing of CAE software, as seen in the articles "[Automated Regression Testing for General-Purpose Engineering Simulation CAE Software](https://welsim.com/2023/08/22/automated-regression-testing-for-general-purpose-engineering-simulation-cae-software.html)" and "[Quickly Create Regression Test Cases for WELSIM](https://welsim.com/2023/08/22/automated-regression-testing-for-general-purpose-engineering-simulation-cae-software.html)". This article focuses on the running tests for engineering simulation CAE software.
<p align="center">
  <img src="\assets\blog\20240130\welsim_cae_tip_of_iceburg.jpg" alt="welsim_cae_tip_of_iceburg" />
</p>


Currently, major CAE software on the market does not publicly disclose their automated testing systems; they are only provided for internal development use, and end-users cannot access the testing system. WELSIM is currently the only general-purpose CAE software that opens up its automated testing system and provides open-source test cases worldwide. Therefore, this article can only use WELSIM for demonstration.


After launching the software, locate the command for automated testing in the GUI's menu bar or toolbar.
<p align="center">
  <img src="\assets\blog\20240130\welsim_regression_system_play_tests.png" alt="welsim_regression_system_play_tests" />
</p>

Clicking the "Play Test" button and select the tests from the dialog.
<p align="center">
  <img src="\assets\blog\20240130\welsim_regression_system_load_files.png" alt="welsim_regression_system_load_files" />
</p>


Currently, the reading of test files supports two formats: xml and wstb. Xml represents specific individual test, while wstb can contain multiple files for testing. As shown in the following picturec, wstb is essentially a collection of xml test files.
<p align="center">
  <img src="\assets\blog\20240130\welsim_regression_system_group_file.png" alt="welsim_regression_system_group_file" />
</p>


After reading the test file, the main testing user interface will be displayed. If a valid test file was selected in the previous step, the main window will list the test case. The testing main interface has various functions, which will be explained in four separate areas.
<p align="center">
  <img src="\assets\blog\20240130\welsim_regression_system_playback_ui.png" alt="welsim_regression_system_playback_ui" />
</p>


Area 1 occupies the majority of the interface, facilitating the display of a large number of test cases. Users can toggle on or off the cases they want to run. Each case has a progress bar to display the current testing progress. Each case also has a test result, with a green background indicating "Success" for passing tests and a red background indicating "Failed" for failed tests.

Area 2 displays the right-click context menu, offering common functions such as select all, deselect all, remove all, save test files, and more. The position of the context menu is flexible and depends on the mouse-click location, typically in a blank area.

Area 3 displays essential buttons, such as deleting project after a single test is completed, adding cases, remove cases, and saving test files. By default, the system closes the current project after each test, but users can change this by clicking the button. When the project is not closed after a test, users can manually save the project as a wsdb file. This feature is useful for test personnel to investigate the cause when a case fails. The "Save Test" button can save the currently failed cases, allowing users to rerun them after fixing the issues.

Area 4, at the bottom of the main interface, provides crucial functions for running, pausing, or stopping tests. The default time for each step of the test is 100 milliseconds, but users can modify it. The system also supports displaying logs.

The testing time depends on the number and size of cases. A quick test set usually completes within 10 minutes, while long-term tests typically finish within 15 hours. When all tests pass, the product's current state is considered relatively stable. If failed cases are identified, they can be run individually to investigate the causes. Appropriate updates to the software or test scripts can then be made.

## Test File Format

XML files are simple, intuitive, easy to read, and have good machine readability and writing performance, making them suitable as an automated test file format. The image below provides an example of a simple structural analysis test file.
<p align="center">
  <img src="\assets\blog\20240130\welsim_regression_system_xml_format.png" alt="welsim_regression_system_xml_format" />
</p>


According to the numbering, the file is divided into 7 sections:
1. Selecting the unit system.
2. Creating a new project, adding a cube, and meshing.
3. Adding a fixed boundary condition, selecting a face.
4. Adding a pressure boundary condition, selecting a face, and setting the pressure value.
5. Solving.
6. Adding a displacement result, evaluating and validating the results.
7. Adding a stress result, evaluating and validating the results.

Each element in the test script has three attributes: object, command, and arguments. Object is used to locate the QT widget related to the GUI, corresponding one-to-one with the object names in the software product. Command has options like activate and setCurrent. Arguments define additional parameters, such as table index, boundary selection, numerical values, key values, etc.

There are two types of elements: wsevent for event-driven actions, executing each step operation, and wscheck for validating a specific value. Engineering simulation software needs to ensure the accuracy of calculation results, and wscheck units are used for this task. During the execution of wsevent operations, extensive checks on software controls are performed to detect software defects such as crashes, memory leaks, etc.

## Behavior

Running the WelSim automated test requires adding the environment variable WELSIM_DATA_ROOT to the test case folder. Instructions are provided in the test case package.

Automated testing can only detect the functionalities covered by the test cases, so it needs continuous maintenance and addition of test cases as the CAE software evolves. WelSim has opened its testing system and released open-source test cases, allowing developers of solvers and backend applications to ensure accuracy and stability without creating their own automation systems.

The WelSim automated testing system is based on the software itself and can only be conducted after the software is launched. Some large software testing frameworks are independent processes that test the target software through inter-process communication. Both testing frameworks are feasible and effective, and developers can choose based on the software's characteristics and their technical stack.

Automated testing files are not limited to XML format. Depending on the software architecture and testing requirements, they can be in formats like Python or JavaScript, each with its advantages.

The current WelSim testing framework does not save test results, but future versions may support result storage. Results can be displayed through a webpage, and historical test data retrieval is supported, facilitating long-term product maintenance.



---

<small>
_WELSIM is the #1 engineering simulation software for the open-source community._
</small>
