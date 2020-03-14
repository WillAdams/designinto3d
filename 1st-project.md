---
description: 'Creating a first project using BlockSCAD, OpenSCAD, and Carbide Create'
---

# 1st Project

The first project is a rectangular block with the proportions of the monolith from Arthur C. Clarke's science fiction classic, _2001: A Space Odyssey_, 1:4:9, where the second and third value are the second and third natural squares \(the book goes on to imply that the progression continues in other dimensions, but that is beyond the scope of this project\).

A quick and easy way to model in 3D is to use the Blockly variant of OpenSCAD, BlockSCAD: [https://www.blockscad3d.com/editor/](https://www.blockscad3d.com/editor/)

In it, one simply drags blocks and arranges them and updates variable values until one arrives at a desired design. While one could simply use a cube object and manually enter the values:

`cube(size = [4,1,9], center = false);`

The best practice would be to use a module and have the calculations done automatically based on the user inputting the thickness desired:

![Design into 3D: 1st Project: BlockSCAD](.gitbook/assets/blockscad.PNG)

With the part designed, the next consideration is manufacture. The easiest way to get a project from BlockSCAD \(or OpenSCAD\) into a CAM tool such as Carbide Create is to export a DXF. If this were done along the standard 2D view, one would get a rectangle as wide as the cube, but only as deep as the thickness, where instead what is wanted is the height, so the block needs to be rotated.

In order to do this, one would create a checkbox \(or Boolean\) in 

