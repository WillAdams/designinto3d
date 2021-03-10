---
description: Drawing in 2 dimensions to make 3 dimensional parts
---

# 2D Drawing

As noted previously, before one can make a part, one must define the geometry of the design. This is done using classic geometric constructs, and possibly curves defined mathematically \(but usually drawn up in a CAD or Bézier curve drawing program\). We will use Carbide Create as a specific example \(freely available from: [https://carbide3d.com/carbidecreate/](https://carbide3d.com/carbidecreate/)\), but the concepts would apply to any CAD or vector drawing program and will be explored first.

![Carbide Create interface.](.gitbook/assets/carbide_create_interface%20%282%29.png)

As with most drawing tools, there are menus for commands or different program functions/states, a palette of drawing tools, and a work area. 

## Points

The most basic geometric construct as noted by Euclid in [_Elements_](https://mathcs.clarku.edu/~djoyce/java/elements/elements.html)_:_ [_Book I_](https://mathcs.clarku.edu/~djoyce/java/elements/bookI/bookI.html)_:_ [_Definition 1_](https://mathcs.clarku.edu/~djoyce/java/elements/bookI/defI1.html) is a point in coordinate space \(most CAD tools and vector drawing applications use Cartesian coordinates\) ― some CAM tools allow one to assign a drilling operation at a point, but many vector editors disallow a point as an individual stand-alone entity, instead, they are used as a building block for everything else. Carbide Create does not allow the creation of single points, so one would create a circle to define the perimeter of the circle which one wished to machine \(see below\).

Points of course will be used to define the Cartesian X, Y coordinates of all geometry in the design. Toolpaths will then allow specifying Z, extending this into the 3rd dimension. Note that in some circumstances the term “Node” will be used for a point.

## Lines

Straight lines are a fundamental building block of vector drawing and are of course defined as the shortest distance between two points \(Euclid’s _Elements: Book I:_ [_Definitions 2–5_](https://mathcs.clarku.edu/~djoyce/java/elements/bookI/bookI.html#defs)\). Some CAM tools \(including Carbide Create\) will allow one to assign various toolpaths to lines, and if not directly on the line, the offset will be determined by which point is the origin and which is the final point \(path direction\). Carbide Create allows one to draw lines as unclosed paths, by choosing either the Polyline \(or Curve\) tool:

![Carbide Create Polyline Tool.](.gitbook/assets/carbide_create_screengrab_polyline_hl%20%284%29.png)

clicking at the beginning and end points:

![Carbide Create drawing line with Polyline tool.](.gitbook/assets/carbide_create_interface_create_polyline%20%281%29.png)

and then clicking on "Done". Note that open lines in Carbide Create will be indicated by being magenta when not selected, as opposed to the black of closed paths. The current selection is drawn in orange.

Open polylines \(or curves, see below\) are not typically used in Carbide Create, instead one will usually re-work closed paths so that they have suitable geometry. There are commands for editing polylines when they are selected in addition to the normal transforms \(see below\) ― since the edits possible are a subset of those for the Curve tool, and the editing interface makes it possible to convert a polyline into a curve, this is discussed in the Curve tool section below.

Lines will be used to define Rectangles \(which may be squares\) and regular Polygons as described below.

## Arcs

Many CAD programs will allow the definition of arcs which are easily drawn and may be specified in several ways — an origin point, end point, and a point of rotation are typical. Carbide Create does not have an arc tool, but they may be made using Boolean operations as parts of circles and geometry based on circles \(segments and so forth\), as fillets when rounding the corners of a rectangle \(see below\), or drawn using the Curve tool \(see below\).

## Polylines

Polylines are made up of multiple points describing lines and are differentiated by being open or closed. Note that there are multiple ways to represent a given figure, and the capabilities and interface options will be different based on how it was created, and if it has been edited. For example, a square may have corner options if drawn using the Rectangle tool and may be changed to a rectangle by altering one dimension parameter or other, but if drawn with the regular Polygon tool, may be changed into another polygon or resized proportionally, and if drawn using the Polyline or Curve tool may only be resized proportionally or node-edited \(which to a degree are possible with the other creation options\).

### Open Paths

As noted above, toolpaths may be assigned to open paths, and the directionality will determine any offset. Open paths are necessarily limited in the toolpaths which may be assigned, and it will typically not be possible to assign any but the most basic of operations to them. In Carbide Create, open paths may be converted to closed by using the Join command \(see Curve Editing below\) and it is also possible to combine two \(or more\) open paths drawn in Carbide Create into a single path, open or closed. 

### Closed Paths 

Closed paths meet back at the point of origin and open up additional operations in CAM tools. In Euclid’s _Elements: Book I:_ [_Definition 13–14_ ](https://mathcs.clarku.edu/~djoyce/java/elements/bookI/defI13.html)they are described as a defined boundary comprising a figure. They may be made up of lines, arcs, curves, or some combination. Often tools will have especial support for regular polygons, allowing their creation or definition quickly and efficiently. Carbide Create has specific support for Circles, Rectangles \(which may be squares\), and Regular Polygons.

#### Circles

Circles are defined in Euclid’s _Elements: Book I:_ [_Definition 15–17_](https://mathcs.clarku.edu/~djoyce/java/elements/bookI/defI15.html) __as a plane figure with one line equidistant from a point, _c.f._, [_Book III_](https://mathcs.clarku.edu/~djoyce/java/elements/bookIII/bookIII.html). In Carbide Create one draws circles from the inside out, clicking first at the center point, then on a point at the perimeter to define the radius \(and diameter\):

![Carbide Create drawing a circle.](.gitbook/assets/carbide_create_interface_create_circle%20%282%29.png)

Note that the **Done** button allows one to cancel out of the circle drawing mode.

Circles are defined as four Bézier curves which is necessarily an approximation of a perfect circle, but one with an error so small as to not matter for machining purposes.

#### Rectangles and Squares

Named as quadrilaterals in Euclid’s _Elements: Book I:_ [_Definition 19_](https://mathcs.clarku.edu/~djoyce/java/elements/bookI/defI19.html), rectangles have a specific tool for their creation, squares may be defined by making height and width equal, and in Carbide Create they have a corner feature which other shapes do not. As circles are, they are drawn from the inside out in Carbide Create:

![Carbide Create drawing a rectangle.](.gitbook/assets/carbide_create_interface_create_rectangle%20%281%29.png)

Since Carbide Create draws from center out, shapes are often twice the desired dimensions, in such instances they may be easily scaled to half their size \(this applies to other shapes and is often useful/expedient\) so as to have them at the intended size.

### Polygons

Drawing programs often have support for regular polygons, as does Carbide Create. As with other objects, Polygons are drawn from the center point out:

![Carbide Create drawing a hexagon.](.gitbook/assets/carbide_create_interface_create_polygon.png)

Once drawn, they may be adjusted in their dimensions, and for their number of sides, see below.

### Parameters

Once shapes have been drawn, they may be selected and changed or modified. The most basic change is simply modifying their dimensions, but other properties and features may be available.

#### Circle Parameters

For a circle, the size parameter adjustment may be done in terms of its overall size using the **Resize** tool \(either Width or Height, only one may be adjusted, the other will be forced to match\), or **Radius**:

![Carbide Create modifying circle parameters.](.gitbook/assets/carbide_create_screengrab_circle_parameters%20%281%29.png)

#### Rectangle Parameters

Rectangles may also be modified in their dimensions, but one is not limited to a regular square, Width and/or Height may be specified separately:

![Carbide Create modifying rectangle parameters.](.gitbook/assets/carbide_create_interface_parameters_rectangle%20%283%29.png)

Note that in addition to the dimensions, one may change the shaping/appearance of corners. The possible options are:

![Carbide Create corner treatments.](.gitbook/assets/carbidecreate_corner_treatments.png)

* Square \(the default shown above\)
* Fillet \(rounded corners which allow applying an arc to a given corner\)
* Chamfer \(45 degree angles\)
* Flipped fillet \(quarter circles removed from corners\)
* Dogbone \(placing a circle up against the corner so as to ensure that after cutting with a round endmill a part with a right angle corner will still fit\)
* Tee \(placing a semicircle at a corner to ensure that a part with right angle corners will still fit ― note that orientation may not be specified, but by adding the feature, then rotating the part this may be controlled\)

Once a corner treatment is specified, one may set its dimension in terms of the radius/diameter:

![Carbide Create modifying Rectangle corner parameters.](.gitbook/assets/carbide_create_interface_rectangle_fillet_parameters%20%282%29.png)

#### Polygon Parameters

Polygons may be adjusted for Width or Height \(since only regular polygons are supported, only one measurement may be specified, the other will be forced to the correct dimension\) and number of sides:

![Carbide Create modifying Polygon parameters.](.gitbook/assets/carbide_create_interface_polygon_parameters%20%284%29.png)

## Transformations

Geometry may be adjusted in a number of ways:

* Moved to a different location in the drawing area
* Resized or scaled to a different size/proportion
* Rotated
* Flipped along an axis \(Carbide Create affords tools for horizontal and vertical\)
* Aligned, either to another piece of geometry or the defined Stock

Another option which drawing programs may afford is offsetting ― this is especially important for Carbide Create since it allows one to adjust the geometry in terms of the radius or diameter of the endmill \(see below\).

### Move

When selecting geometry in Carbide Create and selecting **Move**, the X and Y coordinates may be entered, and the reference point selected from the proxy point \(indicated by the green highlighted circle\), and will move to that point when the Return/Enter is pressed:

![Carbide Create Move transform.](.gitbook/assets/carbide_create_interface_transform_move%20%281%29.png)

### Resize

In addition to moving, geometry may also be transformed. Using the numeric interface selections may be scaled symmetrically using the hollow square drag handles at the corners ― midpoints of the selection marquee afford asymmetric scaling by dragging instead \(this is a simple way to create an ellipse/oval\):

![](.gitbook/assets/carbide_create_interface_transform_scale%20%281%29.png)

### Rotate

Objects may be rotated. This is often useful for decorative designs, and may be required to control part orientation when cutting or doing mechanical design. Note that for some objects it may be better to alter their size rather than rotating them in Carbide Create.

### Flip

Objects may be flipped \(mirrored\) horizontally or vertically. Useful for decorative designs, it also allows \(for instance\) the creation of reversed geometry for creating stamps or printing blocks or creating a mirror of a part for cutting it as an inlay.

### Align

Most, if not all CAD and design tools allow an option for aligning one or more objects. Typically if only one object is selected, the alignment is against the drawing area, in the case of Carbide Create, against the Stock. Alignment affords precision, and control, especially when one is using Rotation.

### Offset Path

Geometry may be selected and offset, either to the inside or outside:

![Carbide Create offset interface options](.gitbook/assets/carbide_create_interface_offsetpath%20%282%29.png)

When offsetting paths to the outside in Carbide Create, corners are rounded off to match the distance specified as a radius. This allows one to instantiate as geometry the path which would be assigned to an endmill when cutting out a shape. If sharp corners are desired either draw the design at the largest possible size and inset only, or export to an SVG, do the offsetting operation in a 3rd party tool such as Inkscape, and then reimport, or redraw the geometry.

### Boolean Operations

Booleans allow for the instantiation of geometry from existing geometry. Named for the British Mathematician George Boole: [https://www.britannica.com/biography/George-Boole](https://www.britannica.com/biography/George-Boole), they result in new figures based on a logical interaction of two or more figures, so the interface for them only appears when two or more objects are selected \(the green indicates the geometry which will be produced by the operation, the black what is removed\):

![Carbide Create Boolean options.](.gitbook/assets/carbide_create_interface_boolean%20%281%29.png)

Depending on the selection, Carbide Create affords the following Boolean operations:

* Union ― the current selection \(two or more objects\) will be added together, creating a new object which is the outermost perimeter of the selection
* Intersection ― only available when two objects are selected, the new object will be that area included within both objects
* Subtraction ― the key object \(indicated by a dashed highlight\) will be removed from each of the other object\(s\) in the selection

Note that in most programs, the selection is modified, so if the original geometry will be needed after, it may be necessary that the objects be duplicated and dragged back into alignment with the originals.

If a given operation does not have the desired result, undoing it in Carbide Create will change which object is the current key object \(indicated by a dashed highlight\) ― reattempting the operation will then do so based on that new aspect of the selection with different results than previously.

## Curves 

Curves are available in most vector drawing programs, and when present may be defined in several ways. 

### Bézier Curves 

The most common is Bézier curves which are defined by an on-curve point \(the origin\), a matching off-curve point, and an additional off-curve point paired with the ultimate \(ending\) on-curve point. Carbide Create uses Bézier curves in its Curve tool. Note that points are termed as Nodes in the various Curve tool options.

To create a curve, select that tool, then click or click-drag where one wants on-curve points \(clicking creates sharp nodes, click-dragging creates smooth nodes, with the click placing the on-curve node, and the drag-release determining the position of the off-curve node ― either may be changed to the other, see below\):

![Carbide Create drawing curve.](.gitbook/assets/carbide_create_interface_create_curve.png)

#### Open or Closed Paths

Once a Curve \(or Polyline\) is created it may be either open \(indicated by being magenta when not selected\), or closed \(black\). Open paths may be closed using the Join command:

![Carbide Create closing curve using Join command. ](.gitbook/assets/carbide_create_interface_join_curve%20%281%29.png)

Note that the beginning and ending nodes will be connected as directly as possible:

![Carbide Create curve closed using Join command.](.gitbook/assets/carbide_create_interface_join_curve_after.png)

and it may be necessary to adjust the curve if the path crosses itself.

#### Principles for Bézier Curves

Bézier Curves should be drawn following some basic principles:

* on-curve nodes should be at extrema \(north/south \(top/bottom\) or east/west \(left/right\)\) and at points of inflection \(where a shape changes direction, such as at the middle of an _S_ curve\)
* curves are smoothest when off-curve nodes follow the “Rule of 30” and are approximately one-third \(~30 percent\) of the distance towards the next on-curve node

#### Node Edit Mode

The underlying points of geometry may be modified by selecting it and choosing Node Edit Mode:

![Carbide Create Node Edit Mode](.gitbook/assets/carbide_create_interface_node_edit_mode.png)

As noted above, geometry is made up of lines and/or curves which are bounded by on-path nodes, and for curves, have a pair of off-path nodes which determine how the curve is drawn.

When in Node Edit Mode it is possible to right-click and:

* add an on-path node
* delete an on-path node
* toggle a node from smooth to sharp and vice-versa

Off-path nodes may be dragged to reshape paths, and by holding the Alt \(Option\) key, dragged without affecting the other off-path node for the associated on-path node creating a sharp node and asymmetry.

#### Drawing Tutorials

A very basic drawing task is to draw an oval. Originally this tutorial was available at: [http://community.carbide3d.com/t/lets-draw-an-ellipse-with-new-users/4194](http://community.carbide3d.com/t/lets-draw-an-ellipse-with-new-users/4194) — and is provided here in an updated form.

Start by launching Carbide Create — in Job Setup \(gear icon\) set the width of the drawing area to 20", the height to 15", and go into Job Setup \| Document background \| Edit Ensure the grid spacing is 0.50. Download the following file:

![](.gitbook/assets/cc_diamond.png)

Placing it on the background layer scaled so that it fills the entire drawing area \(0.557 should work\). Ensure that Snap to Grid is enabled.

Select the Curve tool and click on each of the four points of the placed image, clicking again on the first to close the path.

Download and place the image below on the background scaled as before:

![](.gitbook/assets/cc_ellipse.png)

Select the path and go into Node Edit Mode and right-click on each node and select "Toggle Smooth" \(or press the "s" key\) and drag the off-curve nodes to match the positioning of the background image.

The following additional drawing tutorials are available:

* [https://community.carbide3d.com/t/lets-make-a-b-for-anyone/14223](https://community.carbide3d.com/t/lets-make-a-b-for-anyone/14223) — drawing more complex forms with the Curve tool
* [https://community.carbide3d.com/t/how-to-draw-a-compass-rose/16170](https://community.carbide3d.com/t/how-to-draw-a-compass-rose/16170https://community.carbide3d.com/t/how-to-draw-a-star-carbide-create/16022)
* [https://community.carbide3d.com/t/how-to-draw-a-star-carbide-create/16022](https://community.carbide3d.com/t/how-to-draw-a-compass-rose/16170https://community.carbide3d.com/t/how-to-draw-a-star-carbide-create/16022)

### Quadratic B-Splines

A curve which alternates on-curve and off-curve nodes, B-Splines are used for TrueType fonts, since their calculation is efficiently done, but are not used in typical CAD or Bézier curve drawing applications. Note that when TrueType fonts are converted to paths, conversion from B-Splines to Bézier curves may result in odd node placement.

## Geometry

When drawing and modeling it is often necessary to place parts relative to the original positioning based on a distance and possibly rotation determined by the dimensions of the parts. Geometry and trigonometry allow the calculation of such positioning, usually in terms of right triangles, or chords for elements based on circles or segments of circles. 

There are of course several different sorts of triangles depending on the specifics of their angles and the length of their sides. 

By length:

* scalene ― all sides are different lengths
* isosceles ― two sides are the same length
* equilateral ― all three sides are the same length

By angles:

* right triangle ― one angle is 90 degrees \(may also be an isosceles or scalene triangle\)
* oblique ― no angle is equal to 90 degrees
* obtuse ― one angle is greater than 90 degrees
* acute ― all angles are less than 90 degrees

Depending on the angles and the orientation of a given triangle, various labeling may be appropriate. 

For specific triangles, different formulae apply. 

We begin of course with the Pythagorean theorem:

$$
a^2 + b^2 = c^2
$$

which allows us to determine the length of one side of a right triangle, given the lengths of the other two sides.

$$
c = \sqrt{a^2 + b^2}
$$

$$
b = \sqrt{c^2 - a^2}
$$

$$
a = \sqrt{c^2 - b^2}
$$

All the possible formulae for calculating the lengths of the sides of a right triangle are:

![Formulae for calculating lengths of triangle sides.](.gitbook/assets/triangle-sides.png)

Similarly, the angles of a right triangle may be calculated by:

![Formulae for calculating the angles of a right triangle.](.gitbook/assets/triangle-angles.png)

Projects involving circles are usually calculated in terms of chords, radius, and the height of the chord segment.

![Formulae for calculating radius, length or chord, and height of chord segment.](.gitbook/assets/circle-chord.png)

## Resources

For further information on Carbide Create please see:

* [http://docs.carbide3d.com/assembly/carbidecreate/userguide/](http://docs.carbide3d.com/assembly/carbidecreate/userguide/) \(a web page\)
* [http://carbide3d.com/carbidecreate/video/](http://carbide3d.com/carbidecreate/video/) \(a collection of tutorial videos\)
* [http://community.carbide3d.com/c/software/carbide-create](http://community.carbide3d.com/c/software/carbide-create) \(a community forum\)
* [https://wiki.shapeoko.com/index.php/Carbide\_Create](https://wiki.shapeoko.com/index.php/Carbide_Create) \(a wiki page\)

![](.gitbook/assets/carbide3d_create_motion_keyboard_shortcuts.png)

* [Carbide3D\_create\_motion\_keyboard\_shortcuts.pdf](https://community.carbide3d.com/uploads/default/original/3X/1/1/11767141a1e1d62246952219ec915572aae4c699.pdf) \(available at: [https://community.carbide3d.com/t/keyboard-cheat-sheet-for-carbide-create-and-motion/7839](https://community.carbide3d.com/t/keyboard-cheat-sheet-for-carbide-create-and-motion/7839)\)

## Third Dimensional Shapes

Extending all of these into 3 dimensions becomes more complex with each additional element, each of which complicates the mathematics. Up through arcs and regular curves, these are usually manageable, as is expressed in constructive solid geometry \(CSG\), and OpenSCAD \(and its Blockly derivative BlockSCAD\) is essentially a scripting front-end for this. Extending arbitrary curves into 3 dimensional space involves complex geometric calculations which are the domain of 3 dimensional modeling tools such as Blender and various commercial programs. Fortunately, the regular polygons and extruded shapes of CSG afford one a very wide array of design options.

