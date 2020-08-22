---
description: A system for parametric design of projects for CNC or traditional techniques
---

# Introduction

Design into 3D is an effort to create a systematic set of design and fabrication techniques and project generators for objects made using CNC machines, documenting things well enough that one would be able to draw up traditional plans using pen and pencil and fabricate an instance of a project using hand tools, or create files which will efficiently and correctly make toolpaths for cutting on a CNC.

It is simultaneously:

* an opensource project which is a collection of projects for objects such as boxes, furniture, and tools \(available on [https://cutrocket.com/u/WillAdams](https://cutrocket.com/u/WillAdams) and [https://www.thingiverse.com/willadams/designs](https://www.thingiverse.com/willadams/designs) and [https://github.com/WillAdams/Design\_Into\_3D/](https://github.com/WillAdams/Design_Into_3D/)\)
* a [Kickstarter](https://www.kickstarter.com/projects/designinto3d/design-into-3d-a-book-of-customizable-project-desi)
* a book \(currently in early draft stages\)
* an ebook \(you are here\)
* a paper submitted to the TeX User's Group 40th Anniversary 2019 conference [https://www.tug.org/tug2019/program.html](https://www.tug.org/tug2019/program.html) ― Design into 3D is a system for modeling parametric projects for manufacture using CNC machines. It documents using OpenSCAD to allow a user to instantly see a 3D rendering of the result of adjusting a parameter in the Customizer interface; parameters are then saved as JSON files which are then read into a LuaLaTeX file which creates a PDF as a cut list/setup sheet/assembly instructions and METAPOST to create SVG files which may be loaded into a CAM tool. [http://tug.org/TUGboat/tb40-2/tb125adams-3d.pdf](http://tug.org/TUGboat/tb40-2/tb125adams-3d.pdf)
* a website: [https://designinto3d.com/](https://designinto3d.com/)
* a design philosophy

The design philosophy touches on the idea that fundamentally there are only two types of furniture \(and arguably objects\):

* platforms
* boxes

with more complicated pieces incorporating both structures, and that any object is fundamentally described in two ways: 

* its design
* its dimensions

Currently it uses [BlockSCAD](https://www.blockscad3d.com/) and [OpenSCAD](https://wiki.shapeoko.com/index.php/OpenSCAD) as a 3D modeling front-end using the [customizer feature](https://github.com/openscad/openscad/issues/1781) in OpenCAD which is available in current versions.[\[1\]](http://www.openscad.org/news.html#20190518) 

There are several possible approaches for making the design:

* use the Projection\(\) command to allow the exporting of a 2D view of the design as a DXF or SVG which may then have toolpaths made using a traditional CAM tool
* directly export the 3D design as an STL which may then have toolpaths made using a 3D CAM tool such as MeshCAM or pyCAM
* import the OpenSCAD file into FreeCAD and use the Path Workbench to create G-Code
* When the parameters for a suitable design are entered into the customizer they may be saved as a preset in a JSON file which is stored in the same directory as the OpenSCAD source file. while the JSON may then be loaded into a file which generates a design using those parameters ― eventually for cutting, or toolpaths without further user intervention. The initial implementation of this uses [METAPOST](https://wiki.shapeoko.com/index.php/METAPOST) via the library embedded in [LuaTeX](http://luatex.org/) and importing the JSON file using the [Lua scripting language](http://www.lua.org/).

The first and last options will be explored in the course of this text.

This online ebook is available under a Creative Commons license: Attribution-NonCommercial-ShareAlike 3.0 Unported \(CC BY-NC-SA 3.0\) [https://creativecommons.org/licenses/by-nc-sa/3.0/](https://creativecommons.org/licenses/by-nc-sa/3.0/)

The Kickstarter edition will be available under a license which will allow commercial usage to a reasonable degree.

Please contact [willadams@aol.com](mailto:willadams@aol.com) if you wish to arrange for any other sort of arrangement.

