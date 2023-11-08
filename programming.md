---
description: The underlying mechanism behind the designs
---

# Programming

A number of different programming tools and methodologies have been shown throughout this work. Tools which are notable and/or which are used include:

* OpenSCAD --- [https://openscad.org/ ](https://openscad.org/)--- developed from Art of Illusion, this is described as "The Programmers Solid 3D CAD Modeller" and is a de facto standard, so that many other tools extend it.
* BlockSCAD --- [https://www.blockscad3d.com/ ](https://www.blockscad3d.com/) --- a Blockly implementation of OpenSCAD, BlockSCAD affords a quick, easy, and interactive way to model in 3D.
* OpenSCAD Graph Editor (OSGE) --- [https://github.com/derkork/openscad-graph-editor](https://github.com/derkork/openscad-graph-editor) --- a visual programming system, OSGE allows full access to all of OpenSCAD (in marked contrast to the limited number of commands and options afforded by BlockSCAD), including support for the Customizer.
* METAPOST --- [https://www.tug.org/metapost.html](https://www.tug.org/metapost.html) --- a PostScript-oriented re-implementation of the venerable METAFONT [https://www-cs-faculty.stanford.edu/\~knuth/abcde.html#mfbk](https://www-cs-faculty.stanford.edu/\~knuth/abcde.html#mfbk) MP allows one to create 2D drawings as SVGs which may then be imported into Carbide Create to make projects.
* lualatex --- [http://luatex.org/](http://luatex.org/) --- a latter-day implementation of the venerable TeX typesetting system, this allows Lua-scripting, and includes an embedded METAPOST interpreter.
* RapCAD --- [https://rapcad.org/](https://rapcad.org/) --- an alternative to OpenSCAD, RapCAD notably adds the option of writing out text files with full user control.
* gcodepreview --- [https://github.com/WillAdams/gcodepreview](https://github.com/WillAdams/gcodepreview) --- a library for OpenSCAD/RapCAD which allows 3D modeling tool movement/cutting and the generation of a matching G-code file.
* GSharp --- [https://github.com/NRSoft/GSharp](https://github.com/NRSoft/GSharp) --- a system which allows programming in G-code using loops and variables even on G-code implementations which lack such features.
* FullControl GCODE --- [https://fullcontrolgcode.com/software](https://fullcontrolgcode.com/software) --- this was originally an Excel spreadsheet, but it was re-implemented in Python and is available as a website: [https://fullcontrol.xyz/](https://fullcontrol.xyz/) as well as a Python module: [https://github.com/FullControlXYZ/fullcontrol](https://github.com/FullControlXYZ/fullcontrol)
* [http://www.guenther-sohler.net/openscad/](http://www.guenther-sohler.net/openscad/) --- a recent development, this implements Python within OpenSCAD, allowing one to either use a Python (.py) file, or OpenSCAD which uses or references Python files

New ones are regularly developed, and future developments will be documented here as circumstances warrant.&#x20;

Naturally, any programming language which is able to write out files can be used to make G-code, and many programming languages have 3D libraries which will allow modeling in 3D --- this page will focus on those tools which are specifically applicable to CNC usage.

Programming allows dividing a project into two different aspects:

* parameters which define dimensions and features
* algorithms which instantiate the various designs and relationships

Creating a project programmatically allows one to have multiple views of the project --- finished project, any optional states required by features such as lids, and arranging the parts so as to visualize their relationship, and so as to actually cut them out, and to move parts around so as to check fit of joinery and so forth.

Most systems for 3D modeling have one directly model the part itself, then depend on 3D CAM software to create toolpaths to cut things out. A more direct approach is to instead model toolpaths, which has the advantages of ensuring that a part can be cut, that the cutting toolpath is as efficient as it possibly can be, and eliminating the need for a separate CAM program.

Many of the tools discussed here are visual programming languages (VPLs). While this makes things more approachable to some folks, and arguably more expressive, like most things in life, there are tradeoffs. VPLs are not popular, or widely used, and this nicheness can make usage even more awkward. Further considerations are that they attempt to solve a question which does not at this time have an agreed-upon answer:

What does an algorithm look like?

A further concern is scalability --- while many VPLs allow the definition of functions and modules, the usage of them usually goes against the visual nature which is the _raison d'être_ of choosing a VPL, resulting in the exact textual representation which one was trying to escape from, but trapping the words in little boxes or frames. Arguably not using such componentry is even worse as evinced by pages such as:

{% embed url="https://blueprintsfromhell.tumblr.com/" %}

and

{% embed url="https://scriptsofanotherdimension.tumblr.com/" %}

Traditional visual documentation practices may be applicable:

[https://terrastruct.com/blog/post/draw-software-architecture-diagrams/](https://terrastruct.com/blog/post/draw-software-architecture-diagrams/)

## G-code

The language used for toolpaths is G-code (RS-274) [https://www.nist.gov/manuscript-publication-search.cfm?pub\_id=823374](https://www.nist.gov/manuscript-publication-search.cfm?pub\_id=823374) --- in some implementations it is a full-fledged programming language, so it is possible to use it directly to program if one has a suitable 3D previewing tool. Unfortunately, most hobby-level G-code implementations lack variables, branching, and looping, so are only suited to the G-code which is output by CAM programs.

There is a 3rd party tool which will accept G-code with such commands and instantiate them:\
\
[https://github.com/NRSoft/GSharp](https://github.com/NRSoft/GSharp)\
\
which is incorporated into bCNC which is also on Github:&#x20;

[https://github.com/vlachoudis/bCNC](https://github.com/vlachoudis/bCNC)

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

<figure><img src=".gitbook/assets/image (198).png" alt=""><figcaption></figcaption></figure>

As verified by a 3rd party G-code simulator, CutViewer Mill:

<figure><img src=".gitbook/assets/image (201).png" alt=""><figcaption></figcaption></figure>

The control software for many CNC machines will afford G-code entry in one or more ways. For the Carbide 3D machines which I use (and support), this is Carbide Motion, which has two options: MDI --- one can enter G-code into the MDI one line at a time, and also "Quick Actions" which allow entering small programs which can then be run at will.&#x20;

For a list of the G-codes supported by Carbide Motion and Grbl see:\
\
[https://docs.carbide3d.com/software-faq/list-of-supported-gcodes/](https://docs.carbide3d.com/software-faq/list-of-supported-gcodes/)\
and\
[https://my.carbide3d.com/faq/grbl-g-code-definitions/](https://my.carbide3d.com/faq/grbl-g-code-definitions/)

## OpenSCAD

Billed as "The Programmer's Solid 3D CAD Modeller", OpenSCAD affords a programming environment which has variable and loops and 3D modeling and which allows one to export designs as DXF, SVG, and STL files, and affords a variety of tools for creating 3D, and to a lesser extent, 2D designs.

There are a few things to note. Writing out one of the afore-mentioned filetypes requires using a separate CAM tool. OpenSCAD has little to no support for writing out text files. There are certain parameters for setting the size of the elements used to create curved elements which will greatly influence the appearance of the 3D preview, and the verisimilitude of the 3D model.

The OpenSCAD parameters for controlling appearance are:

* $fn --- a global parameter, if applied can make it difficult to ensure that large circles have sufficient segments to render well, while conversely, can cause small circles to be drawn with so many that performance unnecessarily suffers and the appearance is not substantively improved
* $fa --- this sets the smallest number of degrees which will be used to draw a circle using lines, so if set to 4 would result in a circle being approximated using 90 line segments each connected to the next at 4 degrees.
* $fs --- this sets the smallest length which is allowed to be used to draw a circle

Since $fs controls small circles ensuring that the sides are not so small that a point of diminishing returns is reached, and $fa controls large circles, ensuring that the sides are not so smooth that performance suffers, there is no reason to set $fn in normal usage, and many arguments for not doing so. One useful approachis to make the values conditional:

```
$fn = $preview ? 64 : 128;
```

## Linewinder

Once upon a time, there was a drawing tool made by Mattel which had a grid system where a pen was positioned by two cranks along an XY coordinate system, allowing one to draw by rotating the cranks to position the pen and lowering or lifting it as indicated by notations on an instruction strip.

This might work well as an interface concept for a drawing program, but one where:

* there are formulae
* variables may be declared
* each node has associated with it a pair of values each of which is a number, variable, or formula, and when the node is selected, it is possible to edit the underlying formula or variable definition or value
* loops would be shown graphically in the drawing area, surrounding all nodes which a given loop creates with a surrounding border

## gcodepreview

While OpenSCAD allows 3D modeling, it unfortunately does not allow writing out files other than DXFs and SVGs and STLs, but there is fortunately, a similar tool which implements much of the OpenSCAD language, the RapCAD implementation which is able to write out files, allowing one to export toolpaths to G-code, making it well-suited to creating a library which allows modeling in 3D as if one was cutting with a machine.&#x20;

Every module must do what it does twice over, modeling in 3D in OpenSCAD, and if enabled, writing out matching G-code. Further, in some instances, it will be desirable or even necessary to directly write out G-code which has no OpenSCAD equivalent.&#x20;

### setupstock

The first thing which must be done is to define the stock, then it is possible to model the shapes of tools in such a way that they may be hulled together along toolpaths and then subtracted from the stock. Since G-code is inherently subtractive, the stock is simply a comment which defines it. The necessary parameters are:

* stocklength
* stockwidth
* stockthickness
* zeroheight --- either Top or Bottom
* stockorigin --- Lower-Left, Center-Left, Top-Left, or Center

The latter two match job setup options in Carbide Create and determine where the stock will be placed relative to the origin.

<figure><img src=".gitbook/assets/image (231).png" alt=""><figcaption></figcaption></figure>

which generates matching G-code:

<figure><img src=".gitbook/assets/image (222).png" alt=""><figcaption></figcaption></figure>

### generategcode

As noted above, it is necessary to be able to toggle G-code generation on/off, both for performance considerations, and because the command used for this, writeln, is not supported by OpenSCAD, but is specific to RapCAD.

Naturally, it is included as a true/false (boolean) option in the customizer:

```clike
generategcode = false; 
```

and of course the module tests for that variable being set to true when writing out G-code is necessary.

When one is generating G-code some additional commands will be needed.

### toolchange

This command will output an M6 tool change command and the tool number used as an argument.

### startspindle

Starts the spindle at the specified RPM.

### retract

Issues a rapid movement to the specified Z-height (usually safety/retract height)

### closecut

Outputs the commands to end a cut (retract to safety/retract height and M02).

### beziercurves

For the underlying mathematics see: [https://jamie-wong.com/post/bezier-curves/](https://jamie-wong.com/post/bezier-curves/) [https://pomax.github.io/bezierinfo/](https://pomax.github.io/bezierinfo/) and [https://blog.richardekwonye.com/bezier-curves](https://blog.richardekwonye.com/bezier-curves) and [https://ciechanow.ski/drawing-bezier-curves/](https://ciechanow.ski/drawing-bezier-curves/) [https://ciechanow.ski/curves-and-surfaces/](https://ciechanow.ski/curves-and-surfaces/)&#x20;

### Python version

The integration of Python into OpenSCAD [http://www.guenther-sohler.net/openscad/](http://www.guenther-sohler.net/openscad/) allows directly writing out a file rather than using RapCAD

```python
f = open("gcode.nc", "w")

f.write('{} {} {} {}\n'.format(a, x, y, z))

my_lst = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
my_lst_str = ''.join(map(str, my_lst))
```

which must be set up in multiple modules and used sequentially.

There are two ways to incorporate files into OpenSCAD:

* use — this will allow definitions in either Python, or in OpenSCAD and using a mix of OpenSCAD and Python code
* include — this allows using variables from the main OpenSCAD file, but does not allow directly making use a function defined in Python

Since we want to be able to turn on/off calling Python from w/in OpenSCAD we require a total of 3 files:

* a Python file which is loaded using use \<gcodepreview.py>; — this is able to define Python functions
* an OpenSCAD file which is loaded using use \<pygcodepreview.scad>; — this wraps the defined Python function in OpenSCAD
* an OpenSCAD file which is loaded using include \<gcodepreview.scad>; — this allows using OpenSCAD variables from the main file to determine whether or no an OpenSCAD module which calls a Python module should be called

Thus we have a Python file which is loaded using use:

{% code title="gcodepreview.py" %}
```python
def popengcodefile(fn):
    global f
    f = open(fn, "w")

def writeln(*arguments):
    line_to_write = ""
    for element in arguments:
        line_to_write += element
    f.write(line_to_write)
    f.write("\n")

def pclosegcodefile():
    f.close()
```
{% endcode %}

An OpenSCAD file which is loaded using use and which references the Python file:

{% code title="pygcodepreview.scad" %}
```clike
//!OpenSCAD

module oopengcodefile(fn) {
    popengcodefile(fn);
}

module owritecomment(comment) {
    writeln("(",comment,")");
}

module oclosegcodefile() {
    pclosegcodefile();
} 
```
{% endcode %}

And a second OpenSCAD file which references the module definitions from the previous OpenSCAD file:

{% code title="gcodepreview.scad" %}
```clike
//!OpenSCAD

module opengcodefile(fn) {
if (generategcode == true) {
    oopengcodefile(fn);
    }
}

module writecomment(comment) {
if (generategcode == true) {
    owritecomment(comment);
    }
}

module closegcodefile() {
    if (generategcode == true) {
    oclosegcodefile();
    }
}
```
{% endcode %}

which is all put together by an OpenSCAD file:

```clike
//!OpenSCAD

use <gcodepreview.py>;
use <pygcodepreview.scad>;
include <gcodepreview.scad>;

/* [G-code] */
Gcode_filename = "gcode.nc"; 
/* [G-code] */
generategcode = true;

a = 300;

opengcodefile(Gcode_filename);

writecomment(str(a));

writecomment("Test");

closegcodefile();
```

which when run, creates the file:

{% code title="gcode.nc" %}
```
(300)
(Test)
```
{% endcode %}

This concept may then be expanded upon to create a complete system for modeling files as if cutting, and writing out the matching G-code.

### Usage

Putting the commands together has several expectations and requirements. The simplest usage is one where a single cut is made and the tool is plunged at the beginning, the cut is made, and then the tool is lifted to the retract height --- more complex cuts have the same requirements, to ensure that the tool is moved so that it cuts and does not collide with the stock at a rapid rate.

Having multiple cuts presents the possibility of redundant G-code commands, but the simplistic and persistent nature of G-code, that a single command is a movement to the specified position from the current one, and that OpenSCAD requires describing both positions means that every other OpenSCAD command after the first can omit writing out the G-code, which will then omit the redundant commands and result in terse code which still describes the expected machine motion.

Available at: [https://github.com/WillAdams/gcodepreview](https://github.com/WillAdams/gcodepreview)

## OpenSCAD Graph Editor

If one loads the library gcodepreview as a module into OSGE, it is pretty straight-forward to use it to create a file to cut out a design using G-code:

<figure><img src=".gitbook/assets/image (75).png" alt=""><figcaption></figcaption></figure>

which when generated as OpenSCAD code previews as expected:

<figure><img src=".gitbook/assets/image (171).png" alt=""><figcaption></figcaption></figure>

which with a bit of editing works as expected in RapCAD:

<figure><img src=".gitbook/assets/image (188).png" alt=""><figcaption></figcaption></figure>

and generates G-code which previews as expected:

<figure><img src=".gitbook/assets/image (166).png" alt=""><figcaption></figcaption></figure>

Available at: [https://github.com/WillAdams/gcodepreview/blob/main/flatten.graph.tres](https://github.com/WillAdams/gcodepreview/blob/main/flatten.graph.tres)

## Programming Modules

Rather than create each project completely from scratch, one will often develop libraries of modules which effectively customize the language/system so as to make it more expressive and consistent. The gcodepreview library noted above when loaded into OpenSCAD Graph Editor allows one to create projects which are able to make use of arbitrary G-code, and by extension to create a module which does so.

### cutjoinery

A potentially useful example would be one for creating joinery. The first consideration is which values would need to be passed into the module:

* orientation --- whether the joint is horizontal or vertical
* side --- which side of the joint is cut, since a different number of fingers will be used on each side the possibilities could be labeled as: even, odd, or both
* number of pins --- the code is simpler if it is required that the user specify this, rather than attempting to calculate it, and it is a useful control for the user
* bx, by, bz --- the origin point of the joint
* ex, ey, ez --- the ending point
* clear center --- whether or not the center channel is cleared, since when both are cut together it would be redundant to have it cut by both the even and odd sub-modules
* tool radius --- used to calculate the geometry of the joint
* square tool no, V tool no, large V tool no --- the specific tools used define the geometry of the joint as cut/modeled

The initial structure requires 4 sub-modules, one for each possible combination of orientation and side:

<figure><img src=".gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

The actual work of modeling/cutting is then done in these sub-modules. Working this up wants a graphical representation/preview --- for that, we turn to Carbide Create to draw things up in profile and in 2D so as to assign 3D toolpaths, first matching the stock setup as assigned in OpenSCAD Graph Editor/OpenSCAD:

<figure><img src=".gitbook/assets/image (181).png" alt=""><figcaption></figcaption></figure>

In Carbide Create:

![](<.gitbook/assets/image (192).png>)

so that we can draw up things in Carbide Create as we work through the programming. First consideration is what the call is to the module:

<figure><img src=".gitbook/assets/image (221).png" alt=""><figcaption></figcaption></figure>

<figure><img src=".gitbook/assets/image (126).png" alt=""><figcaption></figcaption></figure>

which we will match in Carbide Create, keeping the twain in synch so as to keep track of our progress and how things fit together:

<figure><img src=".gitbook/assets/image (223).png" alt=""><figcaption></figcaption></figure>

### DXF

[https://stackoverflow.com/questions/54937433/how-do-i-write-a-dxf-code-for-a-polyline](https://stackoverflow.com/questions/54937433/how-do-i-write-a-dxf-code-for-a-polyline)

## Other tools to consider

* [https://github.com/chigraph/chigraph](https://github.com/chigraph/chigraph)
* [https://github.com/studiotc/NodeGraphInterface](https://github.com/studiotc/NodeGraphInterface)
* SnapSCAD --- [https://github.com/martymcguire/snapscad](https://github.com/martymcguire/snapscad)
* [https://chigraph.io/](https://chigraph.io/)
* [http://nodezator.com/](http://nodezator.com/)
* [https://ryven.org/](https://ryven.org/) and [https://github.com/Tanneguydv/Pythonocc-nodes-for-Ryven](https://github.com/Tanneguydv/Pythonocc-nodes-for-Ryven)
* [https://github.com/Bycelium/PyFlow](https://github.com/Bycelium/PyFlow)
* [https://nodeeditor.seneral.dev/index.html](https://nodeeditor.seneral.dev/index.html)
* [https://nodes.io/](https://nodes.io/)
* [https://github.com/Nodi3d/nodi](https://github.com/Nodi3d/nodi)
* [https://makecode.buildbee.com/](https://makecode.buildbee.com/)
* [https://bitbybit.dev/](https://bitbybit.dev/)
* [https://github.com/nortikin/sverchok](https://github.com/nortikin/sverchok)
* [https://github.com/kovacsv/VisualScriptCAD](https://github.com/kovacsv/VisualScriptCAD)
* [https://macad3d.net/](https://macad3d.net/)
* [https://nodi3d.com/](https://nodi3d.com/)
* [https://brlcad.org/](https://brlcad.org/)
* [https://beegraphy.com](https://beegraphy.com)
* [https://github.com/sgenoud/replicad](https://github.com/sgenoud/replicad)
* [https://www.nodebox.net/](https://www.nodebox.net/)
* [https://github.com/zalo/CascadeStudio](https://github.com/zalo/CascadeStudio)
* [https://book.gtoolkit.com/index.html](https://book.gtoolkit.com/index.html)

