---
description: Cutting fingerjoints on boards flat on the machine
---

# Radiused Fingerjoints

There are many examples of cutting fingerjoints with dogbones to allow for the radius on an endmill, which works, but results in visible voids in the project. An alternative technique is to cut the fingerjoints and then use a cove radius endmill to round off the fingers as necessary allowing for a joint which does not have visible voids. For discussion see: [https://community.carbide3d.com/t/design-into-3d-boxes-magazine-storage/16238](https://community.carbide3d.com/t/design-into-3d-boxes-magazine-storage/16238)

Interestingly, it is possible to take a file intended for lasercutting and simply add some lines for the radiusing and then cut out the box \(if one is willing to forgo an accurate 3D preview of the cut\). Since this affords an expedient technique which allows approaching the project in a straight-forward fashion which can be built on to understand the concepts in question, this will be shown first.

## Generate the Design

Start with a suitable generator ― we will use:

{% embed url="https://www.makercase.com/" %}

This project will be a 3" x 3" x 3" open box:

![MakerCase: 3&quot; x 3&quot; x 3&quot; Open Box](.gitbook/assets/makercase_3x3x3_open%20%281%29.png)

Download the box plans as an SVG:

![MakerCase: 3&quot; x 3&quot; x 3&quot; Open Box: SVG Plans](.gitbook/assets/box.svg)

Import them into Carbide Create and arrange for cutting:

![Carbide Create: 3&quot; x 3&quot; x 3&quot; Open Box: SVG Plans: Imported and arranged](.gitbook/assets/cc_makercase_3x3x3_import.png)

_If_ the MakerCase tool allowed one to set the stock thickness \(0.25"\) which will be used. 

### Making the Bottom

Reworking the files is a useful review of how the box is constructed. Starting with the bottom, draw a box the size of the base:

![Carbide Create: Radiused Fingerjoints: 3&quot; x 3&quot; x 3&quot;: Bottom Outline ](.gitbook/assets/cc_radiused_fingerjoints_3x3x3_bottom_initial_outline.png)

Inset by the thickness of the stock which will be used \(plus desired glueline if need be\):

![Carbide Create: Radiused Fingerjoints: 3&quot; x 3&quot; x 3&quot;: Bottom Inset](.gitbook/assets/cc_radiused_fingerjoints_3x3x3_bottom_bottom_inset.png)

The design will not be precisely recreated, but the basic concept will be followed. The bottom is symmetrical which makes later design easier, and the fingerjoints are inset somewhat ― we will use half the stock thickness, so adjust the grid spacing accordingly and draw in a rectangle which represents this length centered at one edge of the box:

![Carbide Create: Radiused Fingerjoints: 3&quot; x 3&quot; x 3&quot;: Initial Joinery](.gitbook/assets/image%20%2810%29.png)

This needs to be divided into fifths \(two fingers and three gaps\):

![Carbide Create: Radiused Fingerjoints: 3&quot; x 3&quot; x 3&quot;: Finger Width](.gitbook/assets/image%20%283%29.png)

And then duplicated and dragged into registration with the desired positioning:

![Carbide Create: Radiused Fingerjoints: 3&quot; x 3&quot; x 3&quot;: Finger Width](.gitbook/assets/image%20%281%29.png)

Then set the rectangles at the finger locations to be the height of the box and drag them into position:

![Carbide Create: Radiused Fingerjoints: 3&quot; x 3&quot; x 3&quot;: Vertical Fingers](.gitbook/assets/image%20%284%29.png)

Since the box is square, the two fingers and the outer rectangle may be duplicated, rotated 90 degrees, and dragged into registration with the part:

![Carbide Create: Radiused Fingerjoints: 3&quot; x 3&quot; x 3&quot;: Vertical Fingers](.gitbook/assets/image%20%285%29.png)

Select the narrow rectangles for the fingers and the inset of the bottom:

![Carbide Create: Radiused Fingerjoints: 3&quot; x 3&quot; x 3&quot;: Fingers and Inset Base](.gitbook/assets/image%20%289%29.png)

And then Boolean union:

![Carbide Create: Radiused Fingerjoints: 3&quot; x 3&quot; x 3&quot;: Finished Bottom](.gitbook/assets/image%20%288%29.png)

### Making the Sides

For the sides we can recycle the remaining rectangles by setting them to the same thickness and aligning them with the base and recreating the inset and Boolean unioning the parts:

![Carbide Create: Radiused Fingerjoints: 3&quot; x 3&quot; x 3&quot;: Bottom Fingers for Sides](.gitbook/assets/image.png)

![Carbide Create: Radiused Fingerjoints: 3&quot; x 3&quot; x 3&quot;: Side after Boolean Union](.gitbook/assets/image%20%282%29.png)



## Model the Endmill

Unfortunately, Carbide Create doesn't support cove radius endmill geometry, so it will be necessary to work out where to place lines so as to cut the desired radius ― draw up a profile of your endmill to work this out ― a cove radius should have a tip diameter, a diameter at the top which determines how widely it will cut, a total cutting height, and of course the radius itself:

![Cove radius endmill: 1/4&quot; radius](.gitbook/assets/tool_cove_radius_0_25.png)

Then draw up the side view to help determine where the cut should be made and draw in the tooling showing where the cuts should \(and should not\) be made:



