---
description: Cutting fingerjoints vertically in boards at the front of the machine
---

# Fingerjoints

Starting with the box design template from the previous chapter: [https://www.blockscad3d.com/community/projects/965700](https://www.blockscad3d.com/community/projects/965700) it is a simple matter of adding cuts for joinery along the corners of the box. Fingerjoints are notable since they can be implemented along all edges of a box and with a bit of a relief can be cut flat on the machine simplifying fixturing and making manufacture more efficient, but the traditional technique of fingerjoints at the box corner with the top and bottom in rabbeted grooves is simpler to calculate.

If fingerjoints are cut in sheet goods with the boards flat, it is necessarily more complex

The interplay of the geometry of the board being flat and the cutter being round requires certain options and accommodations in the module for cutting the joints. It is necessary to specify:

* Endmill Diameter
* Whether the cut should be adjusted for endmill diameter
* Whether the cut should be relieved for endmill diameter
* If the cut should be adjusted at its beginning or end for the thickness of the material



 

