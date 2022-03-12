---
description: Miter joints with hidden joinery cut flat on the machine
---

# Blind Miter Box Joints

The ideal joint would be void free and not show any endgrain, while being self-aligning and offering sufficient long-grain glue surface for strength — the classic example of this is the blind miter dovetail which is pretty much the exclusive domain of hand tool woodworking.

A similar design would be the blind miter box (or finger) joint which has seen a number of implementations:

* [https://joinerynotebook.blogspot.com/2016/03/blind-mitered-finger-joint-boxes.html](https://joinerynotebook.blogspot.com/2016/03/blind-mitered-finger-joint-boxes.html)
* [https://www.finewoodworking.com/2012/05/05/cutting-and-fitting-a-blind-finger-joint](https://www.finewoodworking.com/2012/05/05/cutting-and-fitting-a-blind-finger-joint)
* [https://community.carbide3d.com/t/full-blind-finger-joints/947](https://community.carbide3d.com/t/full-blind-finger-joints/947)
* [https://community.carbide3d.com/t/overengineered-box-for-the-endmills-i-dont-have-yet/429](https://community.carbide3d.com/t/overengineered-box-for-the-endmills-i-dont-have-yet/429)

As the latter two links make clear, there are two possible approaches:&#x20;

* Use the radius of the endmill to define the fingers so as to minimize voids, and end-grain–end-grain connections
* Overcut with dogbones which makes the layout simpler, and has the benefit of increasing long-grain--long-grain glue surface

The former can become quite complex and requires over-cutting where the fingers and miter angle intersect which creates voids, while the latter has voids designed in, but which has the noted advantages of increasing long-grain glue surface, and greatly simplifying the geometry, reducing the number of tools needed. With a rabbeted lid and bottom, it is still possible to have a fully mitered appearance, preserving the visible diagonal if one simply shortens where the box joints are cut, and adds in the successive V endmill cutting necessary to cut visible miter. Note that this may create a fragile cross-grain element which will require care in cutting, and post-processing.

The joint in question is simple enough that it raises the idea: Why not keep track of the iterations of tools and depth of cuts and pass those into the tool files so as to allow automation of making multiple layouts in a DXF or SVG, each of which is for a different tool/depth combination.

This is discussed at: [https://community.carbide3d.com/t/a-different-sort-of-box/36882](https://community.carbide3d.com/t/a-different-sort-of-box/36882)

This allows one to cut out a box in as few operations as stock size and working area permit.

* bottom (cut to size, possibly rabbet)
* top (cut to size, possibly rabbet, possibly add features, e.g., a thumb indent for a sliding lid)
* front and/or back and one or both sides (repeat once for 2 operations if need be) — this will cut the joinery blind box joints and miter as well as rabbets for lid, bottom, and if applicable, a relief cut to ease sawing the lid off, or a cut out of the front to allow for a sliding lid

using only two, or possibly three tools:

* a square endmill
* a narrow V endmill
* (optional) a smaller endmill which allows cutting dogbones for the box joints which are so small as to hopefully escape notice

Drawing things in profile with the V endmill makes the starting point of the joint geometry quite obvious:

![](<.gitbook/assets/image (113) (1) (1).png>)

![](<.gitbook/assets/image (123).png>)

which is easily modeled in 3D:

![](<.gitbook/assets/image (114) (1) (1) (1).png>)

![](<.gitbook/assets/image (119).png>)

Adding an option for laying out things so as to generate a DXF results in:

![](<.gitbook/assets/image (115) (1).png>)

which may be easily exported to OpenSCAD where the projection() command can be added so that it may be exported as a DXF and imported into Carbide Create:

![](<.gitbook/assets/image (121) (1).png>)

Once it is imported, the elements must be dragged into alignment, then it is simply a matter of working up the depth which is being cut to, and drawing or modeling the fingers --- draw in appropriate geometry to model them, and add a square in the profile drawing to show to what depth things should be cut:

![](<.gitbook/assets/image (115) (1) (1) (1).png>)

&#x20;Then assign a pocket toolpath to that depth:

![](<.gitbook/assets/image (117) (1) (1).png>)

then select the rounded rectangles for the V cut and start it at the bottom of the pocket:

![](<.gitbook/assets/image (118) (1).png>)

and assign a V carving toolpath --- alternately, it is possible to instead create a line which describes the desired V cut and assign a no-offset Contour Toolpath which has the advantage of not having any extraneous plunging at the ends.

Once toolpaths are assigned, the design may be previewed:

![](<.gitbook/assets/image (116) (1) (1) (1) (1).png>)

