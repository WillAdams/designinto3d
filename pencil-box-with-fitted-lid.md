---
description: A simple pencil box with lid and optionally divided compartments
---

# Box with Fitted Lid

Arguably, the simplest project of all is one where all features are cut out from a single piece of stock. The earliest wooden boxes were made thus, characterized as a dug out chest, usually with a single compartment. The development of the electric router brought such designs back into vogue.

As with all projects, we begin by defining the parameters of the design and its display:

![Pencil Box Parameters](.gitbook/assets/image%20%2877%29.png)

Then a module for cutting the desired shapes:

![Pencil Box module for cutting pockets at specified depth and location](.gitbook/assets/image%20%2876%29.png)

Then modules for cutting each part:

![Pencil Box top module](.gitbook/assets/image%20%2880%29.png)

![Pencil Box bottom module setup](.gitbook/assets/image%20%2884%29.png)

![Pencil Box bottom module loop](.gitbook/assets/image%20%2885%29.png)

Creating a file for cutting is simply a matter of capturing each elevation of features:

![](.gitbook/assets/image%20%2883%29.png)

Available at:

{% embed url="https://www.blockscad3d.com/community/projects/1213467" %}

The project can then be exported to OpenSCAD code and modified to use the customizer:

`Width = 8.25;   
Depth = 2.625;   
Height = 0.625;   
Units = 25.4; // [1:Millimeters, 25.4:Inches]   
Number_of_Rows = 2;   
Number_of_Columns = 3;   
Large_Compartment = "Depth-wise"; // [Width-wise, Depth-wise, None]   
Corner_Radius = 0.25;   
Lid_Proportion = 40;   
Stock_Thickness = 0.5625;   
Endmill_Diameter = 0.125;   
my_3D_Preview = false;   
$fn=80;`

![Pencil Box in OpenSCAD with customization](.gitbook/assets/image%20%2882%29.png)

Add the command:

`projection()`

to get a flattened view which may be exported to a DXF or SVG and then imported into Carbide Create:

![Pencil Box in OpenSCAD projection](.gitbook/assets/image%20%2881%29.png)





