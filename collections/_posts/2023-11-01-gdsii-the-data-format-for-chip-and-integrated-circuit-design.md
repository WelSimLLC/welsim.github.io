---
lang: en
layout: post
title:  "GDSII, the data format for chip and integrated circuit design"
date:   2023-11-01
author: "[SimLet](https://twitter.com/getwelsim)"
---

GDSII, short for Graphic Design System, is a data format used for the exchange of integrated circuit or layout data in Electronic Design Automation (EDA). It is a binary file format that represents planar geometric shapes, text labels, and related layout information in a hierarchical manner. Over the past 30 years, GDSII has become a standard, with almost all EDA software and hardware systems supporting it.
<p align="center">
  <img src="\assets\blog\20231101\welsim_ic_design.png" alt="welsim_ic_design" />
</p>


GDSII was developed as a standard in the 1980s by Calma, and ownership passed from Calma to GE, then to Valid, and finally to Cadence over the years. Although versions have gone through iterative updates, the format and syntax have remained essentially unchanged. GDSII has consistently served as the industry-standard database for integrated circuit layouts. Despite significant developments in OASIS, GDSII still remains the primary format for describing the physical layout of chips. In part, the long lifespan of GDSII can be attributed to its elegant architecture and simplicity. Additionally, the presence of a vast legacy codebase may contribute to the slow adoption of alternative solutions like OASIS.


This article provides examples to help readers quickly understand the GDSII format and how to read and write GDS files.

<p align="center">
  <img src="\assets\blog\20231101\welsim_gds_layers.png" alt="welsim_gds_layers" />
</p>

## GDSII Format
The GDSII file format is clear and straightforward, defining the file's library, structure, and various parameters through keywords. This article focuses on what one may encounter when working on CAD/CAE/EDA projects.

### Library records
The GDSII file always begins with the HEADER record, which includes the version number being used. Next, the BGNLIB record documents the date of the last modification and last access to the file. LIBNAME records the document's name. Following this are optional file header record: REFLIBS, FONTS, ATTRTABLE, GENERATIONS, and FORMAT. The final record in the file header must be UNITS, which records units and precision. After the file header, there is the structure section. When all the information is defined, the file concludes with the ENDLIB record.

```
HEADER 600 
BGNLIB 10/31/2023 14:28:48 10/31/2023 14:28:48 
LIBNAME WelSim_First
UNITS 0.001 1e-09 
…
ENDLIB
```

### Structure records
Each structure has two header records and one tail record, enclosing an arbitrary list of elements. The first structure header record is BGNSTR, which includes the creation date and last modification date. Following this is the STRNAME record. Then, the structure section is open, allowing for the listing of one of seven elements: BOUNDARY, PATH, SREF, AREF, TEXT, NODE, BOX. The final record for a structure is ENDSTR. Following it must be another structure section or the conclusion of the entire library, ENDLIB.

```
BGNSTR
STRNAME
...
ENDSTR
```


### Boundary Element
The boundary element defines a filled polygon. It begins with the BOUNDARY record and may include optional records ELFLAGS and PLEX. Following these, it must include the LAYER, DATATYPE, and XY records. The LAYER record is used to specify the layer for this boundary (numbered from 0 to 63). The DATATYPE record contains insignificant information, and its parameter should be zero. The XY record includes a variable number of coordinate pairs, ranging from four pairs to 200 pairs, to define the outline of the polygon. The number of points in this record is determined by the length of the record. It's important to note that since the boundary must be closed, the first and last coordinate values must be the same.

<p align="center">
  <img src="\assets\blog\20231101\welsim_gds_box.png" alt="welsim_gds_box" />
</p>

```
BOUNDARY 
LAYER 0 
DATATYPE 0 
XY 0: 0
0: 1000
2000: 1000
2000: 0
0: 0
ENDEL
```

### Path Element
A path is an open graphic with non-zero width, typically used for placing conductor wires. It begins with the PATH record, followed by optional ELFLAGS and PLEX records. Next, the LAYER record must be included to specify the desired path material. Additionally, a DATATYPE record and an XY record must be present to define the path's coordinates. A path can include anywhere from two to 200 points. Before the XY record in the path specification, there are two optional records: PATHTYPE and WIDTH. The PATHTYPE record describes the nature of the endpoints of the path segment. If its value is 0, the segment will have square endpoints terminating at the path vertices. A value of 1 indicates round endpoints, and a value of 2 indicates square endpoints with a width equal to half their width. The width of the path is defined by the optional WIDTH record. If the width value is negative, it will scale independently of any structure.

<p align="center">
  <img src="\assets\blog\20231101\welsim_gds_path.png" alt="welsim_gds_path" />
</p>

```
PATH 
LAYER 1 
DATATYPE 0 
PATHTYPE 0 
WIDTH 500 
XY 0: 0
0: 10000
20000: 0
18000: 15000
8000: 15000
ENDEL
```



