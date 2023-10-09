---
description: Design made up of discrete parts allows customization without programming.
---

# Adjustable Modular Designs

Full blind box joints may be cut instead with a radius. There are a couple of different features which make the joint work:

* a bisecting angle where the joint will be exposed&#x20;
* the fingerjoints, alternating so that they fit together

The fingerjoints fitting together, provides a great deal of glue surface:

![](.gitbook/assets/WIN\_20210711\_18\_46\_40\_Pro.jpg)

![](.gitbook/assets/WIN\_20210711\_18\_47\_23\_Pro.jpg)

Fitting the bottom and lid snuggly against fingers removes the need to remove material from the top and bottom fingers at the top and bottom angles --- if the box is sawn in twain so that it has a V area at that point it will then be necessary to relieve the material where the V endmill cannot cut for the fingers directly above and below the lid.

The initial part of the joint is made by cutting away as much of the angles as can be using a ball-nosed endmill, and machining the fingers. Laying out two parts at once makes this easier to see, and allows one to cut both a front/back and one of the sides in a single operation. The specifics of the first example joint are:

* 1/4"  thick and 3.5" wide stock
* cut using a 1/8" ball-nosed endmill, a 1/8" 90 degree V endmill, a suitably small endmill for relieving the board to make cutting the box apart to open it easier, and a cove radius endmill which matches the radius of the ball endmill

![](<.gitbook/assets/image (62).png>)

![](<.gitbook/assets/image (207).png>)

Then the V angles are cut to make the miter:

![](<.gitbook/assets/image (324).png>)

![](<.gitbook/assets/image (59).png>)

Then, a cove radius endmill is used to relieve the fingers:

![](<.gitbook/assets/image (257).png>)

(which cut Carbide Create cannot preview accurately at this time, so the tool used is simply provided with appropriate feeds and speed and set to a diameter which will show)

![](<.gitbook/assets/image (90).png>)

Lastly the pockets for the top and bottom and relief and indicator cuts for sawing off the lid are drawn in and then suitable toolpaths applied:

![](<.gitbook/assets/image (240).png>)

![](<.gitbook/assets/image (298).png>)

With the joint laid out, while it is specific to a given size of board (though it can easily be adapted to narrower boards by deleting finger pairs and adjusting the placement of the remaining elements) it is a simple matter to adjust the file for a given depth and width of box --- simply open the file and adjust the width to match the sum of the lengths of the parts.

The file is available at: [https://community.carbide3d.com/t/modular-joinery-system-for-blind-miter-fingerjoint-boxes/36161](https://community.carbide3d.com/t/modular-joinery-system-for-blind-miter-fingerjoint-boxes/36161)

To adjust it for a given box size, add the desired depth and width of the box to arrive at the width required for the stock. If using pre-cut pieces for the top and bottom, use that dimension, plus the stock thickness, plus some reasonable dimension for play. In this case, the pre-cut piece is a 200mm × 200mm piece of two-color HDPE, so 8.125" × 8.125" for box dimensions, and the stock area should be 16.25" wide:

![](<.gitbook/assets/image (323).png>)

![](<.gitbook/assets/image (152).png>)

Select everything and then go into Node Edit mode:

![](<.gitbook/assets/image (243).png>)

Drag-select all nodes associated with the right most joint:

![](<.gitbook/assets/image (277).png>)

and drag it to the far-right, so that it has the same relative position to the end of the stock as previously:

![](<.gitbook/assets/image (211).png>)

Draw in a rectangle which defines one of the two parts and is placed to match the stock:

![](<.gitbook/assets/image (34).png>)

Then select everything but this rectangle and again go into Node Edit mode and select the nodes associated with the middle two joints:

![](<.gitbook/assets/image (37).png>)

and drag them into position relative to the rectangle which defines where the two parts are cut away at:

![](<.gitbook/assets/image (264).png>)

Verify the positioning of everything and check with the 3D preview:

![](<.gitbook/assets/image (250).png>)

