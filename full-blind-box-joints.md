---
description: Miter joints with hidden joinery cut flat on the machine
---

# Full Blind Box Joints

The ideal joint would be void free and not show any endgrain, while being self-aligning and offering sufficient long-grain glue surface for strength --- the classic example of this is the blind miter dovetail which is pretty much the exclusive domain of hand tool woodworking.

A similar design would be the blind miter box or fingerjoint which has seen a number of implementations:

* [https://joinerynotebook.blogspot.com/2016/03/blind-mitered-finger-joint-boxes.html](https://joinerynotebook.blogspot.com/2016/03/blind-mitered-finger-joint-boxes.html)
* [https://www.finewoodworking.com/2012/05/05/cutting-and-fitting-a-blind-finger-joint](https://www.finewoodworking.com/2012/05/05/cutting-and-fitting-a-blind-finger-joint)
* [https://community.carbide3d.com/t/full-blind-finger-joints/947](https://community.carbide3d.com/t/full-blind-finger-joints/947)
* [https://community.carbide3d.com/t/overengineered-box-for-the-endmills-i-dont-have-yet/429](https://community.carbide3d.com/t/overengineered-box-for-the-endmills-i-dont-have-yet/429)

As the latter two links make clear, there are two possible approaches:&#x20;

* Use the radius of the endmill to define the fingers so as to minimize endgrain--endgrain connections
* Overcut with dogbones which makes the layout simpler

The former can become quite complex and requires over-cutting where the fingers and miter angle intersect which creates voids, while the latter has voids designed in, but which has the advantages of increasing long grain glue surface, and greatly simplifying the geometry, reducing the number of tools needed. With a rabbeted lid and bottom, it is still possible to have a fully mitered appearance, preserving the visible diagonal if one simply shortens where the box joints are cut, and adds in the successive V endmill cutting necessary to cut visible miter.

The joint in question is simple enough that it raises the idea: Why not keep track of the iterations of tools and depth of cuts and pass those into the tool files so as to allow automation of making multiple layouts in a DXF or SVG, each of which is for a different tool/depth combination.

This is discussed at: [https://community.carbide3d.com/t/a-different-sort-of-box/36882](https://community.carbide3d.com/t/a-different-sort-of-box/36882)

This allows one to cut out a box in 2, 3 or 4 operations:

* bottom (cut to size)
* top (cut to size) — possibly combined w/ the bottom
* front/back and one or both sides (repeat once for 2 operations if need be) — this will cut the joinery blind box joints and miter as well as feature for lid, bottom, and a relief cut to ease sawing the lid off

using only two tools:

* a small endmill
* a narrow V endmill

Drawing things in profile with the V endmill makes the starting point of the joint geometry quite obvious:

![](<.gitbook/assets/image (113) (1) (1).png>)

which is easily modeled in 3D:

![](<.gitbook/assets/image (114) (1) (1).png>)

Adding an option for laying out things so as to generate a DXF results in:

![](<.gitbook/assets/image (115).png>)

which may be easily exported to OpenSCAD where the projection() command can be added so that it may be exported as a DXF and imported into Carbide Create:

![](<.gitbook/assets/image (121).png>)

Once it is imported, the elements must be dragged into alignment, then it is simply a matter of working up the depth which is being cut to, and drawing or modeling the fingers --- draw in appropriate geometry to model them, and add a square in the profile drawing to show to what depth things should be cut:

![](<.gitbook/assets/image (115) (1) (1).png>)

&#x20;Then assign a pocket toolpath to that depth:

![](<.gitbook/assets/image (117).png>)

then select the rounded rectangles for the V cut and start it at the bottom of the pocket:

![](<.gitbook/assets/image (118).png>)

which then previews as:

![](<.gitbook/assets/image (116) (1) (1) (1).png>)

