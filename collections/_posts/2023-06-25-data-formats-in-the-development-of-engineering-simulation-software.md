---
lang: en
layout: post
title:  "Data formats in the development of engineering simulation software"
date:   2023-06-25
author: "[SimLet](https://twitter.com/getwelsim)"
---

Data is one of the core components of engineering software, and the stability of data reading, writing, conversion, and manipulation is crucial for the performance of engineering software. General-purpose engineering simulation CAE software is no exception, and due to its long research and development cycle, it also places high demands on maintainability. Simulation software covers a wide range of fields, involving data persistence commonly used in software engineering, and computational results such as node and element data solved using finite element and finite volume methods, thus various data formats are needed to implement different features.

<p align="center">
  <img src="\assets\blog\20230625\welsim_data.png" alt="welsim_data" />
</p>


Choosing the right data format can greatly improve product performance and maintainability, while also benefiting developers by saving development time and resources. Based on years of practical experience in developing WELSIM, this article discusses data formats and application concepts in general-purpose engineering simulation software.

## Geometric shape data
The entry point for general-purpose simulation software is geometric models, commonly referred to as CAD models by engineers. Since the core of CAE simulation software lies in computation and analysis, the primary method to obtain geometric data is by reading CAD models rather than generating them from scratch.
<p align="center">
  <img src="\assets\blog\20230625\welsim_data_cad.png" alt="welsim_data_cad" />
</p>


Currently, the most suitable geometric data format for simulation software is STEP. STEP was introduced in the 1980s and is still widely used today. The STEP format provides a clear and precise representation of the entire 3D model, including not only the basic geometric shape but also the topology, allowing for high-precision reading and storage. It supports length units and is capable of meeting the requirements of the majority of CAE applications. Well-known cloud-based CAD vendor OnShape exports CAD data in the STEP format, and the popular open-source geometry engine OpenCascade also provides excellent support for STEP, facilitating its application and compatibility. Currently, STEP is the primary CAD file import format for WELSIM.

There are also other well-known geometric data formats such as JT, ACIS, and Parasolid. Due to the space limitations of this article, they may be discussed in future articles.

In addition to complete geometric data formats, there is another category represented by STL, which contains only surface information. This type of data does not include topological information but consists of triangular mesh data representing the surface. With the recent rise of 3D printing, such data formats as STL have become popular. However, their application in general CAE analysis is somewhat limited due to the lack of topological and volumetric information.
<p align="center">
  <img src="\assets\blog\20230625\welsim_data_stl.png" alt="welsim_data_stl" />
</p>


## Mesh data
Mesh data is the most important input data for engineering simulation software, characterized by its large volume and diverse types. Balancing performance and versatility is the primary criterion for selecting a mesh data format. After years of practical development and customer feedback, WELSIM considers UNV and PVTU as two excellent formats for mesh data.
<p align="center">
  <img src="\assets\blog\20230625\welsim_data_mesh.png" alt="welsim_data_mesh" />
</p>



UNV is a general-purpose neutral mesh data format proposed by I-DEAS. It has clear and easily understandable field definitions and is easy to implement in programming. UNV supports a wide range of element types and includes a group module that allows the definition of various boundary conditions and contacts. It is widely accepted and effective in the industry. In practical applications, the default format is ASCII text, but developers can also use tools like gzstream to convert it to binary files.

PVTU is an unstructured mesh format based on VTU proposed by Kitware. Its distinctive feature is its support for multi-core parallel reading and writing, greatly improving the speed of mesh file operations. The underlying version, VTU, is an XML-based data format, and the core data can be stored in either ASCII or binary formats, meeting different usage scenarios.


## Material data
Engineering software involves a large amount of material data. Although the data volume for materials is not as large as mesh or result data, it may still include test data and other content, making it medium size. XML is a good choice as it balances readability, read/write efficiency, and support for web-based applications. There is currently no universal data format standard for materials due to their diverse types, and most software vendors design their own formats. Both WELSIM and MatEditor software uses XML format as their text data format, demonstrating excellent performance. It is worth noting that material data often includes numerous units. When designing the format, it is advisable to reuse existing units as much as possible to reduce file size and improve read/write efficiency.
<p align="center">
  <img src="\assets\blog\20230625\welsim_data_material.png" alt="welsim_data_material" />
</p>



## Solver input data
Solver control input data, referred to as solver files, typically separate the mesh data from the control commands. As a result, solver files are not large in size, and ASCII text format is suitable for this purpose. The format of solver files primarily depends on the specifications of the solver. If it is a customized solver, using JSON can quickly implement the reading and writing of solver files, making it a good choice. Additionally, JSON inherently supports RPC communication, providing a foundation for remote invocation of the solver and reducing maintenance costs. Some traditional solver formats also have widespread use, such as Calculix using the Abaqus format, and Dyna and Nastran formated are widely applied as well.
<p align="center">
  <img src="\assets\blog\20230625\welsim_data_solver.png" alt="welsim_data_solver" />
