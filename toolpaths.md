---
description: Toolpath options in Carbide Create
---

# Toolpaths

Carbide Create affords a number of different toolpath options which provide for a wide variety of geometries which may be cut away from material depending on the endmill used. The first consideration is which sort of tool may be used with a given sort of toolpath. Carbide Create supports for the following endmill types:

* square
* ball-nosed
* V-endmill

The following toolpath types may be used with the following sorts of tools in Carbide Create:

* Contour --- square or ball-nosed endmills
* Pocket --- square or ball-nosed endmills
* Drill --- square, ball-nosed, or V-endmills
* VCarve --- only V-endmills
* Advanced VCarve --- V endmills must be used, but there is an option for a second tool for cutting a flat-bottomed pocket which a square endmill may be used for

The following toolpaths are for either decorative or for Carbide Create Pro only and so will not be considered at this time:

* Texture&#x20;
* Engrave (Pro only)
* 3D Rough (Pro only)
* 3D Finish (Pro only)

The most notable limitation is that V-endmills may only be used so as to get a correct 3D preview with the toolpaths which are specifically for V carving --- while they may be assigned to other toolpaths, the 3D preview will not be correct.

Normally square and ball-nosed endmills will have correct previews when used with various toolpaths.

## Contour

Contour toolpaths follow along a drawn element of geometry, and will be aligned relatively towards it based on path orientation/direction which will determine the Offset Direction:

* Inside / Left
* No Offset
* Outside / Right

Where the toolpath will fall relative to the geometry will always be clear when viewed in the 3D preview, and the offsets will alter the geometry of features --- given a 1" circle cut with a 1/4" square endmill the following dimensions will be realized:

![Carbide Create | Contour Toolpath | Offsets](<.gitbook/assets/image (91).png>)

* Inside / Left --- a 1" hole will be made, and a post 1/2" in diameter will be left
* No Offset --- a 1.25" hole will be made, and a post 0.75" in diameter will be left
* Outside / Right --- a 1.5" hole will be made, and a post 1" in diameter will be left

When not cutting all the way through, a square walled slot will result:

![](<.gitbook/assets/image (90).png>)

If cut with a ball-nosed endmill, a rounded groove may be achieved:

![](<.gitbook/assets/image (89).png>)

## Pocket

Pocket toolpaths allow cutting out the interior of geometry:

![](<.gitbook/assets/image (119).png>)

which will be a flat bottomed pocket with vertical walls if cut out with a square endmill.

If one uses a ball-nosed endmill, the bottom will be scalloped, and there may be artifacts left behind:

![](<.gitbook/assets/image (114).png>)

If there is nested geometry, then the pocketing algorithm will alternate between cutting and not cutting, leaving islands:

![](<.gitbook/assets/image (121).png>)

![](<.gitbook/assets/image (116) (1).png>)

## Drill

Drill toolpaths plunge the tool at the center of the selected geometry:

![](<.gitbook/assets/image (116).png>)

As noted above, square, ball-nosed, and V endmills may be used, and will be correctly previewed in how they cut:

![](<.gitbook/assets/image (120).png>)
