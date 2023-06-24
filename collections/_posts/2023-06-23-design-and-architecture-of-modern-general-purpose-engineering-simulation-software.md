---
lang: en
layout: post
title:  "Design and architecture of modern general-purpose engineering simulation software"
date:   2023-06-23
author: "[SimLet](https://twitter.com/getwelsim)"
---

General-purpose engineering simulation software is a comprehensive information product that integrates multiple fields such as software engineering, computational mathematics, engineering, physics, and product design. It is highly difficult to build and has a long research and development cycle. The success of a general-purpose engineering simulation software is very closely related to its well-presented design and product architecture.


With the advancement of technology, we have observed a significant amount of differences between modern simulation software and products from ten years ago. Developers have shifted their focus from the accuracy and stability of computational results and user-friendly interfaces because these requirements have largely been addressed. The emergence of new technologies such as AR/VR, cloud computing, and artificial intelligence has introduced new demands for general-purpose simulation software, particularly in terms of flexibility.

<p align="center">
  <img src="\assets\blog\20230623\welsim_soft_archetect.png" alt="welsim_soft_archetect" />
</p>

Good software is now expected to run not only on local desktops but also be deployable on cloud servers. It should offer both local and remote high-performance computing capabilities, enabling a faster and more flexible invocation of various solvers. Great software should even achieve real-time simulation and rendering with immediate response. These updated requirements pose new challenges for the development of modern general-purpose simulation software. This article explores the design and architecture of modern large-scale general-purpose simulation software from a product perspective.


The design of any software aims to meet the product's positioning and customer requests. The design should be focused on essential features, as an excessively complex design can hinder the development process and delay product delivery. This is particularly vital for general-purpose software, which have a broad scope of applications and need minimalistic designs. A key aspect of the design includes foresight. As simulation software have relatively long development cycles, they require a design that anticipates trends 5 to 10 years in advance.



From the viewpoint of the product and users, this article proposes the following functions that a modern general-purpose simulation software should possess:

* Flexible mechanisms for inter-process invocation, communication, and data transfer. Have support for real-time computing and rendering capabilities.  The ability to call multiple solvers, mesh generators, and other computationally intensive executable programs.
* Provide simple and direct interfaces for external invocation, startup, shutdown, and interaction to facilitate easy implementation and maintenance of automated regression testing.
* User-friendly graphical interface that supports virtual reality and augmented reality, with display options extending beyond desktop monitors.
* Supports cloud computing, remote invocation, remote visualization, and team collaboration functionalities.
* Data exchanging interfaces for artificial intelligence-based automation analysis or solving.
* Weakly coupled interfaces and settings for multi-physics and multi-scale analyses.

<p align="center">
  <img src="\assets\blog\20230623\soft_design.png" alt="soft_design" />
</p>


Software architecture has an important link between design and development. It places high demands on architects. Due to the broad scope and intricate details large-scale general-purpose simulation software involves, it often requires a team with years of experience in simulation software development including a series of brainstorming and discussions. Currently, there is no official standard for the architecture of large-scale general-purpose software; they are mostly developed independently by major vendors. Having a universal architecture would benefit the entire industry and community. WELSIM has extensive authentic experience in developing a general-purpose engineering simulation software. Based on the mentioned design requirements, a practical and achievable solution has been proposed. Some aspects have already been applied in product development. It should be noted that the core objective of software architecture is to minimize maintenance costs, rather than implementing functionalities.


Now, let's explore the core concerns in the architecture of modern general-purpose simulation software, some solutions for those have already been implemented in WELSIM.


## Processes and communication
Modern simulation software place high demands on flexibility, as stated in the first design requirement above. Managing and scheduling multiple executable programs is inevitable in large-scale software, and inter-process communication is also crucial. However, there is no industry standard for multi-process management, necessitating customized architecture and development based on the product's functions and requirements. WELSIM has designed a process management and communication mechanism based on WebSocket and RPC interfaces. The WebSocket interface is used for communication between the GUI main program and the Daemon program, while the RPC interface is used for communication between the smaller executable programs such as solvers and the Daemon. RPC communication uses the JSON data format, and for large data, a direct memory read/write or binary file formats can be utilized.

