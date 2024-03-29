---
description: Joining two or more pieces to create three dimensional parts.
---

# 3D Project

Removing one or more shapes from one piece of wood, and the negative of that shape from another so that the pieces fit together is the basis of wood joinery techniques, allowing one to extend wood from the single plane of a board. Traditional wood joinery often takes advantage of the sharp internal geometries which are possible with saws and chisels, but working with a router in a CNC requires us to take into consideration the rounded cut which an endmill will make if it does not cut past the edge of a part or cuts into a part with an internal angle.

The first machined joint which took into account the use of round tools to join parts was the Knapp joint: [https://furnishgreen.com/fun-furniture-fact-the-knapp-joint/](https://furnishgreen.com/fun-furniture-fact-the-knapp-joint/). See: [https://community.carbide3d.com/t/knapp-joint-with-cnc/19723](https://community.carbide3d.com/t/knapp-joint-with-cnc/19723) for further details and an example file. The problem with it and similar and traditional joints (_i.e._, dovetails, but also box/finger joints) is that they require a CNC which will allow for a fixture for holding boards on end when cutting such as: [https://cutrocket.com/p/5cb25f3380844/](https://cutrocket.com/p/5cb25f3380844/) and will at the least require 2 setups (clamp all four boards at once, cut one set of corner joints, and if feasible opposite ends) in addition to cutting boards to length and machining any features which one might need.

An alternative technique would be to lay the stock out flat and machine the edges so that things are not merely cut to size, but also have any necessary features cut in place and geometry along the edges which will allow parts to fit together. Finger joints are popular for this, and can be cut on a CNC if one finds the semicircular voids which are the result of cutting dogbones and similar features where necessary acceptable. For a lengthy discussion of this see: [https://community.carbide3d.com/t/design-into-3d-boxes-magazine-storage/16238](https://community.carbide3d.com/t/design-into-3d-boxes-magazine-storage/16238) (including a work-around which will be explored later in this text).

## The Simple Box Rabbeted Joint

One of the oldest of woodworking joints however is the rabbeted joint which fortuitously allows for this sort of thing without voids. It is so simple that it is the subject of a video, “The Simple Box” by Carbide 3D:

{% embed url="https://www.youtube.com/watch?v=V93xDM3lXsM" %}

which is discussed at: [https://community.carbide3d.com/t/a-simple-cnc-box-in-depth/7530](https://community.carbide3d.com/t/a-simple-cnc-box-in-depth/7530).&#x20;

A rabbeted joint has the following advantages over a simple butt joint:

* aligns along the join
* increased glue surface

Since it is cut at right angles, it is easily machined into stock which is laying flat on the machine bed, and it affords two options for orientation:

* use a larger endmill (easing machining) and depend on adhesives to secure the bottom and have a lid which lifts off
* use a smaller endmill and machine grooves trapping the lid and bottom (which is the technique used in the video linked above and which will be detailed in this chapter)

Other hybrid options are possible, and a style which uses butt joints for the ends and sides, and grooves (which are visible) for the lid and bottom is popular for inexpensive packaging.&#x20;

### Dimensions

The first consideration is overall dimensions, in this case 3″ wide × 7″ deep × 1½″ high, and the thickness of the stock, ¼″. Based on those, we draw up the three different views (clockwise from top-left: side, top/bottom, end):

![Carbide Create Initial view of Rabbeted Box 3×7×1½″](<.gitbook/assets/Carbide Create\_Rabbeted Box with features 3×7×1½\_initialview.png>)

Next, draw in the thickness of the material:

![Carbide Create Rabbeted Box 3×7×1½″ with boards drawn in.](<.gitbook/assets/Carbide Create\_Rabbeted Box with features 3×7×1½\_drawinboards.png>)

It is at the overlapping squares where it will be necessary to adjust the sizing of parts to accommodate rabbets and so forth. First, reduce the grid spacing to half the board thickness (0.25" so we change grid spacing to 0.125" in this case), then adjust parts to show the fit of the various rabbeted joints using Boolean operations:

![Carbide Create Rabbeted Box 3×7×1½″ with parts drawn in.](<.gitbook/assets/Carbide Create\_Rabbeted Box with features 3×7×1½\_drawinparts.png>)

To confirm these dimensions, we model things in 3D. All dimensions need to be specified in terms of the overall dimensions of the box and the stock thickness:

* 3" wide (along X)
* 7" deep (along Y)
* 1½″ high (along Z)
* ¼" thick (actual, not nominal thickness)

First these dimensions are entered into a 3D modeling system as parameters. For this, [BlockSCAD ](https://www.blockscad3d.com/)will be used: [https://www.blockscad3d.com/editor/](https://www.blockscad3d.com/editor/)

![BlockSCAD Rabbeted Box 3×7×1½″ dimensions as variables.](.gitbook/assets/BlockSCAD\_3D\_variables.png)

With the dimensions available one can then begin laying out the box and associated parts.

### Parts

Each part will ultimately need to be located within a cube the dimensions of the box:

![BlockSCAD Rabbeted Box 3×7×1½″ cube.](.gitbook/assets/BlockSCAD\_3D\_cube.png)

Start with the top/bottom, since its orientation and placement match that of the entire box in situ (save for the bottom being upside down). Note that it must be shifted within the box outline up and over by half the stock thickness (and reduced in dimensions by that as well), and that at this time, we will ignore the matter of toolpaths in doing the 3D modeling. However, best practice is to modularize the code, and that will be done:

![BlockSCAD Rabbeted Box 3×7×1½″ bottom.](.gitbook/assets/BlockSCAD\_3D\_makebottom.png)

It will be necessary to create some variables and code.

The BlockSCAD project for this is available at: [https://www.blockscad3d.com/community/projects/1048451](https://www.blockscad3d.com/community/projects/1048451)

For expedience the calculations are done directly (however, it is suggested for more complex projects that they be done either in variables, or calculated as modules). Similarly, it is simpler to create the part in an orientation which is easily machined, for the bottom for example, shown upside down relative its orientation in the box. A further consideration is that the rabbet should be slightly increased for the sake of the glue joint, and an option should be added for part spacing.

Taking all of that into account, it is straight-forward to show the different lengths and their attendant calculations with a bit of color-coding:

![BlockSCAD Rabbeted Box 3×7×1½″ parts and dimensions.](<.gitbook/assets/Rabbeted Box with features 3\_7\_1\_5\_partsdimensions (1).png>)

This should make it obvious that the box sides are the full depth of the box, while the box ends are the width of the box less twice the rabbet dimension (since they are inset into the sides). Similarly the bottom is the width and depth of the box less the rabbet twice over, since it is placed in grooves which are one rabbet deep, leaving one rabbet of thickness around it. Lastly the lid is the same width as the bottom, but is only shorter than the box depth by a single rabbet, since it aligns with the edge of the box at the opening.

Placement of the geometry for rabbets should be obvious from that as well, with anything which isn't clear working itself out in the course of drawing things up.

In Carbide Create begin by arranging rectangles of the appropriate sizes for the six parts needed:

![Carbide Create Rabbeted Box 3×7×1½″ part outlines only.](<.gitbook/assets/Rabbeted Box with features 3×7×1½\_partoutlinesonly.png>)

Model them by drawing in additional rectangles which represent the interior of the box to model the rabbets. Basically you need to draw outlines for all the stock which will be left uncut:

![Carbide Create Rabbeted Box 3×7×1½″ part geometry.](.gitbook/assets/Carbide\_Create\_screengrab\_rabbetedbox\_paths.PNG)

(and we've taken the liberty of drawing in the circle for the finger hole).

### Machining

Adding the machining operations takes us into the 3rd dimension. While one could most expediently add outline profiles only, the rabbets require additional geometry to cut their corners, and it is best practice to cut as a pocket down to tab depth.

Select the geometry for the parts and offset by a distance at least 10% greater than the diameter of the endmill which will be used:

![Carbide Create rabbeted box parts selected for offsetting.](<.gitbook/assets/Rabbeted Box with features 3×7×1½\_partoutlines\_selected.png>)

After, an optional optimization would be to edit out the small divots in the offset path:

![Carbide Create rabbeted box after offsetting parts.](<.gitbook/assets/Rabbeted Box with features 3×7×1½\_partoutlines\_offset.png>)

With the outer outlines for the rabbet/pocket made, it is simply a matter of selecting the feature geometries as well and pocketing to one-half the stock thickness:

![Carbide Create rabbeted box rabbets.](<.gitbook/assets/Carbide Create\_Rabbeted Box with features 3×7×1½\_rabbets.png>)

Then select each part outline and add suitable toolpaths and tabs to allow them to be cut free:

![Carbide Create rabbeted box toolpaths with tabs.](<.gitbook/assets/Carbide Create\_Rabbeted Box with features 3×7×1½\_rabbets\_profiles.png>)

The box may then be cut out, the pieces post-processed if need be (setting the Z origin on the spoilboard surface should minimize this), and then glued-up and assembled.

![Rabbeted box.](.gitbook/assets/WIN\_20200409\_22\_12\_01\_Pro.jpg)

See: [https://cutrocket.com/p/5e8fd99cc1578/](https://cutrocket.com/p/5e8fd99cc1578/)

### Variation: Rabbeted Box: 1½″ × 1½″ × 8″&#x20;

Creating a variation is simply a matter of entering the new dimensions (height, width, depth, stock thickness) into the BlockSCAD or OpenSCAD program, exporting an SVG, then re-arranging in the CAM program to create a file to cut which is efficient in terms of material usage, or directly creating a file in Carbide Create per the relative dimensions and techniques noted above.

![BlocksCAD: Rabbeted Box: 1½″ × 1½″ × 8″](<.gitbook/assets/Rabbeted Box with features 1\_5x8x1\_5\_BlockSCAD.png>)

See: [https://www.blockscad3d.com/community/projects/819419](https://www.blockscad3d.com/community/projects/819419)

Or in Carbide Create:

![Carbide Create: Rabbeted Box: 1½″ × 1½″ × 8″](<.gitbook/assets/Rabbeted Box with features 1\_5x8x1\_5\_Carbide Create.png>)

See: [https://cutrocket.com/p/5fb0a1afbf9d6/](https://cutrocket.com/p/5fb0a1afbf9d6/) for a file, and comments and discussion: [https://community.carbide3d.com/t/design-into-3d-rabbeted-box-with-features/20741/36](https://community.carbide3d.com/t/design-into-3d-rabbeted-box-with-features/20741/36).
