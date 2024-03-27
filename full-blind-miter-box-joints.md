---
description: One joint, two levels, three tools
---

# Full Blind Miter Box Joints

Adding a third tool, a large V endmill, and using it to cut a full blind miter joint at the end of the joints simplifies the geometry quite a bit, and with modern adhesives, still allows for a very strong joint. Layout is much the same, only simpler, as is the geometry and alignments, which are all more forgiving.

One concern with doing this is that the thickness to which even a 1/2" tool will cut is strictly limited, being of course equal to half the diameter:

<figure><img src=".gitbook/assets/image (179).png" alt=""><figcaption></figcaption></figure>

While in theory one could just source an arbitrarily large tool to brute force this, the reality of available tooling and the trim routers which are used as spindles on many less expensive CNC machines makes this untenable. Using larger tooling also increases the area lost to such features at the corners, including increasing the waste area around the parts. Fortunately, the geometry of the cut makes for an obvious solution which will take advantage of the tooling which one is using for the narrow V cut along the outer edge of the joint.

Positioning the tool to have it make the cut at the upper edge of the narrow V cut increases the possible thickness by that height:

<figure><img src=".gitbook/assets/image (115).png" alt=""><figcaption></figcaption></figure>

The further consideration is that the fingers should be relieved to a depth equal to or greater than the radius of the narrow tool, matched to how close to the sides fo the joint the recesses are cut, so as to eliminate the fit interference of the fingers against the rounded ends of the pockets for them. Another option would be round the top of the positive joinery elements using a suitable tool, but that would add another tool change.

The most expedient option seems to be just two passes, one at the bottom of the stock, the other at the mid-point:

<figure><img src=".gitbook/assets/image (93).png" alt=""><figcaption></figcaption></figure>

Which has the advantage of having an overlap (if tool cut depth is greater than half the stock thickness), and being invariant of tool geometry (with the proviso that thickness of the stock must be equal to or less than twice the depth to which the large V tool can cut).

A further consideration is the width of the central channel for the V tool and the size of the tool used to cut it. Probably the simplest option is to use a smaller square endmill than the V tool.

For more on this see:

[https://community.carbide3d.com/t/full-blind-finger-joints-in-carbide-create/53329](https://community.carbide3d.com/t/full-blind-finger-joints-in-carbide-create/53329)





