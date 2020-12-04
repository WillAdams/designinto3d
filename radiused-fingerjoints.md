---
description: Cutting fingerjoints on boards flat on the machine
---

# Radiused Fingerjoints

There are many examples of cutting fingerjoints with dogbones to allow for the radius on an endmill, which works, but results in visible voids in the project. An alternative approach is to cut the fingerjoints and then use a cove radius endmill to round off the fingers as necessary allowing for a joint which does not have visible voids. For discussion see: [https://community.carbide3d.com/t/design-into-3d-boxes-magazine-storage/16238](https://community.carbide3d.com/t/design-into-3d-boxes-magazine-storage/16238)

Interestingly, it is possible to take a file intended for lasercutting and simply add some lines for the radiusing and then cut out the box \(if one is willing to forgo an accurate 3D preview of the cut\). Since this affords an expedient approach which allows approaching the project in a straight-forward fashion which can be built on to understand the approach, this will be shown first.

Start with a suitable generator ― we will use:

{% embed url="https://www.makercase.com/" %}

This project will be a 3" x 3" x 3" open box:

![MakerCase: 3&quot; x 3&quot; x 3&quot; Open Box](.gitbook/assets/makercase_3x3x3_open%20%281%29.png)

Download the box plans as an SVG:

![MakerCase: 3&quot; x 3&quot; x 3&quot; Open Box: SVG Plans](.gitbook/assets/box.svg)

Import them into Carbide Create and arrange for cutting:

![Carbide Create: 3&quot; x 3&quot; x 3&quot; Open Box: SVG Plans: Imported and arranged](.gitbook/assets/cc_makercase_3x3x3_import.png)

Unfortunately, Carbide Create doesn't support cove radius endmill geometry, so it will be necessary to work out where to place lines so as to cut the desired radius ― draw up a profile of your endmill to work this out ― a cove radius should have a tip diameter, a diameter at the top which determines how widely it will cut, a total cutting height, and of course the radius itself:



