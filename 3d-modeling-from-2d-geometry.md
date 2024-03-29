---
description: 3D Modeling using Carbide Create Pro
---

# 3D Modeling from 2D Geometry

The optional Pro mode affords 3D modeling. The interface for this is quite straight-forward, but there are a number of options which quickly become combinatorially complex.

First, one has to have geometry which can be used as the basis for a 3D model --- the 2D geometry will define the edges of what will be modeled:

![](<.gitbook/assets/image (36).png>)

Switch to the Model tab and select geometry and then choose Add Shape:

![](<.gitbook/assets/image (43).png>)

which affords an interface for adding or subtracting a 3D area based on the selected geometry. One technique is to add the entirety of the stock:

![](<.gitbook/assets/image (53).png>)

So a Flat shape which has a height equal to the stock thickness which is Added (and one uses geometry which is the width and depth of the stock to arrive at:

![](<.gitbook/assets/image (119).png>)

Alternately, one can add only a median thickness which will afford a bit more flexibility, esp. if the design is to modeled proud of the surface:

![](<.gitbook/assets/image (35).png>)

With the surface which one wishes to work with defined, one can add or subtract shapes by selecting the geometry which defines them:

![](<.gitbook/assets/image (216).png>)

and setting parameters which will model as desired:

![](<.gitbook/assets/image (142).png>)

For any given shape, various parameters and options may be tried out --- the terminology used is typical of 3D modeling and may be easily looked up, or one may simply try variations until a desired result is achieved.

The possible shapes which may be added are:

* Round
* Angled
* Flat

When adding a shape the angle used for the model may be specified.

Additionally the height may be limited, or not, or scaled to a specified dimension.

Each component may be named, and the type of the merge used for 3D modeling specified:

* Add
* Subtract
* Min
* Max
* Multiply
* Equal

and lastly a Base Height may be specified which will result in the 3D modeling component having that height added beneath it if not present and calculated as starting at that base height.

Adding flat shapes is quite straight-forward:

![](<.gitbook/assets/image (76).png>)

![](<.gitbook/assets/image (232).png>)

Adding at an angle will attempt to angle the geometry up towards the specified height at the requested angle, modified by how the height is treated:

![](<.gitbook/assets/image (217).png>)

![](<.gitbook/assets/image (63).png>)

While subtraction simply reverses things:

![](<.gitbook/assets/image (48).png>)

![](<.gitbook/assets/image (19).png>)

Scaling height when adding can be useful to ensure that a particular elevation will be achieved by a given object:

![](<.gitbook/assets/image (32).png>)

![](<.gitbook/assets/image (24).png>)

Geometry may be modeled in 3D on top of existing objects:

![](<.gitbook/assets/image (150).png>)

![](<.gitbook/assets/image (29).png>)

Setting the Merge type to equal and the base height to where the top of the rounded form reaches will result in there being a level base for the text to be modeled from so that it isn't wrapped around the rounded form:

![](<.gitbook/assets/image (30).png>)

Similarly, one can subtract using the various modeling settings to arrive at:

![](<.gitbook/assets/image (17).png>)

![](<.gitbook/assets/image (283).png>)

![](<.gitbook/assets/image (154).png>)

Once one has a design completely modeled, one used 3D toolpaths to cut things out by selecting geometry to define where the cutting will be limited to, and applying a 3D Roughing and then one or more 3D Finishing toolpaths, usually using ball-nosed endmills in a progression of sizes from large to small.

For additional tutorials see:

* [https://community.carbide3d.com/t/starting-with-2-5-d-carving/15168/](https://community.carbide3d.com/t/starting-with-2-5-d-carving/15168/)
* [https://community.carbide3d.com/t/trial-ver-432-3d-carving-not-finding-much-info-other-than-a-star/16190](https://community.carbide3d.com/t/trial-ver-432-3d-carving-not-finding-much-info-other-than-a-star/16190)
* [https://community.carbide3d.com/t/vcarve-pro-wide-flutes/18942](https://community.carbide3d.com/t/vcarve-pro-wide-flutes/18942)
* [https://community.carbide3d.com/t/carbide-create-pro-3d-tutorial-small-game-board-piece/18456](https://community.carbide3d.com/t/carbide-create-pro-3d-tutorial-small-game-board-piece/18456)
* [https://community.carbide3d.com/t/3d-model-creating-a-ramp-object/22423](https://community.carbide3d.com/t/3d-model-creating-a-ramp-object/22423)
* [https://community.carbide3d.com/t/carbide-create-pro-wavy-flag/16974/15](https://community.carbide3d.com/t/carbide-create-pro-wavy-flag/16974/15)
* [https://community.carbide3d.com/t/modeling-a-bowl-in-carbide-create/30993](https://community.carbide3d.com/t/modeling-a-bowl-in-carbide-create/30993)
