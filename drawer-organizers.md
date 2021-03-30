---
description: Flexible organization setup
---

# Drawer Organizers

Drawer organization is a typical aspect of homes, especially the kitchen. Customization options and parameters include the dimensions of the drawer, the number of dividers along each axis, and the dimensions/spacing of each, as well as the thickness of the stock.

To simplify things, the interface will make certain assumptions:

* no sides or front
* spacing will be evenly divided amongst the dividers \(but specific dividers may be disabled, or set to start from right or rear\)

Programmatically this will be done by the following possible values: 

Position

* 0 --- divider is disabled
* 1--9 --- divider will start at that numbered position

Length

* positive values will have the divider starting to the left/in front of that position and continuing to the right or rear
* negative values will have the divider starting to the right of/behind that position and continuing left or to the front

In order to do this we need a module which has an input for the maximum possible number of positions:

![Draw divider module](.gitbook/assets/image%20%2861%29.png)

Then, based on the logic of which is the highest numbered position which has a non-zero number the distances are apportioned evenly and calculated. First create variables for each divider position:

![Drawer divider variables](.gitbook/assets/image%20%2863%29.png)

To make checking the position easier, draw in a surround:

![Drawer divider surround](.gitbook/assets/image%20%2862%29.png)







