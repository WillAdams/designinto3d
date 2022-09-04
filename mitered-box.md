---
description: >-
  Modern adhesives allow for a box to be cut using just miters and glued and
  folded.
---

# Mitered Box

The simplest way to cut a box shape is to use a suitable sheet good and simply cut miters into it --- modern adhesives are able to make this a strong joint and most CAM tools allow for it to be drawn up and modeled with just a few lines.

Initial discussion at: [https://community.carbide3d.com/t/design-into-3d-miter-box/13813](https://community.carbide3d.com/t/design-into-3d-miter-box/13813) but Carbide Create gaining the ability to generate a 3D preview of a V endmill assigned to a contour toolpath simplifies this greatly.

As with all boxes, they are defined by their height, width, and depth, with the stock thickness determining the interior dimensions and the specifics of joinery. Stock width and length will be the box depth or box width plus twice the height:

* Height
* Width
* Depth
* Stock Thickness
* Stock Width == Box Depth + Box Height \* 2
* Stock Length == Box Width + Box Height \* 2

The design is easily drawn up using straight lines:

<figure><img src=".gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

which would then have no-offset Contour toolpaths assigned using a 90 degree V endmill.

Surround the parts with a rectangle, and geometry offset from it by endmill diameter plus 10%:

<figure><img src=".gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

Alternately, to make workholding easier, only the edges of the parts strictly need to be cut out:

<figure><img src=".gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

Only two toolpaths are necessary, a no-offset Contour with a V endmill:

<figure><img src=".gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

(which is done to stock thickness (t) less an onion skin (0.015"))

and pockets to cut the parts free:

<figure><img src=".gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

As the 3D preview shows, workholding may be done at the corners, depending on the onion-skin of the V endmill cut to hold things in place:

<figure><img src=".gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>
