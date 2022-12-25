---
description: The underlying mechanism behind the designs
---

# Programming

A number of different programming tools and methodologies have been shown throughout this work. Tools which are notable and which are used include:

* OpenSCAD --- [https://openscad.org/ ](https://openscad.org/)--- developed from Art of Illusion, this is described as "The Programmers Solid 3D CAD Modeller" and is a de facto standard, so that many other tools extend it.
* BlockSCAD --- [https://www.blockscad3d.com/ ](https://www.blockscad3d.com/) --- a Blockly implementation of OpenSCAD, BlockSCAD affords a quick, easy, and interactive way to model in 3D.
* OpenSCAD Graph Editor (OSGE) --- [https://github.com/derkork/openscad-graph-editor](https://github.com/derkork/openscad-graph-editor) --- a visual programming system, OSGE allows full access to all of OpenSCAD (in marked contrast to the limited number of commands and options afforded by BlockSCAD), including support for the Customizer.
* METAPOST --- [https://www.tug.org/metapost.html](https://www.tug.org/metapost.html) --- a PostScript-oriented re-implementation of the venerable METAFONT [https://www-cs-faculty.stanford.edu/\~knuth/abcde.html#mfbk](https://www-cs-faculty.stanford.edu/\~knuth/abcde.html#mfbk) MP allows one to create 2D drawings as SVGs which may then be imported into Carbide Create to make projects.
* lualatex --- [http://luatex.org/](http://luatex.org/) --- a latterday implementation of the venerable TeX typesetting system, this allows Lua-scripting, and includes an embedded METAPOST interpreter.
* RapCAD --- [https://rapcad.org/](https://rapcad.org/) --- an alternative to OpenSCAD, RapCAD adds the option of writing out text files with full user control.
* gcodepreview --- [https://github.com/WillAdams/gcodepreview](https://github.com/WillAdams/gcodepreview) --- a library for OpenSCAD/RapCAD which allows 3D modeling tool movement/cutting and the generation of a matching G-code file.

New ones are regularly developed, and future developments will be documented here as circumstances dictate.&#x20;

Programming allows dividing a project into two different aspects:

* parameters which define dimensions and features
* algorithms which instantiate the various designs and relationships

Creating a project programmatically allows one to have multiple views of the project --- finished project, any optional states required by features such as lids, and arranging the parts so as to visualize their relationship, and so as to actually cut them out, and to move parts around so as to check fit of joinery and so forth.

Most systems for 3D modeling have one directly model the part itself, then depend on 3D CAM software to create toolpaths to cut things out. A more direct approach is to instead model toolpaths, which has the advantages of ensuring that a part can be cut, that the cutting toolpath is as efficient as it possibly can be, and eliminating the need for a separate CAM program.

## G-code

The language used for toolpaths is G-code (RS-274) [https://www.nist.gov/manuscript-publication-search.cfm?pub\_id=823374](https://www.nist.gov/manuscript-publication-search.cfm?pub\_id=823374) --- in some implementations it is a full-fledged programming language, so it is possible to use it directly to program if one has a suitable 3D previewing tool. Unfortunately, most hobby-level G-code implementations lack variables, branching, and looping, so are only suited to the G-code which is output by CAM programs.

A straight-forward program which cuts an "X" in a 100mm square using two different tools from origin at the Lower-Left, and Top of the stock with a Retract Height of 5mm:

```clike
(Design File: gcode_sample_102_390.c2d)
(stockMin:0.00mm, 0.00mm, -1.00mm)
(stockMax:100.00mm, 100.00mm, 0.00mm)
(STOCK/BLOCK,100.00, 100.00, 1.00,0.00, 0.00, 1.00)
G90
G21
(Move to safe Z to avoid workholding)
G53G0Z-5.000
(Toolpath..Contour.Toolpath.1)
M05
(TOOL/MILL,3.17, 0.00, 0.00, 0.00)
M6T102
M03S18000
(PREPOSITION FOR RAPID PLUNGE)
G0X0.000Y0.000
G1Z-0.762F381.0
X100.000Y100.000F1143.0
Z5.000
(Toolpath..Contour.Toolpath.2)
M05
(Move to safe Z to avoid workholding)
G53G0Z-5.000
(TOOL/MILL,0.03, 0.00, 10.00, 45.00)
M6T390
M03S10000
(PREPOSITION FOR RAPID PLUNGE)
G0X0.000Y100.000
G1Z-1.000F203.2
X100.000Y0.000F254.0
Z5.000
M02
```

This previews as:

<figure><img src=".gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

As verified by a 3rd party G-code simulator, CutViewer Mill:

<figure><img src=".gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

## gcodepreview

OpenSCAD affords a programming environment which has variable and loops and 3D modeling, and in the RapCAD implementation is able to write out files, allowing one to export toolpaths to G-code. The first thing which must be done is to define the stock, then it is possible to model the shapes of tools in such a way that they may be hulled together along toolpaths and then subtracted from the stock.

### setupstock

Every module must do what it does twice over, modeling in 3D in OpenSCAD, and if enabled, writing out matching G-code. Further, in some instances, it will be desirable or even necessary to directly write out G-code which has no OpenSCAD equivalent. Since G-code is inherently subtractive, the stock is simply a comment which defines it. The necessary parameters are:

* stocklength
* stockwidth
* stockthickness
* zeroheight --- either Top or Bottom
* stockorigin --- Lower-Left, Center-Left, Top-Left, or Center

The latter two match job setup options in Carbide Create and determine where the stock will be placed relative to the origin.

<figure><img src=".gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

which generates matching G-code:

<figure><img src=".gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

### generategcode

As noted above, it is necessary to be able to toggle G-code generation on/off, both for performance considerations, and because the command used for this, writeln, is not supported by OpenSCAD, but is specific to RapCAD.

Naturally, it is included as a true/false (boolean) option in the customizer:

```clike
generategcode = false; 
```

and of course the module tests for that variable being set to true when writing out G-code is necessary.

&#x20;

