---
description: Design made up of discrete parts allows customization without programming.
---

# Adjustable Modular Designs

The ideal joint would be void free and not show any endgrain, while being self-aligning and offering sufficient long-grain glue surface for strength --- the classic example of this is the blind miter dovetail which is pretty much the exclusive domain of hand tool woodworking.

A similar design would be the blind miter box or fingerjoint which has seen a number of implementations:

* [https://joinerynotebook.blogspot.com/2016/03/blind-mitered-finger-joint-boxes.html](https://joinerynotebook.blogspot.com/2016/03/blind-mitered-finger-joint-boxes.html)
* [https://www.finewoodworking.com/2012/05/05/cutting-and-fitting-a-blind-finger-joint](https://www.finewoodworking.com/2012/05/05/cutting-and-fitting-a-blind-finger-joint)
* [https://community.carbide3d.com/t/full-blind-finger-joints/947](https://community.carbide3d.com/t/full-blind-finger-joints/947)
* [https://community.carbide3d.com/t/overengineered-box-for-the-endmills-i-dont-have-yet/429](https://community.carbide3d.com/t/overengineered-box-for-the-endmills-i-dont-have-yet/429)

As the latter two links make clear, there are two possible approaches:&#x20;

* Use the radius of the endmill to define the fingers so as to minimize endgrain--endgrain connections
* Overcut with dogbones which makes the layout simpler

The former can become quite complex and requires over-cutting where the fingers and miter angle intersect which creates voids, while the latter has voids designed in.

There are a couple of different features which make the joint work:

* a bisecting angle where the joint will be exposed&#x20;
* the fingerjoints, alternating so that they fit together

The fingerjoints fitting together, provides a great deal of glue surface:

![](.gitbook/assets/win\_20210711\_18\_46\_40\_pro.jpg)

![](.gitbook/assets/win\_20210711\_18\_47\_23\_pro.jpg)

Fitting the bottom and lid snuggly against fingers removes the need to remove material from the top and bottom fingers at the top and bottom angles --- if the box is sawn in twain so that it has a V area at that point it will then be necessary to relieve the material where the V endmill cannot cut for the fingers directly above and below the lid.

The initial part of the joint is made by cutting away as much of the angles as can be using a ball-nosed endmill, and machining the fingers. Laying out two parts at once makes this easier to see, and allows one to cut both a front/back and one of the sides in a single operation. The specifics of the first example joint are:

* 1/4"  thick and 3.5" wide stock
* cut using a 1/8" ball-nosed endmill, a 1/8" 90 degree V endmill, a suitably small endmill for relieving the board to make cutting the box apart to open it easier, and a cove radius endmill which matches the radius of the ball endmill

![](<.gitbook/assets/image (99).png>)

![](<.gitbook/assets/image (92).png>)

Then the V angles are cut to make the miter:

![](<.gitbook/assets/image (97).png>)

![](<.gitbook/assets/image (98).png>)

Then, a cove radius endmill is used to relieve the fingers:

![](<.gitbook/assets/image (93).png>)

(which cut Carbide Create cannot preview accurately at this time, so the tool used is simply provided with appropriate feeds and speed and set to a diameter which will show)

![](<.gitbook/assets/image (94).png>)

Lastly the pockets for the top and bottom and relief and indicator cuts for sawing off the lid are drawn in and then suitable toolpaths applied:

![](<.gitbook/assets/image (96).png>)

![](<.gitbook/assets/image (95).png>)

With the joint laid out, while it is specific to a given size of board (though it can easily be adapted to narrower boards by deleting finger pairs and adjusting the placement of the remaining elements) it is a simple matter to adjust the file for a given depth and width of box --- simply open the file and adjust the width to match the sum of the lengths of the parts.

The file is available at: [https://community.carbide3d.com/t/modular-joinery-system-for-blind-miter-fingerjoint-boxes/36161](https://community.carbide3d.com/t/modular-joinery-system-for-blind-miter-fingerjoint-boxes/36161)

To adjust it for a given box size, add the desired depth and width of the box to arrive at the width required for the stock. If using pre-cut pieces for the top and bottom, use that dimension, plus the stock thickness, plus some reasonable dimension for play. In this case, the pre-cut piece is a 200mm × 200mm piece of two-color HDPE, so 8.125" × 8.125" for box dimensions, and the stock area should be 16.25" wide:

![](<.gitbook/assets/image (104).png>)

![](<.gitbook/assets/image (106).png>)

Select everything and then go into Node Edit mode:

![](<.gitbook/assets/image (110).png>)

Drag-select all nodes associated with the right most joint:

![](<.gitbook/assets/image (111).png>)

and drag it to the far-right, so that it has the same relative position to the end of the stock as previously:

![](<.gitbook/assets/image (112).png>)

Draw in a rectangle which defines one of the two parts and is placed to match the stock:

![](<.gitbook/assets/image (100).png>)

Then select everything but this rectangle and again go into Node Edit mode and select the nodes associated with the middle two joints:

![](<.gitbook/assets/image (109).png>)

and drag them into position relative to the rectangle which defines where the two parts are cut away at:

![](<.gitbook/assets/image (101).png>)

Verify the positioning of everything and check with the 3D preview:

![](<.gitbook/assets/image (108).png>)

A much simpler option is to use a small endmill and to overcut the fingers with Tees which allows the joints to be square, which has the advantages of increasing long grain glue surface, and greatly simplifying the geometry, reducing the number of tools needed. With a rabbeted lid and bottom, it is still possible to have a fully mitered appearance, preserving the visible diagonal.

Drawing things in profile with the V endmill makes the starting point of the joint geometry quite obvious:

![](<.gitbook/assets/image (113) (1).png>)

which is easily modeled in 3D:

![](<.gitbook/assets/image (114) (1) (1).png>)

Then it is simply a matter of working up the depth which is being cut to, and drawing or modeling the fingers --- draw in appropriate geometry to model them, and add a square in the profile drawing to show to what depth things should be cut:

![](<.gitbook/assets/image (115).png>)

&#x20;Then assign a pocket toolpath to that depth:

![](<.gitbook/assets/image (117).png>)

then select the rounded rectangles for the V cut and start it at the bottom of the pocket:

![](<.gitbook/assets/image (118).png>)

which then previews as:

![](<.gitbook/assets/image (116) (1).png>)

