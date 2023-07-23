---
description: A simple box with fitted lid and optionally divided compartments
---

# Box with Fitted Lid

Arguably, the simplest project of all is one where all features are cut out from a single piece of stock. The earliest wooden boxes were made thus, characterized as a dug out chest, usually with a single compartment. The development of the electric router brought such designs back into vogue.

As with all projects, we begin by defining the parameters of the design and its display:

![Fitted Pencil Box Parameters](<.gitbook/assets/image (77).png>)

Then a module for cutting the desired shapes:

![Fitted Pencil Box module for cutting pockets at specified depth and location](<.gitbook/assets/image (76) (1).png>)

Then modules for cutting each part:

![Fitted Pencil Box top module](<.gitbook/assets/image (80).png>)

![Fitted Pencil Box bottom module setup](<.gitbook/assets/image (87).png>)

![Fitted Pencil Box bottom module loop](<.gitbook/assets/image (88).png>)

Creating a file for cutting is simply a matter of capturing each elevation of features:

![](<.gitbook/assets/image (84).png>)

Available at:

{% embed url="https://www.blockscad3d.com/community/projects/1213467" %}

The project can then be exported to OpenSCAD code and modified to use the customizer:

`Width = 8.25;` \
`Depth = 2.625;` \
`Height = 0.625;` \
`Units = 25.4; // [1:Millimeters, 25.4:Inches]` \
`Number_of_Rows = 2;` \
`Number_of_Columns = 3;` \
`Large_Compartment = "Depth-wise"; // [Width-wise, Depth-wise, None]` \
`Corner_Radius = 0.25;` \
`Lid_Proportion = 40;` \
`Stock_Thickness = 0.5625;` \
`Endmill_Diameter = 0.125;` \
`my_3D_Preview = false;` \
`$fn=80;`

![Fitted Pencil Box in OpenSCAD with customization](<.gitbook/assets/image (83).png>)

Add the command:

`projection()`

to get a flattened view which may be exported to a DXF or SVG and then imported into Carbide Create:

![Fitted Pencil Box in OpenSCAD projection](<.gitbook/assets/image (85).png>)

Once imported into Carbide Create it is simply a matter of assigning toolpaths:

![Fitted Pencil Box in Carbide Create](<.gitbook/assets/image (86) (1).png>)

Files are available at: [https://community.carbide3d.com/t/fitted-box-design-generator-underway/13437/29](https://community.carbide3d.com/t/fitted-box-design-generator-underway/13437/29)

### One or more variations

The problem with the generator, is that even the most minor change requires re-creating the toolpaths.

One thing which is persistent as regards toolpaths, but which is easily changed is text, so if one had a box design which had for its dividers a character from a single font, one could change the number of dividers as simply as re-typing a number, and still have the product ready to run.

First step is to make a font which has dividers for numbers, so:

![Design into 3D font for round box dividers](<.gitbook/assets/designinto3d\_font (2).png>)

This font is available at: [https://community.carbide3d.com/t/fitted-box-design-generator-underway/13437/30](https://community.carbide3d.com/t/fitted-box-design-generator-underway/13437/30)

It works when placed in the Carbide 3D font directory (Help | About | Open Data Directory).

Once installed, load the Carbide Create file, select the center divider, then choose the font tool and replace the number with the number of dividers you want:

![Fitted round box with variable dividers](<.gitbook/assets/image (81).png>)

![Fitted round box with 2 or 7 dividers](.gitbook/assets/win\_20190825\_11\_17\_15\_pro.jpg)
