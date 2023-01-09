---
description: Cutting box joints on boards flat on the machine
---

# Radiused Box joints

There are many examples of cutting box joints with dogbones to allow for the radius on an endmill, which works, but results in visible voids in the project. An alternative technique is to cut the box joints and then use a cove radius endmill to round off the box joints as necessary allowing for a joint which does not have visible voids. For discussion see: [https://community.carbide3d.com/t/design-into-3d-boxes-magazine-storage/16238](https://community.carbide3d.com/t/design-into-3d-boxes-magazine-storage/16238)

As shown there, one option is to add geometry to relieve the box using a V carving toolpath. This works, but results in visible voids since the straight line of the V angle doesn't match the arc of the radius left by the round endmill.

Interestingly, it is possible to take a file intended for lasercutting and simply add some geometry for the radiusing and then cut out the box (if one is willing to forgo an accurate 3D preview of the cut). Since this affords an expedient technique which allows approaching the project in a straight-forward fashion which can be built on to understand the concepts in question, this will be shown first.

## Generate the Design

Start with a suitable generator ― we will use:

{% embed url="https://www.makercase.com/" %}

This project will be a 3" x 3" x 3" open box:

![MakerCase: 3" x 3" x 3" Open Box](<.gitbook/assets/makercase\_3x3x3\_open (1).png>)

Download the box plans as an SVG:

![MakerCase: 3" x 3" x 3" Open Box: SVG Plans](.gitbook/assets/box.svg)

Import them into Carbide Create and arrange for cutting:

![Carbide Create: 3" x 3" x 3" Open Box: SVG Plans: Imported and arranged](.gitbook/assets/cc\_makercase\_3x3x3\_import.png)

Note that MakerCase tool allowed one to set the stock thickness (0.25") and the same dimension should be used in Carbide Create.&#x20;

### Making the Bottom

Reworking the files is a useful review of how the box is constructed. Starting with the bottom, draw a box the size of the base:

![Carbide Create: Radiused Box joints: 3" x 3" x 3": Bottom Outline ](.gitbook/assets/cc\_radiused\_fingerjoints\_3x3x3\_bottom\_initial\_outline.png)

Inset by the thickness of the stock which will be used (plus desired glueline if need be):

![Carbide Create: Radiused box joints: 3" x 3" x 3": Bottom Inset](.gitbook/assets/cc\_radiused\_fingerjoints\_3x3x3\_bottom\_bottom\_inset.png)

The design will not be precisely recreated, but the basic concept will be followed. The bottom is symmetrical which makes later design easier, and the box joints are inset somewhat ― we will use half the stock thickness, so adjust the grid spacing accordingly and draw in a rectangle which represents this length centered at one edge of the box:

![Carbide Create: Radiused box joints: 3" x 3" x 3": Initial Joinery](<.gitbook/assets/image (24).png>)

This needs to be divided into fifths (two box and three gaps):

![Carbide Create: Radiused box joints: 3" x 3" x 3": Box Joint Width](<.gitbook/assets/image (6).png>)

And then duplicated and dragged into registration with the desired positioning:

![Carbide Create: Radiused box joints: 3" x 3" x 3": Box Joint Width](<.gitbook/assets/image (1) (1) (1).png>)

Then set the rectangles at the box joint locations to be the height of the box and drag them into position:

![Carbide Create: Radiused box joints: 3" x 3" x 3": Vertical Box Joints](<.gitbook/assets/image (7) (1).png>)

Since the box is square, the two box joints and the outer rectangle may be duplicated, rotated 90 degrees, and dragged into registration with the part:

![Carbide Create: Radiused box joints: 3" x 3" x 3": Vertical Box Joints](<.gitbook/assets/image (10).png>)

Select the narrow rectangles for the box joints and the inset of the bottom:

![Carbide Create: Radiused box joints: 3" x 3" x 3": Box Joints and Inset Base](<.gitbook/assets/image (23).png>)

And then Boolean union:

![Carbide Create: Radiused box joints: 3" x 3" x 3": Finished Bottom](<.gitbook/assets/image (22).png>)

### Making the Sides

For the sides we can recycle the remaining rectangles by setting them to the same thickness and aligning them with the base and recreating the inset and Boolean unioning the parts:

![Carbide Create: Radiused box joints: 3" x 3" x 3": Bottom Box Joints for Sides](<.gitbook/assets/image (3) (1) (2).png>)

### Making the Front/Back

![Carbide Create: Radiused box joints: 3" x 3" x 3": Side after Boolean Union](<.gitbook/assets/image (3) (1) (1).png>)

(Alternately, the bottom could have been duplicated, rotated and aligned against the bottom and Boolean subtracted.)

Since the box is symmetrical on can re-use the previous set of rectangles and create a crossing set which may then be Boolean unioned:

![Carbide Create: Radiused box joints: 3" x 3" x 3": Side before Boolean Union](<.gitbook/assets/image (11).png>)

At which point one simply has to fill in the top and clean up the bottom:

![Carbide Create: Radiused box joints: 3" x 3" x 3": Side](<.gitbook/assets/image (12).png>)

Repeat a similar process for the front/back:

![Carbide Create: Radiused Box joints: 3" x 3" x 3": Side](<.gitbook/assets/image (16).png>)

Duplicate the geometry for the front/back and sides and arrange them with the bottom part in a single file as before.

## Model the Endmill

Unfortunately, Carbide Create doesn't support cove radius endmill geometry, so it will be necessary to work out where to place lines so as to cut the desired radius ― draw up a profile of your endmill to work this out ― a cove radius should have a tip diameter, a diameter at the top which determines how widely it will cut, a total cutting height, and of course the radius itself.

The endmill used will be a 5/16" (8mm) diameter endmill with 1/8" cove radius with 1/16" tip to match a 1/4" diameter endmill: &#x20;

![Cove radius endmill: 1/8" radius](.gitbook/assets/20201206\_085531-1-.jpg)

![Diagram: Cove radius endmill: 1/8" radius](.gitbook/assets/tool\_cove\_radius\_0\_25.png)

Then draw up the side view to help determine where the cut should be made and draw in the tooling showing where the cuts should (and should not) be made:

![Carbide Create: Radiused Box joints: 3" x 3" x 3": Side View of Bottom](<.gitbook/assets/image (9) (1).png>)

If we modify a copy of the front/back part to show the radius which will be left when cutting it can be dragged into place to verify the fit:

![Carbide Create: Radiused box joints: 3" x 3" x 3": Radius Preview](<.gitbook/assets/image (5) (1).png>)

With the geometry verified it is now possible to draw in circles which will allow us to determine where the cove radius endmill will cut and connect their centerpoints with the lines along which the tool should move:

![Carbide Create: Radiused box joints: 3" x 3" x 3": Toolpath Preview](<.gitbook/assets/image (18).png>)

Use that construct to place lines relative to each edge which needs to be radiused:

![Carbide Create: Radiused box joints: 3" x 3" x 3": Radius Lines](<.gitbook/assets/image (21).png>)

At this point one could go to the Toolpath pane and set up all the cuts, but since a cove radius endmill cannot be previewed in Carbide Create we will instead model the endmill, and then the design in BlockSCAD/OpenSCAD.

Due to limitations of the Computational Solid Geometry (CSG) kernel used in OpenSCAD and similar modeling techniques used in other CAM tools it is not possible to directly model a cove radius endmill in 3D. A work-around for this limitation in OpenSCAD is to instead model a series of stacked truncated inverted cones which are hulled together for each layer:

![OpenSCAD: Modeling Cove Radius Endmill](<.gitbook/assets/image (4) (1) (1).png>)

## Model the Box

As before, start with the prototype box from:

{% embed url="https://www.blockscad3d.com/community/projects/1012246" %}

Save it as a copy with a new name and set parameters as desired:

![BlockSCAD: Box: 3" x 3" x 3"](<.gitbook/assets/image (14).png>)

Note however, that it can be a source of potential error to have the same value inputs when programming, so temporarily change the values for Height, Width, and Depth to 3, 4, and 5 respectively.

Work up modules and alter things as needed to add the joinery which matches what has already been drawn:

![BlockSCAD: Box: 3" x 3" x 3": Box joints](<.gitbook/assets/image (17).png>)

Available at:&#x20;

{% embed url="https://www.blockscad3d.com/community/projects/1065533" %}

## Model the Joinery

Export the OpenSCAD code and then test it to determine what material intersects and needs to be removed:

![OpenSCAD: Box: 3" x 3" x 3": Intersecting Areas](<.gitbook/assets/image (25).png>)

Modify the module for the box joint cuts to round them off:

![OpenSCAD: Box: 3" x 3" x 3": Radiused Box Joints](<.gitbook/assets/image (19).png>)

Repeating the intersection verifies that the rounding works:

![OpenSCAD: Box: 3" x 3" x 3": Intersecting Thinness](<.gitbook/assets/image (15).png>)

But unfortunately also indicates that some material will be left for a fit which would require post-processing. The tip on the cove radius endmill selected above is too wide to clear this material without leaving a void larger than is desired or one which would be visible inside the box, so the solution is to draw in a suitable geometry to clear this material as a V carving.

![Carbide Create: Box: 3" x 3" x 3": Geometry for V carving](<.gitbook/assets/image (54).png>)

With the rounding working the 3D model is verified:

![OpenSCAD: Box: 3" x 3" x 3": Radius and V carving Relief cut](<.gitbook/assets/image (52).png>)

Including the intersection:

![OpenSCAD: Box: 3" x 3" x 3": Radius and V carving Relief cut intersection](<.gitbook/assets/image (53).png>)

Which once verified, allows us to preview the box:

![OpenSCAD: Box: 3" x 3" x 3": 3D Model](<.gitbook/assets/image (57).png>)

The OpenSCAD source is available at: [https://github.com/WillAdams/Design\_Into\_3D/blob/master/box/fingerjoint/radius/Design%20into%203D\_%20Box\_%20fingerjoint\_radius.scad](https://github.com/WillAdams/Design\_Into\_3D/blob/master/box/fingerjoint/radius/Design%20into%203D\_%20Box\_%20fingerjoint\_radius.scad)

Unfortunately, that file is not directly useful for CAM work, since it is not possible to export an unclosed path as a DXF or SVG from OpenSCAD. There is code for directly exporting G-Code commented out of the above, but due to limitations of coordinates and arguments in OpenSCAD and possibly rounding issues as well as the specific steps required to get a suitable text file out of OpenSCAD the effort has been set aside for the time being.

## Make the Box

With the concept proven out it is simply a matter of making the toolpaths to cut out the design. As noted above, while it is possible to create the toolpaths, it is not possible to directly preview the tool cutting shape with any readily available tool.

With the parts laid out, select the part outlines and offset them a suitable distance:

![Carbide Create: Box: 3" x 3" x 3": Parts Outline](<.gitbook/assets/image (27).png>)

Select the outline and the parts and assign a pocket toolpath which will cut down to tab depth:

![Carbide Create: Box: 3" x 3" x 3": Parts Toolpath](<.gitbook/assets/image (29).png>)

Select the lines for the relief cut, select a suitable tool and assign it a suitable tool cutting to a depth which will cut the relief (in this case 0.125") ― the actual tool used doesn't matter since it's not possible to get a correct preview, but matching the outer diameter if convenient will help in verifying the cut:

![Carbide Create: Box: 3" x 3" x 3": Radius Toolpath](<.gitbook/assets/image (30).png>)

Then add the geometry for the internal (hidden) V carving relief:

![](<.gitbook/assets/image (55).png>)

Next add an outer profile toolpath to cut out the parts:

![Carbide Create: Box: 3" x 3" x 3": Profile Toolpath](<.gitbook/assets/image (26).png>)

And preview insofar as is possible:

![Carbide Create: Box: 3" x 3" x 3": Preview using square and V endmills](<.gitbook/assets/image (56).png>)

Lastly generate the G-Code, secure the stock, set zero relative to it, and cut the part out.

![Carbide Create: Box: 3" x 3" x 3": Successful cut](.gitbook/assets/20201229\_202932-1-.jpg)

The parts should then merely require separating and some basic cleanup with a sharp chisel and suitable files:

![Carbide Create: Box: 3" x 3" x 3": Parts ready for assembly](.gitbook/assets/20210101\_135801-1-.jpg)

Which then fit together:

![Carbide Create: Box: 3" x 3" x 3": Box](.gitbook/assets/20210101\_135732-1-.jpg)

A file for cutting this is available at: [https://community.carbide3d.com/t/design-into-3d-boxes-magazine-storage/16238/59](https://community.carbide3d.com/t/design-into-3d-boxes-magazine-storage/16238/59)

A noted above, it should be possible to create a program which converts the G-Code into an OpenSCAD file which could then be used to preview the cut.