</p>



## Result data
Result data is the most crucial and voluminous data in simulation software. Depending on the solution, result files may or may not include mesh data. For solving processes that involve adaptive mesh, the result file size will be significantly increased because of the containing mesh.

Similar to mesh data, VTU is currently the best format for result data. It has an open-source library and friendly licensing, enabling quick reading and writing of VTU result files. Although it is based on XML data format, it also supports saving the large data portion in binary format. PVTU supports parallel result files, effectively utilizing multi-core hardware resources and increasing read/write efficiency. For multi-step analysis, result files can be read and written using the PVD format, which is based on the VTU. PVD is the default file format of the open-source software Paraview. For more details, refer to the article "ParaView Data (pvd) file format and writing." Thanks to the ecosystem of VTK and Paraview, VTU result files are widely compatible.
<p align="center">
  <img src="\assets\blog\20230625\welsim_data_result.png" alt="welsim_data_result" />
</p>



## Cache data
Caching is widely used in operating systems and various software applications. In the CAE simulation, caching methods are used at various stages to store temporary computational results, user operations, and other data. Caches can be stored in project or computing directories, as well as in the temporary folder of the operating system.

SQLite can be used for some cache files, such as cache during meshing generation, cache at solving, GPU computing cache, local storage cache, etc. SQLite offers fast read/write speeds and is easily scalable. Cache files can be designed in a specific format according to requirements.
<p align="center">
  <img src="\assets\blog\20230625\welsim_data_cache.png" alt="welsim_data_cache" />
</p>


## RPC interaction data
Modern general-purpose simulation software requires higher flexibility. Using RPC communication and process management mechanisms is undoubtedly the best implementation approach. For more details, refer to the article "(Design and architecture of modern general-purpose engineering simulation software)[https://welsim.com/2023/06/23/design-and-architecture-of-modern-general-purpose-engineering-simulation-software.html]." In RPC communication, TLS is inevitably needed to ensure security. This includes certificates and key files (containing public and private keys) encrypted with RSA, usually in ASCII text format. Other types of files required for RPC may be in YAML format, and the content can be in JSON format.


## Project persistence data
Project persistence is an essential feature of a complete set of engineering software. The design quality of project persistence data directly affects the development efficiency of the product and the stability of backward compatibility with previous versions. The core of project persistence data in CAE software is the tree objects and their property data. WELSIM utilizes the HDF5 format, which exhibits excellent performance and maintainability. The compression feature of HDF5 can also handle large data within projects. HDF5 provides a rich set of open-source packages for reading and writing H5 files, and the official HDFView tool is available to open and browse H5 files.
<p align="center">
  <img src="\assets\blog\20230625\welsim_data_persistence.png" alt="welsim_data_persistence" />
</p>


## Configuration data
A mature software product has various configuration files that can be customized or modified for different settings and can be persistently stored for GUI settings. The requirements for configuration files are strong readability and ease of understanding, as they need to allow users from different areas to modify the files. YAML (Yet Another Markup Language) is a highly readable and expressive data interchange format that uses a concise and easy-to-read syntax to represent data. It supports features such as comments and multi-line strings, making configuration files easier to write and maintain. YAML is very suitable as a configuration data file format.
<p align="center">
  <img src="\assets\blog\20230625\welsim_data_config.png" alt="welsim_data_config" />
</p>



Some large framework software also provides the automatic generation of configuration files. For example, the QSettings provided by QT can write to different locations based on the operating system without developer intervention, which is also a good way to handle configuration data.


## Log
There are various types of log files, including user operation logs, solver logs, and even logs for software defects. In general, ASCII-formatted TXT files are used for ease of reading. It is important to include timestamps in log files. Additionally, when log files become too large, it is necessary to automatically create a new log file with a different name to store new log data.

## Conclusion
The development of general-purpose engineering simulation (CAE) software is a massive undertaking. Developers need to optimize development resources to deliver products and features as quickly and efficiently as possible while ensuring good maintainability. The data formats summarized in this article have been successfully applied in the development of WELSIM software, demonstrating excellent performance, low maintenance costs, and ease of expansion. They serve as a good reference for software development and data format selection. The data formats discussed in this article are summarized as follows:
<p align="center">
  <img src="\assets\blog\20230625\welsim_data_sum_table_en.png" alt="welsim_data_sum_table_en" />
</p>

Due to space limitations, this article focuses on narrowing down the discussion of data formats, specifically for CAE software. For startup software, it is advisable to choose neutral file formats that offer high versatility. Some neutral formats may also have open-source packages available, which can expedite product development.

---

<small>
WELSIM is the #1 engineering simulation software for the open-source community.
</small>
