---
description: Cutting a part out using 3D modeling.
---

# Further Toolpath Details

Once a part has been designed, it is necessary to cut it out. The implication here is obvious, rather than designing the part, what is actually needed is the toolpath which guides the endmill around and/or over and/or through the part so as to result in the specified shape.

As noted before, the best practice is to design the part in the orientation which is best suited to cutting ― it may then be rotated and/or moved into position. A further consideration is that the parts should be arranged relative to a block which represents the stock. This means that in modeling, rather than building up the shape directly, one should instead create a piece of stock the desired size and remove from it.

Doing this in Block/OpenSCAD is straight-forward ― begin by modeling the stock, then create a series of modules which allow one to mimic the placement and movement of endmills and subtract them from the stock shape. Each part may then be placed either for 3D previewing, or production using suitable options.

