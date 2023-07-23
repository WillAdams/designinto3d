---
description: >-
  Simple butt joints save material but can be made to work with modern adhesives
  and hardware.
---

# Butt Joints and Measuring

Most joinery techniques require that each part be extended into the other and the stock which forms the joints be removed so that the two parts fit together. For simple and rough or rustic projects, it may be appropriate to simply cut the parts to size and mate them using adhesives and hardware. A classic example of this approach is a bird house for wrens:

![Wren birdhouse](<.gitbook/assets/birdhouse\_-wren (1).jpg>)

Like all other projects, it begins with a set of parameters:

![Wren birdhouse: parameters](<.gitbook/assets/image (69) (1).png>)

Usually designed around the dimensions of the stock used:

![Wren birdhouse: calculated dimensions](<.gitbook/assets/image (68).png>)

This requirement suggests a technique which will address the inability to parse an object w/in OpenSCAD to determine its dimensions:

![Wren birdhouse: module for calculating dimensions](<.gitbook/assets/image (71).png>)

Create a module, the output of which may be plugged in wherever a given set of dimensions is used.

An optional improvement here is to allow inputting the desired axis (two is easiest, but more may be done) as shown in:

[https://www.blockscad3d.com/community/projects/1205684](https://www.blockscad3d.com/community/projects/1205684)

The BlockSCAD link for the wren birdhouse is:

{% embed url="https://www.blockscad3d.com/community/projects/1168572" %}

It includes a matrix for laying out the parts for cutting:

![Wren birdhouse: parts for cutting](<.gitbook/assets/image (70).png>)

The parts layout may be easily prepared for exporting as a DXF or SVG using the projection() command as previously shown.

It is frequently necessary to refer to the dimensions of parts while working. While these could be stored as variables, it may be more expressive to calculate them using a module which can then return either width or depth based on a parameter:

![Dimension calculation using a module](<.gitbook/assets/image (72).png>)

Then it is simply a matter of cutting out the parts:

![Birdhouse parts](.gitbook/assets/20210526\_163408.jpg)

and assembling with a few nails and a hinge and associated hardware:

![Wren birdhouse](.gitbook/assets/win\_20210528\_14\_05\_13\_pro.jpg)

Files for this size are available at: [https://community.carbide3d.com/t/a-birdhouse-for-wrens-but-parametric-so-adjustable/32161/11](https://community.carbide3d.com/t/a-birdhouse-for-wrens-but-parametric-so-adjustable/32161/11)
