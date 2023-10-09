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

Carbide Create Pro also adds the option of Ramping in for toolpaths, and Rest machining for Pockets.

The following toolpaths which Carbide Create supports will be discussed here:

* Contour
* Pocket
* Drill
* VCarve
* Advanced VCarve
* Keyhole

Normally square endmills will be used for removing material and creating flat-bottomed pockets and making profile cuts all the way through material to cut parts free, ball-nosed endmills will be used to create rounded forms (including 3D), and V endmills will be used for V carving or chamfering or cutting at a precise angle as for certain types of joinery. Keyhole toolpaths require the use of specialty keyhole cutters which cut wider at the bottom than their shaft. Surfacing tools such as the McFly are used to flatten stock or the spoilboard with either a very shallow pocket toolpath, or a contour toolpath which follows geometry which describes the area to be cut.

Note that in Carbide Create, dimensions may be entered using math expressions (which may contain units indicated by in or mm) which are evaluated by entering = at the end, so 1in+8mm= will result in a dimension of either 1.3150in or 33.400mm depending on the current unit.&#x20;

There are also 3 variables, _w_, _h_, and  _t_ may be used to reference the current stock width, height, and thickness respectively, and the expression may be left as an expression in certain fields by entering it without adding the = at the end, so t/2 will result in half the current stock thickness being used, and will update dynamically when the stock thickness is changed.

Carbide Create v7 adds the option of associating a Toolpath with the content of a specified layer.

## Contour

Contour toolpaths follow along one or more drawn element(s) of geometry, and will be aligned relatively based on path orientation/direction which will determine the Offset Direction:

* Inside / Left
* No Offset (directly along the path)
* Outside / Right

Where the toolpath will fall relative to the geometry will always be clear when viewed in the 3D preview, and the offsets will alter the geometry of features — given a 1" circle cut with a 1/4" square endmill the following dimensions will be realized:

![Carbide Create | Contour Toolpath | Offsets](<.gitbook/assets/image (10).png>)

* Inside / Left — a 1" hole will be made, matching the diameter of the original circle, and a post 1/2" in diameter will be left
* No Offset — a 1.25" hole will be made, and a post 0.75" in diameter will be left
* Outside / Right — a 1.5" hole will be made, and the original 1" diameter circle will be left as a column

When not cutting all the way through with a square endmill, a square walled slot will result:

![](<.gitbook/assets/image (113).png>)

If cut with a ball-nosed endmill, a rounded groove may be achieved:

![](<.gitbook/assets/image (4).png>)

One option for Contour Toolpaths is tabs. In Carbide Create v7 they may be added in the Design tab:

![](<.gitbook/assets/image (20).png>)

then the tabs may be instantiated in the Contour Toolpath setting.

## Pocket

Pocket toolpaths allow cutting out the interior of geometry:

![](<.gitbook/assets/image (89).png>)

which will be a flat bottomed pocket with vertical walls if cut out with a square endmill.

If one uses a ball-nosed endmill, the edges will be rounded, the bottom will be scalloped, and there may be artifacts left behind:

![](<.gitbook/assets/image (60).png>)

If there is nested geometry, then the pocketing algorithm will alternate between cutting and not cutting, leaving islands:

![](<.gitbook/assets/image (69).png>)

![](<.gitbook/assets/image (54).png>)

One option for pocket toolpaths in some CAM programs is Rest machining to remove material which the endmill first used for a pocket cannot reach. Carbide Create Pro adds this:

![](<.gitbook/assets/image (61).png>)

Rest machining allows removing uncut material where a larger endmill cannot reach by indicating the previous size tool used and selecting a smaller tool to cut those areas which were not previously cut away:

![](<.gitbook/assets/image (33).png>)

## Drill

Drill toolpaths plunge the tool at the center of the selected geometry:

![](<.gitbook/assets/image (91).png>)

As noted above, square, ball-nosed, and V-endmills may be used, and will be correctly previewed in how they cut:

![](<.gitbook/assets/image (249).png>)

A notable use for a V-endmill when drilling is to chamfer a small hole.

## VCarve (and Advanced VCarve)

V carving toolpaths may be assigned to closed geometry, and as noted above, will cut either along the center (normal V carving), or along the perimeter (Advanced V carving), to either the depth required, or the max depth which is set. Advanced VCarving adds the option of pocket clearing to the depth set w/ a different endmill.