<p align="center">
  <img src="\assets\blog\20230623\welsim_processes.png" alt="welsim_processes" />
</p>

As shown in the figure above, when the main program (GUI) starts, it simultaneously launches necessary child processes. Among them, daemon.exe serves as the control node for all child processes, acting as a controller that connects the main program with other programs (e.g., solvers) and supports WebSocket communication. start_solvers.exe is the control process for solvers supporting RPC communication. Considering that general-purpose simulation software may have multiple solvers, it supports dynamically adding and removing child processes. start_node.exe represents the control information of the local machine in the network, facilitating the discovery of peers and enabling shared collaboration and control. start_mesher.exe has a similar role to start_solvers.exe, controlling the mesh generation. start_data_layer.exe controls the local data layer for sharing computational data.

This architecture involves two communication mechanisms. WebSocket is a protocol that enables full two-way communication over a single TCP connection. The server and client can establish a permanent connection and perform bidirectional data transmission. RPC is a method to request services over a network without needing to understand the underlying network technology.  On a local machine, it can be used for both network and inter-process communication. The RPC port is configured through a configuration file and allows users to modify it while using default port settings. The RPC port is not open to the Internet. TLS certificates are used to ensure communication security. Next, alongside the architecture design in this article, we will discuss in detail the implementation of these two interfaces in general-purpose simulation software.

### WebSocket API service

When the main application runWelSim.exe is launched, the Deamon service is started simultaneously. Deamon acts as the server, while runWelSim.exe acts as the client, establishing a permanent bidirectional communication using the JSON format. As the server, Deamon receives requests from the front end, such as meshing, solving, cloud computing, remote sharing, etc. After processing, it dispatches various subprocesses to complete the tasks. Thanks to bidirectional communication, Deamon provides real-time progress updates to the front end. In real-time simulation applications, Deamon notifies the corresponding solver to perform calculations and returns the results of each step to the front end immediately. Upon receiving the computation results, the front-end program updates relevant displays, such as real-time rendering results or cloud charts.

Another advantage of using WebSocket in Deamon is that the frontend program can be either a desktop application or a web application. There are no specific requirements for the front-end development framework or programming language. After years of use on the desktop platform, the product can be ported to the cloud platform with minimal effort. It's worth mentioning that WebSocket involves a significant number of asynchronous calls in practical coding, and developers need to have an understanding of relevant network service technologies.

<p align="center">
  <img src="\assets\blog\20230623\welsim_websocket.png" alt="welsim_websocket" />
</p>


### RPC API service
RPC is a remote procedure call mechanism based on the "request/response" model, with a high transmission efficiency and support for both local and remote communications. That's why it's the preferred choice for subprograms in large-scale simulation software. From a programming perspective, the RPC API here is an asynchronous function in a "request/response" style. All subprocesses belonging to Deamon, such as solvers, nodes, etc., provide RPC services and accept real-time calls from clients. As shown in the diagram below, Deamon can access its subprocesses, and the subprocesses promptly return JSON-formatted data to the Deamon client, including a field indicating the success or failure of the call.

<p align="center">
  <img src="\assets\blog\20230623\welsim_rpc_api.png" alt="welsim_rpc_api" />
</p>


From a security perspective, not all RPC ports should be publicly exposed. For example, the ports of the Nodes and DataLayer processes should be kept private. On the other hand, solver ports can be publicly exposed to facilitate quick client calls. The RPC command design mainly includes functions like get/set, and each command has a help flag option. Other developers or users can quickly learn about the designed RPC methods and return content using the -h flag. Access to RPC can be implemented in different languages such as Python, C++, or JavaScript. There are many open-source packages available for development, like gRPC and OpenRPC.


## GUI design and architecture
The graphical user interface (GUI) is one of the key technologies in the development of large-scale general-purpose simulation software. A good GUI must have various simulation requirements for different physical types, be easy to maintain and expand functionalities, and provide an intuitive, user-friendly, and feature-rich interface that allows users to conveniently and quickly perform operations such as preprocessing, and result viewing. It is a complex and long-term development process. After years of development and iteration, WELSIM has refined its frontend GUI module. The overall design of this software-human interaction is presented below.

<p align="center">
  <img src="\assets\blog\20230623\welsim_gui_windows_overview.png" alt="welsim_gui_windows_overview" />
</p>

1. Menu bar: used to display all available commands.
2. Toolbar: used to display commonly used commands. Depending on the product requirements, traditional individual buttons can be used. When there are many commands, the popular Ribbon layout can be used to accommodate more commands.
3. Project tree window: users can conveniently add, edit, copy, or delete nodes, allowing dynamic control of the components used in simulation analysis. The right-click context menu in the window is vital in implementing these functions. In the bottom right corner of each object icon, the object status engine displays the current state of the node, such as success, error, or undefined.
4. Property window: the property window is a powerful addition to the project tree and is often placed below the project tree window. It serves as the main interface for simulation data input. The property window dynamically displays the data content of the current object, allowing users to input or modify data.
5. 3D Graphics window: the 3D graphics window occupies the main space on the screen and is the main module of the simulation software. Therefore, there are many components that need to be displayed, which then leads to challenges in design and architecture. The 3D window involves a large number of mouse and keyboard interaction operations, which require careful design and development. The design of mouse interactions needs to follow the user's intuition and habits while being innovative and user-friendly.
6. Output window: the output window displays various textual information generated by the system and is often placed at the bottom of the screen. The most important function of the output window is to provide prompts for errors and warning messages and guide users in problem-solving.
7. Console window: similar to the output window, modern simulation softwares also support a console command window, such as input control for interpreted languages like Python. For some users, it can meet the needs for secondary development and also provide an interface for automated testing systems.
8. Table window: the table window is mainly used for displaying data and sometimes provides the ability to modify data. As a general-purpose simulation software, the table needs to support various types of data and units, such as boundary condition data, result data, material test data, curve fitting data, etc. It should support functions like unit modification, data sorting, data import/export, and more.
9. Chart window: the chart window is used to display 2D curves and share data with the table window. It's usually placed below the table window. Visualizing the table data through graphics and curves is an important aspect to enhancing user experience. The chart window can also include animation display controllers for commonly used animation display and video generation in post-processing.
10. Additional main windows: for complex data input and display, additional main windows are needed. For example, when data editing various materials, the input and display of large tables, etc. They can be displayed parallel to the 3D graphics window via new tabs.
11. Pop-up windows: depending on the type and importance of commands, pop-up windows are presented to the user. Though, it is generally advised to use them minimally.

For a detailed introduction to GUI design and development in large-scale general-purpose software, you can refer to the articles "[Design and development of context menu in simulation software](https://welsim.com/2023/05/21/design-and-development-of-context-menu-in-simulation-software.html)" and "[Window design and development for general-purpose simulation software](https://welsim.com/2023/05/28/window-design-and-development-for-general-purpose-simulation-software.html)".


<p align="center">
  <img src="\assets\blog\20230623\welsim_desktop_vs_web.png" alt="welsim_desktop_vs_web" />
</p>

Although a desktop GUI has significant advantages in the field of general-purpose simulation and can meet the needs of almost all users, software design and architecture requires foresight, including that, GUI design and development are no exception. When considering future native web-based GUIs, front-end frameworks based on JavaScript such as Electron can be used for development. This allows the cloud-based web GUIs to develop while also maintaining the desktop user interface.

