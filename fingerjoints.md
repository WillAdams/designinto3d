---
description: Cutting fingerjoints vertically in boards at the front of the machine
---

# Fingerjoints

Starting with the box design template from the previous chapter: [https://www.blockscad3d.com/community/projects/1012246](https://www.blockscad3d.com/community/projects/1012246) it is a simple matter of adding cuts for joinery along the corners of the box. Fingerjoints are notable since they can be implemented along all edges of a box and with a bit of a relief can be cut flat on the machine simplifying fixturing and making manufacture more efficient, but the traditional technique of fingerjoints at the box corner with the top and bottom in rabbeted grooves is simpler to calculate, and is discussed at: [https://community.carbide3d.com/t/cnc-finger-joint-box/8880](https://community.carbide3d.com/t/cnc-finger-joint-box/8880) and will be worked out in detail below.

Necessary additional variables are:

* Endmill Diameter
* Thickness of top/bottom grooves \(or possibly rabbets for reducing board thickness along edges to fit into grooves\)
* \(optional\) a number to influence how many fingers will be cut
* Some sort of option for the lid ― options include a sliding lid, a rabbet along the edge for the lid to fit onto, or a through cut after glue-up and a suitable hinge

If fingerjoints are cut in sheet goods with the boards flat, it is necessarily more complex

The interplay of the geometry of the board being flat and the cutter being round requires certain options and accommodations in the module for cutting the joints. It is necessary to specify:

* Endmill Diameter
* Whether the cut should be adjusted for endmill diameter
* Whether the cut should be relieved for endmill diameter
* If the cut should be adjusted at its beginning or end for the thickness of the material

Setting up a box design for this we duplicate the project from the previous chapter as: [https://www.blockscad3d.com/community/projects/1052045](https://www.blockscad3d.com/community/projects/1052045) and update it with the desired dimensions:

* 10 in wide
* 8 in deep
* 3.5 in high
* 0.25" thick stock
* 0.21653543" \(5.5mm\) thick top and bottom
* 0.375" part spacing

![BlockSCAD: Fingerjoints: Vertical: Variables](.gitbook/assets/blockscad-fingerjoint-vertical-variables.png)

Add code to cut grooves for the lid and for the fingerjoints themselves:

![BlockSCAD: Fingerjoints: Vertical: Features](.gitbook/assets/blockscad-fingerjoint-vertical-features.png)

 as well as laying out the parts for cutting:

![BlockSCAD: Fingerjoints: Vertical: DXF](.gitbook/assets/blockscad-fingerjoint-vertical-dxf.png)

The final aspect is cutting the joints ― the boards need to be offset from each other:

![BlockSCAD: Fingerjoints: Vertical: Boards](.gitbook/assets/blockscad-fingerjoint-vertical-boards.png)

and cut in at least pairs \(cutting all four at once will halve the number of operations\):

![BlockSCAD: Fingerjoints: Vertical: Cuts](.gitbook/assets/blockscad-fingerjoint-vertical-cuts.png)

See: [https://www.blockscad3d.com/community/projects/1053568](https://www.blockscad3d.com/community/projects/1053568)

Export to OpenSCAD from BlockSCAD and then customize the file in OpenSCAD to allow exporting SVGs:

![OpenSCAD: Fingerjoints: Vertical: Parts](.gitbook/assets/openscad-fingerjoint-vertical-parts.png)

![OpenSCAD: Fingerjoints: Vertical: Cuts](.gitbook/assets/openscad-fingerjoint-vertical-cuts.png)

The OpenSCAD file is available at: [https://github.com/WillAdams/Design\_Into\_3D/blob/master/box/fingerjoint/vertical/Box\_%20Fingerjoint\_%20Vertical.scad](https://github.com/WillAdams/Design_Into_3D/blob/master/box/fingerjoint/vertical/Box_%20Fingerjoint_%20Vertical.scad)

Export each view and import into Carbide Create files:

![Carbide Create: Fingerjoints: Vertical: Parts](.gitbook/assets/carbidecreate-fingerjoint-vertical-parts.png)

![Carbide Create: Fingerjoints: Vertical: Cuts](.gitbook/assets/carbidecreate-fingerjoint-vertical-cuts.png)

Once imported, it will be helpful for the Cuts file to set the stock size to match the boards being used, and to draw in rectangles representing the boards --- this will help to make clear how they are to be positioned for cutting and how the toolpaths will interact. The 3D preview of the toolpaths shows the cuts which will be made which is accurate save for the excess stock shown at the upper left and lower right corners \(areas not encompassed by the orange highlighted boards in the image above\):

![Carbide Create: Fingerjoints: Vertical: Cut 3D Preview](.gitbook/assets/carbidecreate-fingerjoint-vertical-cut-preview.png)

For the Parts file, it is only necessary at first to cut one side, and a single instance of the front/back part --- the parts need to be positioned in-line and separated by at least the endmill diameter plus 10%. The top/bottom will be measured for from the actual box after it is cut and dry fit. A further consideration here is the matter of accessing the interior of the box --- we will draw in a rectangle which may be cut with a narrow endmill \(or one may do the traditional cutting apart with a bandsaw or hand saw\):

![Carbide Create: Fingerjoints: Vertical: Parts in-line](.gitbook/assets/carbidecreate-fingerjoint-vertical-parts-inline.png)

Since the parts will be cut from an S4S board which is the correct size, it will only be necessary to machine the grooves for the top/bottom, the groove with tabs separating the lid from the base of the box \(import a copy of the fingerjoint cuts and rotate 90 degrees to allow for placement\), and pockets at the ends of each board to cut them to length. To eliminate the need for tabs and the attendant post-processing, work-holding will be two-stage:

* normal clamps outside the cutting area as well as a sacrificial caul clamp across the gap between the parts
* additional cauls added after cutting the grooves to secure the stock and ensure the parts do not move once cut free

To ensure the board is square to the machine the first operation will be to machine a pocket in which to register the board, then the board will be secured and the grooves cut, then the additional cauls put in place, and the last operation will be cutting the pockets which cut the part to length.

![Carbide Create: Fingerjoints: Vertical: Toolpaths](.gitbook/assets/carbidecreate-fingerjoint-vertical-parts-toolpaths.png)

Verify the preview:

![Carbide Create: Fingerjoints: Vertical: Parts Preview](.gitbook/assets/carbidecreate-fingerjoint-vertical-parts-preview.png)

Then cut the parts, then mount them in a fixture such as: [https://cutrocket.com/p/5cb25f3380844/](https://cutrocket.com/p/5cb25f3380844/) and cut the joints, then dry-fit to measure for cutting the top/bottom.

 

