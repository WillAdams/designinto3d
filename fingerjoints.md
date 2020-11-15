---
description: Cutting fingerjoints vertically in boards at the front of the machine
---

# Fingerjoints

Starting with the box design template from the previous chapter: [https://www.blockscad3d.com/community/projects/1012246](https://www.blockscad3d.com/community/projects/1012246) it is a simple matter of adding cuts for joinery along the corners of the box. Fingerjoints are notable since they can be implemented along all edges of a box and with a bit of a relief can be cut flat on the machine simplifying fixturing and making manufacture more efficient, but the traditional technique of fingerjoints at the box corner with the top and bottom in rabbeted grooves is simpler to calculate.

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



 

