---
description: 3D Modeling using Carbide Create Pro
---

# 3D Modeling

The optional Pro mode affords 3D modeling. The interface for this is quite straight-forward, but there are a number of options which quickly become combinatorially complex.

First, one has to have geometry which can be used as the basis for a 3D model --- the 2D geometry will define the edges of what will be modeled:

![](<.gitbook/assets/image (128).png>)

Switch to the Model tab and select geometry and then choose Add Shape:

![](<.gitbook/assets/image (118).png>)

which affords an interface for adding or subtracting a 3D area based on the selected geometry. One technique is to add the entirety of the stock:

![](<.gitbook/assets/image (122).png>)

So a Flat shape which has a height equal to the stock thickness which is Added (and one uses geometry which is the width and depth of the stock to arrive at:

![](<.gitbook/assets/image (138).png>)

Alternately, one can add only a median thickness which will afford a bit more flexibility, esp. if the design is to modeled proud of the surface:

![](<.gitbook/assets/image (117).png>)

With the surface which one wishes to work with defined, one can add or subtract shapes by selecting the geometry which defines them:

![](<.gitbook/assets/image (121).png>)

and setting parameters which will model as desired:

![](<.gitbook/assets/image (124).png>)

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