## Automated regression system
An automated regression testing system is essential for large-scale software. This is especially true for engineering simulation software, where software stability and numerical accuracy within error tolerance are crucial. A well-designed automated regression system is needed. Typically, automated testing is structured in a testing pyramid, including unit testing, integration testing, and end-to-end UI testing. Unit testing is used to verify the small-scale algorithms, such as unit tests for unit conversions in WELSIM to ensure the accuracy of unit-related calculations. Integration testing is used to test executable programs like Deamon, where calculations are performed based on WebSocket input, and the results are verified. Front-end UI testing nominally tests the user interface but also verifies numerical results. The duration of these three types of testing increases with complexity. For large-scale products, the most effective testing approach is end-to-end testing from the user's perspective, making a testing system closely tied to GUI operations the most efficient. This is crucial for the overall quality control of the product.

<p align="center">
  <img src="\assets\blog\20230623\test_pyramid.png" alt="test_pyramid" />
</p>

Therefore, establishing a UI automated testing system is invauable for large modern simulation software. To achieve this, it is mainly done by establishing associations with the GUI framework, primarily using observer patterns, which can be implemented through events, callbacks, or signal/slot mechanisms. WELSIM's proposed automated testing system includes a middleware that provides commands to the front-end interface and reads the UI's state. It also includes a client for testing personnel to use. As shown in the figure below, the middleware is mainly divided into two modules: the translator and the player, which are responsible for controlling and reading the GUI.

<p align="center">
  <img src="\assets\blog\20230623\welsim_testbench_fw.png" alt="welsim_testbench_fw" />
</p>

The client of the automated operation system is like another software. Apart from controlling WELSIM's UI through the middleware, it also needs to maintain a complete set of test files and historical data. The automated testing client should have the following functionalities:
* Allow adding, modifying, and deleting various test cases.
* Generate test reports for easy searching and tracking.
* Fully automated execution without manual intervention.
* Validate attribute values, handle program crashes, infinite loops, image pixel comparisons, etc.
* Test files should only require the scripts without any additional dependency libraries or programs.

Currently, WELSIM's automated testing framework is repeatedly being improved and updated. So, there is a possibility of open-sourcing the testing framework and the validation cases to contribute to the open-source and simulation communities.

## Cloud computing and network connection
Modern general-purpose simulation softwares need better adaptability for network support. Thanks to the multi-process design and RPC services, the framework described in this article can effectively meet the requirements for cloud computing and support complex networks. The Nodes process manages the network connections and communication with other machines, while the DataLayer process is responsible for managing, storing, and publishing data. Its built-in RPC service allows for quick support of various network applications. Additionally, encryption methods such as TLS certificates are applied to enhance network security. For large data, DataLayer performs data compression and decompression to improve network transmission efficiency.

<p align="center">
  <img src="\assets\blog\20230623\welsim_cloud_computing.jpg" alt="welsim_cloud_computing" />
</p>

## Miscellaneous
Due to the space limitations, many other topics in this article cannot be described in detail, such as:

* CAD geometry kernel.
* Mesh generators and solvers, along with their high-performance implementations. Computationally intensive process invocation and communication.
* Post-processing and visualization development, VR/AR implementation. Report generation.
* Data persistence.
* Secondary development features, script control functionality, integration, and development of plugins.
* Globalization and localization, multi-language support.
* Multi-physics coupling.
* Multi-scale coupling.
* Coupling with optimization tools and uncertainty quantification tools.

The above topics may be discussed in dedicated articles in the future.

## Conclusion
The architecture of a large-scale software is a complex task. Furthermore, making it a general-purpose simulation software is even extra complicated due to the various numerical methods and applications involved. The software needs to cover a wide range of computations while keeping up with the latest technologies, such as real-time simulation, cloud computing, artificial intelligence, VR/AR, and 3D printing. This poses many challenges for product managers and architects. The RPC-based modern simulation software architecture proposed in this article can meet these requirements and provide a solid foundation for the long-term maintenance of the product.

The architecture of large-scale software should align with the product positioning and the needs of the clients. Designs that compromise product consistency should be discarded. Removing unnecessary features is a core part of the design for modern large-scale general-purpose simulation software. The architectural approach presented in this article can also be applied to other modern large-scale software.


---

<small>
WELSIM is the #1 engineering simulation software for the open-source community.
</small>
