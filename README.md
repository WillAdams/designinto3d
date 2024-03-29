---
description: A system for parametric design of projects for CNC or traditional techniques
---

# Introduction

Design into 3D is an effort to create a systematic set of design and fabrication techniques and project generators for objects made using CNC machines, documenting things well enough that one would be able to draw up traditional plans using pen and pencil and fabricate an instance of a project using hand tools, or create files which will efficiently and correctly make toolpaths for cutting on a CNC.

It is simultaneously:

* an opensource project which is a collection of projects for objects such as boxes, furniture, and tools (available on [https://cutrocket.com/u/WillAdams](https://cutrocket.com/u/WillAdams) and [https://www.thingiverse.com/willadams/designs](https://www.thingiverse.com/willadams/designs) and [https://github.com/WillAdams/Design\_Into\_3D/](https://github.com/WillAdams/Design\_Into\_3D/))
* a [Kickstarter](https://www.kickstarter.com/projects/designinto3d/design-into-3d-a-book-of-customizable-project-desi)
* a book
* an ebook (you are here)
* a paper submitted to the TeX User's Group 40th Anniversary 2019 conference [https://www.tug.org/tug2019/program.html](https://www.tug.org/tug2019/program.html) ― Design into 3D is a system for modeling parametric projects for manufacture using CNC machines. It documents using OpenSCAD to allow a user to instantly see a 3D rendering of the result of adjusting a parameter in the Customizer interface; parameters are then saved as JSON files which are then read into a LuaLaTeX file which creates a PDF as a cut list/setup sheet/assembly instructions and METAPOST to create SVG files which may be loaded into a CAM tool. [http://tug.org/TUGboat/tb40-2/tb125adams-3d.pdf](http://tug.org/TUGboat/tb40-2/tb125adams-3d.pdf)
* a website: [https://designinto3d.com/](https://designinto3d.com/)
* a design philosophy

The design philosophy touches on the idea that fundamentally there are only two types of furniture:

* platforms
* boxes

with more complicated pieces incorporating both structures, and that any object is fundamentally described in two ways:&#x20;

* its design
* its dimensions

Currently it uses [BlockSCAD](https://www.blockscad3d.com/) and [OpenSCAD Graph Editor ](https://github.com/derkork/openscad-graph-editor)as front-ends to [OpenSCAD](https://wiki.shapeoko.com/index.php/OpenSCAD), a 3D modeling tool which can then afford a comfortable front-end using the [customizer feature](https://github.com/openscad/openscad/issues/1781) in OpenSCAD which is available in current versions.[\[1\]](http://www.openscad.org/news.html#20190518) A new development is that it is now possible to load OpenSCAD files into a web browser using: [https://github.com/seasick/openscad-web-gui](https://github.com/seasick/openscad-web-gui) which will make available files from GitHub or Printables.com and then export to DXF, SVG, or STL.



There are several possible approaches for making designs from BlockSCAD/OpenSCAD:

* use the Projection() command to allow the exporting of a 2D view of the design as a DXF or SVG which may then have toolpaths made using a traditional CAM tool
* directly export the 3D design as an STL which may then have toolpaths made using a 3D CAM tool such as MeshCAM or pyCAM
* import the OpenSCAD file into FreeCAD and use the Path Workbench to create G-Code
* exporting the parameters from the customizer as a preset in a JSON file (which is stored in the same directory as the OpenSCAD source file) the JSON may then be loaded into a program developed using a second language which generates a design using those parameters ― eventually for cutting, or toolpaths without further user intervention. As an example, the initial implementation of this from the afore-mentioned paper in _TUGboat_ uses [METAPOST](https://wiki.shapeoko.com/index.php/METAPOST) via the library embedded in [LuaTeX](http://luatex.org/) and importing the JSON file using the [Lua scripting language](http://www.lua.org/)
* from within OpenSCAD (or some other programming/modeling tool) develop the design so that toolpaths are modeled and the coordinate information may be exported as G-Code commands ― RapCAD (a fork of OpenSCAD) gained the ability to write out files in v1.0.2, see: [https://forum.makerforums.info/t/g-code-preview-using-openscad-rapcad/85729](https://forum.makerforums.info/t/g-code-preview-using-openscad-rapcad/85729/10)

The first and last two options will be explored in the course of this text.

An alternative which is worth exploring is working up a program in a general-purpose programming language and writing out in parallel both .scad code for a 3D model as a preview, and G-Code for actually cutting out the parts. Two examples of this approach are:

* LiveCode: [https://community.carbide3d.com/t/previewing-g-code-using-openscad/35153/12](https://community.carbide3d.com/t/previewing-g-code-using-openscad/35153/12)
* Python: [https://community.carbide3d.com/t/previewing-g-code-using-openscad/35153/27](https://community.carbide3d.com/t/previewing-g-code-using-openscad/35153/27)

This online ebook is available under a Creative Commons license: Attribution-NonCommercial-ShareAlike 3.0 Unported (CC BY-NC-SA 3.0) [https://creativecommons.org/licenses/by-nc-sa/3.0/](https://creativecommons.org/licenses/by-nc-sa/3.0/)

The Kickstarter edition and print versions are available under a license which will allow commercial usage to a reasonable degree.

Please contact [willadams@aol.com](mailto:willadams@aol.com) if you wish to arrange for any other sort of arrangement.
