---
description: The underlying mechanism behind the designs
---

# Programming

A number of different programming tools and methodologies have been shown throughout this work. New ones are regularly developed, and this new development will continue in the future. Tools which are notable and which are used include:

* OpenSCAD --- [https://openscad.org/ ](https://openscad.org/)--- developed from Art of Illusion, this is described as "The Programmers Solid 3D CAD Modeller" and is a de facto standard, so that many other tools extend it.
* BlockSCAD --- [https://www.blockscad3d.com/ ](https://www.blockscad3d.com/) --- a Blockly implementation of OpenSCAD, BlockSCAD affords a quick, easy, and interactive way to model in 3D.
* OpenSCAD Graph Editor (OSGE) --- [https://github.com/derkork/openscad-graph-editor](https://github.com/derkork/openscad-graph-editor) --- a visual programming system, OSGE allows full access to all of OpenSCAD (in marked contrast to the limited number of commands and options afforded by BlockSCAD), including support for the Customizer.
* METAPOST --- [https://www.tug.org/metapost.html](https://www.tug.org/metapost.html) --- a PostScript-oriented re-implementation of the venerable METAFONT [https://www-cs-faculty.stanford.edu/\~knuth/abcde.html#mfbk](https://www-cs-faculty.stanford.edu/\~knuth/abcde.html#mfbk) MP allows one to create 2D drawings as SVGs which may then be imported into Carbide Create to make projects.
* lualatex --- [http://luatex.org/](http://luatex.org/) --- a latterday implementation of the venerable TeX typesetting system, this allows Lua-scripting, and includes an embedded METAPOST interpreter.
* RapCAD --- [https://rapcad.org/](https://rapcad.org/) --- an alternative to OpenSCAD, RapCAD adds the option of writing out text files with full user control.
* gcodepreview --- [https://github.com/WillAdams/gcodepreview](https://github.com/WillAdams/gcodepreview) --- a library for OpenSCAD/RapCAD which allows 3D modeling tool movement/cutting and the generation of a matching G-code file.

Creating a project programmatically requires multiple views of the project --- finished project, any optional states required by features such as lids, and arranging the parts so as to visualize their relationship, and so as to actually cut them out.

\