### SREF Element
The SREF record represents a structure reference, allowing structures to be referenced within other structures, thereby achieving hierarchy. Following this are optional ELFLAGS and PLEX records. Next, the SNAME records the name of the structure required, and the XY record contains a single coordinate to place this structure. Before the XY record, there may be optional transformation records. If structure transformation is needed, the STRANS record must appear first.


<p align="center">
  <img src="\assets\blog\20231101\welsim_gds_sturcture_ref.png" alt="welsim_gds_sturcture_ref" />
</p>

```
BGNSTR 10/31/2023 14:28:48 10/31/2023 14:28:48 
STRNAME Square
SREF 
SNAME Circle
XY -10000: 5000
ENDEL 

BOUNDARY 
LAYER 0 
DATATYPE 0 
XY -15000: 0
-15000: 10000
-5000: 10000
-5000: 0
-15000: 0
ENDEL 
ENDSTR
```

### AREF Element
In addition to the SREF used for individual structures, GDSII also has the AREF (array reference) element, which can place one-dimensional or two-dimensional structure arrays. This is particularly useful for many integrated circuit layouts, including memory. After the optional ELFLAGS and PLEX records, there is the SNAME record to specify the structure being arrayed. Following this, optional transformation records STRANS, MAG, and ANGLE provide the orientation of instances. The COLROW record must then appear to specify the number of columns and rows in the array. The final record is an XY record, which contains three points: the coordinates of the origin instance, the coordinates of the last instance in the column direction, and the coordinates of the last instance in the row direction.

<p align="center">
  <img src="\assets\blog\20231101\welsim_gds_aref.png" alt="welsim_gds_aref" />
</p>

```
BGNSTR 10/31/2023 11:56:33 10/31/2023 11:56:34 
STRNAME ARRAY_EX
AREF
SNAME WELSIM_RECT
ANGLE 10
COLROW 5 3 
XY 0: 0
20000: 0
0: -10000
ENDEL
ENDSTR
```

### Text Element
Text can be included in a circuit using the TEXT record. It starts with the TEXT keyword, followed by optional ELFLAGS and PLEX records. Next is the required LAYER record. Then, a TEXTTYPE record with zero parameters must appear. The optional PRESENTATION record specifies the font. Optional PATHTYPE, WIDTH, STRANS, MAG, and ANGLE records can adjust the text. The last two records are mandatory: an XY record with a single coordinate to position the text and a STRING record to express the actual text.

<p align="center">
  <img src="\assets\blog\20231101\welsim_gds_text.png" alt="welsim_gds_text" />
</p>

```
TEXT 
LAYER 0 
TEXTTYPE 2 
PRESENTATION 0 
XY 5000: 3000
STRING WelSim label
ENDEL
```

### Node Element
The NODE record can specify circuit information. The information in this element is not graphical and does not affect the manufactured circuit; instead, it is intended for use by other CAD systems that utilize topological information. Further details are beyond the scope of this article.

```
NODE
LAYER 21
NODETYPE 1
XY 123000: 124500
123000: 103500
126000: 103500
126000: 124500
123000: 124500
ENDEL
```

### Box Element
The last element in a GDSII file is the BOX element. After the BOX record, there may be optional ELFLAGS and PLEX records, followed by the required LAYER record. It also includes a BOXTYPE record with zero parameters and an XY record. The XY record must contain five points, describing a closed rectangle. Unlike a boundary, this is not a filled graphic; therefore, it is not used to describe the geometric shape of an integrated circuit.

<p align="center">
  <img src="\assets\blog\20231101\welsim_gds_box.png" alt="welsim_gds_box" />
</p>

```
BOX 43 2
92000 -7000
106000 -7000
106000 19000
92000 19000
92000 -7000
ENDEL
```

## Reading and Writing GDS Files
In addition to commercial software vendors, there are many free GDSII tools available. These free tools include editors, viewers, utilities for converting 2D layout data to a generic 3D format, utilities for converting binary formats to readable ASCII formats, and libraries. Through testing and use, the author has found:
1. KLayout is an open-source circuit layout visualization and editing tool. It's user-friendly and suitable for beginners. The open-source code is also suitable for in-depth learning. It supports the conversion of binary GDS files to human-readable ASCII text.
2. gdstk is an open-source GDS I/O library based on C++ with a friendly interface, making it suitable for use in commercial GDS-related projects. There is also a Python version available.
3. Developing custom applications related to GDSII is not complex and can be combined with other CAD kernel modules and 2D/3D display modules to achieve more advanced functionality.


## Conclusion
GDSII is a simple syntax two-dimensional CAD file format commonly used in integrated circuit and chip design. The GDS ecosystem is rich, with extensive support from both commercial and open-source software, making it user and developer-friendly. If you are developing EDA/CAE software, support for GDSII files may be necessary.

---


<small>
_WelSim is not affiliated with GDSII, OASIS, Cadence, KLayout, or gdstk. The development team and organization behind GDSII, OASIS, Cadence, KLayout, and gdstk have no connection to WelSim. This reference is used here solely for the purpose of a technical blog article and software usage._
</small>
