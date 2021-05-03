---
description: >-
  Simple butt joints save material but can be made to work with modern adhesives
  and hardware.
---

# Butt Joints and Measuring

Most joinery techniques require that each part be extended into the other and the stock which forms the joints be removed so that the two parts fit together. For simple and rough or rustic projects, it may be appropriate to simply cut the parts to size and mate them using adhesives and hardware. A classic example of this approach is a bird house for wrens:

![Wren birdhouse](.gitbook/assets/birdhouse_-wren%20%281%29.jpg)

Like all other projects, it begins with a set of parameters:

![Wren birdhouse: parameters](.gitbook/assets/image%20%2869%29.png)

Usually designed around the dimensions of the stock used:

![Wren birdhouse: calculated dimensions](.gitbook/assets/image%20%2868%29.png)

This requirement suggests a technique which will address the inability to parse an object w/in OpenSCAD to determine its dimensions:

![Wren birdhouse: module for calculating dimensions](.gitbook/assets/image%20%2871%29.png)

Create a module, the output of which may be plugged in wherever a given set of dimensions is used.

The BlockSCAD link for the wren birdhouse is:

{% embed url="https://www.blockscad3d.com/community/projects/1168572" %}

It includes a matrix for laying out the parts for cutting:

![Wren birdhouse: parts for cutting](.gitbook/assets/image%20%2870%29.png)

The parts layout may be easily prepared for exporting as a DXF or SVG using the projection\(\) command as previously shown.