If one limits the depth on a normal V carve, one can achieve special effects such as changing a square:

![](<.gitbook/assets/image (244).png>)

into a diamond:

![](<.gitbook/assets/image (16).png>)

## Keyhole

Keyhole toolpaths as noted above, require the use of a special tool, and are not previewed in 3D, since that would require undercuts which the 3D preview does not support. They have the tool plunging at the center of a specified geometry, then moving a fixed distance at a specified angle. It is best practice to machine away the material which may be reached using a normal tool first. For further details, see the discussion at: [https://community.carbide3d.com/t/using-a-keyhole-tool/39989](https://community.carbide3d.com/t/using-a-keyhole-tool/39989/38) and the actual announcement at: [https://community.carbide3d.com/t/carbide-create-v7-question-keyhole-toolpath/47489](https://community.carbide3d.com/t/carbide-create-v7-question-keyhole-toolpath/47489)

## Selection

There are two buttons in Toolpaths which function as the interface for what geometry is associated with a given toolpath:

* Change Vectors
* Select Current Vectors

and the resultant window for the former:

<figure><img src=".gitbook/assets/image (200).png" alt=""><figcaption></figcaption></figure>

also afford the option to associate toolpaths with a Layer. For a discussion of the interactions of selection and toolpaths see: [https://community.carbide3d.com/t/still-struggling-with-toolpath/63383](https://community.carbide3d.com/t/still-struggling-with-toolpath/63383) If more than one piece of geometry is associated with a toolpath, then their arrangement will determine how the toolpath is actually cut.

## Arrangement

As noted in [2D Drawing](2d-drawing.md#arrangement), there are several possible arrangements for multiple pieces of geometry:

* Adjacent/coincident --- the geometries are actually touching along some edges
* Overlapping/intersecting --- the geometries overlap or intersect
* Nesting --- each piece of geometry either contains, or is contained by the other piece(s) of geometry
* No interaction --- geometries do not interact in any fashion

Best practice is for geometries to either nest or have no interaction, and all toolpaths will work as expected for those two cases whether they expect closed or open geometry. Contour toolpaths which work along the geometry will work for any sort of arrangement (though the cutting of them may be repetitive/non-optimal). The other options will have implications for how Toolpaths which expect closed geometries are applied to geometry and interact:

* Adjacent/coincident --- such geometries will effectively be unioned when Toolpaths which interact with closed toolpaths are applied
* Overlapping/intersecting --- depending on the winding, intersecting areas will either be filled or not, which can be hard to predict --- when the Toolpaths are not as expected, it will be necessary to create Boolean Union and/or Intersections of geometry to create the desired effect

The most important consideration here is that it is consistent for a given version how a particular toolpath/geometry selection will be cut when a given toolpath is applied to it, so check the 3D preview, and if not as expected, select the geometry, go to the Design pane, and adjust as necessary to achieve the desired result, if need be, duplicating and unioning.

## Organization

Carbide Create affords the option of organizing toolpaths into groups --- this is done using a contextual right-click menu:

<figure><img src=".gitbook/assets/image (203).png" alt=""><figcaption></figcaption></figure>

Groups may be:

* Disabled/Enabled
* Deleted
* Moved up/down
* Renamed

and there is a menu entry for creating new groups.

Groups may be used to:

* organize toolpaths by tool&#x20;
* separate toolpaths for two-sided cutting
* separate toolpaths for tiling --- note that Carbide Create Pro now has a specific feature for this:  [https://community.carbide3d.com/t/toolpath-tiling-in-carbide-create-pro/59334](https://community.carbide3d.com/t/toolpath-tiling-in-carbide-create-pro/59334)
* separate toolpaths for individual parts

## G-code

Once toolpaths have been set up in a file, they may be sent to a machine to be cut out. The traditional way to do this is to write out the G-code instructions in a text file with a file extension which identifies is a a G-code file. Typically used extensions include:

* .nc
* .gc
* .gcode
* .tap

MeshCAM and early versions of Carbide Create add the possibility of a .egc file extension (for encrypted G-code), and Carbide Create v7 normally stores the G-code in the .c2d file itself, allowing that to be loaded into Carbide Motion when connected to a Carbide 3D machine, at which time the G-code will be extracted and sent to the machine. The Pro license for Carbide Create v7 also affords the option to write out G-code.
