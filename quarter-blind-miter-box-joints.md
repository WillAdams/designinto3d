---
description: Miter joints with hidden joinery cut flat on the machine
---

# Quarter Blind Miter Box Joints

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
* a narrow V endmill (must be narrower in diameter than half the stock thickness)
* (optional) a smaller endmill which allows cutting dogbones for the box joints which are so small as to hopefully escape notice

The joint is made up of two sections:&#x20;

* a 45 degree V miter which is easily cut using a 90 degree V endmill with the stock flat on the machine
* a series of interlocking pockets which make up the box joints

Drawing things in profile with the V endmill makes the starting point of the joint geometry quite obvious:

![](<.gitbook/assets/image (286).png>)

and adding squares to stand in for the pockets and islands which make up the joints affords the balance of the joint:

![](<.gitbook/assets/image (208).png>)

Given the side profile of the joint, it is simple to then draw the geometry for the joint as it will be seen from overhead as it will be cut.&#x20;

Draw in lines which will define where the V tooling will cut the miter:

![](<.gitbook/assets/image (97).png>)

A no-offset Contour toolpath may then be assigned:

![](<.gitbook/assets/image (235).png>)

This may then be verified by checking the 3D preview:

![](<.gitbook/assets/image (52).png>)

The joinery must be positioned relative to the bottom and/or lid which will require rabbets. Draw these in and then measure the remaining space:

![](<.gitbook/assets/image (245).png>)

Determine how many joint positions there will be and then do the math to determine how tall each pocket or island will be and draw one in. For most efficient cutting the height should be a bit less than twice the height of the endmill which will be used.

![](<.gitbook/assets/image (71).png>)

add dogbones which are as small as is possible --- if necessary, use a second endmill to cut the dogbones:

![](<.gitbook/assets/image (302).png>)

Then use the Linear Array tool to duplicate as necessary:

![](<.gitbook/assets/image (114).png>)

and adjust the settings to get two alternating columns:

* Number of rows --- this should be half as many as the total, rounded up
* Number of colums --- 2
* X spacing --- width of the part less the width of the stock
* Y spacing --- twice the height of the box joint
* Row offset --- 0
* Column offset --- height of the box joint

![](<.gitbook/assets/image (51).png>)

Repeat for the others:

![](<.gitbook/assets/image (248).png>)

Extend the geometry which is at the top:

![](<.gitbook/assets/image (102).png>)

Then draw in geometry which represents where the V endmills will be cut and duplicate the rabbet(s):

![](<.gitbook/assets/image (42).png>)

And union things&#x20;

![](<.gitbook/assets/image (95).png>)

Duplicate this geometry, drag it into alignment w/ the original, and union it w/ the geometry for the rabbet:

![](<.gitbook/assets/image (255).png>)

Create a toolpath which cuts to the rabbet depth:

![](<.gitbook/assets/image (213).png>)

Then select the geometry which does not include the rabbet and create a toolpath which starts at the bottom of the pocket, then cut the depth which the shoulder of the V endmill cuts:

![](<.gitbook/assets/image (296).png>)

Which previews as:

![](<.gitbook/assets/image (8).png>)

(The V endmill toolpath should be moved to the bottom of the list)

If the endmill used for the main pocketing won't cut the dogbones, add an inside profile using a sufficiently smaller tool to cut them as well:

![](<.gitbook/assets/image (77).png>)

![](<.gitbook/assets/image (47).png>)

This same technique can be done in a 3D model:

![](<.gitbook/assets/image (6).png>)

![](<.gitbook/assets/image (107).png>)

![](<.gitbook/assets/image (82).png>)

Adding an option for laying out things so as to generate a DXF results in:

![](<.gitbook/assets/image (66).png>)

which is available at:

[https://www.blockscad3d.com/community/projects/1356379](https://www.blockscad3d.com/community/projects/1356379)

which may be easily exported to OpenSCAD:

[https://github.com/WillAdams/Design\_Into\_3D/blob/master/blindmiter\_boxjoint/Design%20into%203D\_%20Box%20with%20Lid.scad](https://github.com/WillAdams/Design\_Into\_3D/blob/master/blindmiter\_boxjoint/Design%20into%203D\_%20Box%20with%20Lid.scad)

which is set up for a Customizer:

![](<.gitbook/assets/image (118).png>)

where the projection() command can be added so that it may be exported as a DXF and imported into Carbide Create:

![](<.gitbook/assets/image (212).png>)

which may then be exported as a DXF or SVG and imported into Carbide Create:

![](<.gitbook/assets/image (318).png>)

Once it is imported, the elements must be dragged into alignment, then it is simply a matter of working up the depth which is being cut to, and applying suitable toolpaths.

![](<.gitbook/assets/image (96).png>)

Things will be easier to work with if each type of cut is on a separate layer:

![](<.gitbook/assets/image (300).png>)

Then select all the part outlines and offset them to the outside by a bit more than the radius of the endmill which will be used to cut them out:

&#x20;

![](<.gitbook/assets/image (27).png>)

![](<.gitbook/assets/image (266).png>)

For each V carving channel, draw a polyline the length of the straight portion (it will snap to the nodes):

![](<.gitbook/assets/image (64).png>)

and then align it to the center of the channel:

![](<.gitbook/assets/image (14).png>)

and assign a no offset Contour Toolpath to the Stock Depth:

![](<.gitbook/assets/image (253).png>)

Then make all other layers visible and merge together all the parts so as to make cuts to the rabbet depth, and then the depth of the joinery.&#x20;

Once toolpaths are assigned, the file may be duplicated if need be and things arranged so as to efficiently be cut out of the stock. A set of files to make a small box are at:

[https://cutrocket.com/p/622970cdb482a/](https://cutrocket.com/p/622970cdb482a/)

When cut:

![](.gitbook/assets/WIN\_20220309\_21\_13\_49\_Pro.jpg)

the parts may then be assembled:

![](.gitbook/assets/WIN\_20220309\_21\_16\_14\_Pro.jpg)

making a finished box:

![](.gitbook/assets/WIN\_20220309\_21\_15\_28\_Pro.jpg)
