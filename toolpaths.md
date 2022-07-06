---
description: Toolpath options in Carbide Create
---

# Toolpaths

Carbide Create affords a number of different toolpath options which provide for a wide variety of geometries which may be cut away from material depending on the endmill used. Carbide Create includes support for the following endmill/tool types:

* square
* ball-nosed
* V-endmill
* engravers

Early versions of Carbide Create had limitations in terms of which endmill type could be assigned to which toolpath, but 629 added support for using V endmills with non-V-carving-specific toolpaths.

The following toolpaths are either for decorative use or for Carbide Create Pro only and so will not be considered at this time:

* Texture (decorative)
* Engrave (Pro only)
* 3D Rough (Pro only)
* 3D Finish (Pro only)

Normally square endmills will be used for removing material and creating flat-bottomed pockets and making profile cuts all the way through material to cut parts free, ball-nosed endmills will be used to create rounded forms (including 3D), and V endmills will be used for V carving or chamfering or cutting at a precise angle as for certain types of joinery.

## Contour

Contour toolpaths follow along a drawn element of geometry, and will be aligned relatively along it based on path orientation/direction which will determine the Offset Direction:

* Inside / Left
* No Offset (directly along the path)
* Outside / Right

Where the toolpath will fall relative to the geometry will always be clear when viewed in the 3D preview, and the offsets will alter the geometry of features — given a 1" circle cut with a 1/4" square endmill the following dimensions will be realized:

![Carbide Create | Contour Toolpath | Offsets](<.gitbook/assets/image (91).png>)

* Inside / Left — a 1" hole will be made, and a post 1/2" in diameter will be left
* No Offset — a 1.25" hole will be made, and a post 0.75" in diameter will be left
* Outside / Right — a 1.5" hole will be made, and a post 1" in diameter will be left

When not cutting all the way through with a square endmill, a square walled slot will result:

![](<.gitbook/assets/image (90).png>)

If cut with a ball-nosed endmill, a rounded groove may be achieved:

![](<.gitbook/assets/image (89).png>)

One option for Contour Toolpaths is tabs. In Carbide Create v7 they may be added in the Design tab:

![](<.gitbook/assets/image (122) (1).png>)

## Pocket

Pocket toolpaths allow cutting out the interior of geometry:

![](<.gitbook/assets/image (119) (1) (1) (1) (1) (1).png>)

which will be a flat bottomed pocket with vertical walls if cut out with a square endmill.

If one uses a ball-nosed endmill, the edges will be rounded, the bottom will be scalloped, and there may be artifacts left behind:

![](<.gitbook/assets/image (114) (1) (1) (1).png>)

If there is nested geometry, then the pocketing algorithm will alternate between cutting and not cutting, leaving islands:

![](<.gitbook/assets/image (121) (1) (1) (1) (1) (1) (1).png>)

![](<.gitbook/assets/image (116) (1) (1) (1) (1).png>)

One option for pocket toolpaths in some CAM programs is Rest machining to remove material which the endmill first used for a pocket cannot reach. Carbide Create Pro adds this:

![](<.gitbook/assets/image (123) (1).png>)

Rest machining allows removing this by indicating the previous size tool used and selecting a smaller tool to cut those areas which cannot be reached:

![](<.gitbook/assets/image (129).png>)

## Drill

Drill toolpaths plunge the tool at the center of the selected geometry:

![](<.gitbook/assets/image (116) (1) (1) (1).png>)

As noted above, square, ball-nosed, and V-endmills may be used, and will be correctly previewed in how they cut:

![](<.gitbook/assets/image (120) (1) (1) (1) (1).png>)

A notable use for a V-endmill when drilling is to chamfer a small hole.

## VCarve (and Advanced VCarve)

V carving toolpaths may be assigned to closed geometry, and as noted above, will cut either along the center (normal V carving), or along the perimeter (Advanced V carving), to either the depth required, or the max depth which is set.

If one limits the depth on a normal V carve, one can achieve special effects such as changing a square:

![](<.gitbook/assets/image (116) (1) (1).png>)

into a diamond:

![](<.gitbook/assets/image (113) (1).png>)
