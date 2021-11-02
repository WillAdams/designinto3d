---
description: Drawing in 2 dimensions to make 3 dimensional parts
---

# 2D Drawing

As noted previously, before one can make a part, one must define the geometry of the design. This is done using classic geometric constructs, and possibly curves defined mathematically (but usually drawn up in a CAD or Bézier curve drawing program). We will use Carbide Create as a specific example (freely available from: [https://carbide3d.com/carbidecreate/](https://carbide3d.com/carbidecreate/)), but the concepts would apply to any CAD or vector drawing program and will be explored first.

![Carbide Create interface.](<.gitbook/assets/carbide\_create\_interface (2).png>)

As with most drawing tools, there are menus for commands or different program functions/states, a palette of tools, and a work area.&#x20;

## Points

The most basic geometric construct as noted by Euclid in [_Elements_](https://mathcs.clarku.edu/\~djoyce/java/elements/elements.html)_: _[_Book I_](https://mathcs.clarku.edu/\~djoyce/java/elements/bookI/bookI.html)_: _[_Definition 1_](https://mathcs.clarku.edu/\~djoyce/java/elements/bookI/defI1.html) is a point in coordinate space (most CAD tools and vector drawing applications use Cartesian coordinates) ― some CAM tools allow one to assign a drilling operation at a point, but many vector editors disallow a point as an individual stand-alone entity, instead, they are used as a building block for everything else. Carbide Create does not allow the creation of single points, so one would create a circle to define the perimeter of a hole which one wished to machine, or the center of which would define the point at which one wished to drill (see below).

Points of course will be used to define the Cartesian X, Y coordinates of all geometry in the design. Toolpaths will then allow specifying Z, extending this into the 3rd dimension. Note that in some circumstances the term “Node” will be used for a point.

## Lines

Straight lines are a fundamental building block of vector drawing and are of course defined as the shortest distance between two points (Euclid’s _Elements: Book I: _[_Definitions 2–5_](https://mathcs.clarku.edu/\~djoyce/java/elements/bookI/bookI.html#defs)). Some CAM tools (including Carbide Create) will allow one to assign various toolpaths to lines, and if not directly on the line, the offset will be determined by which point is the origin and which is the final point (which is to say, the path direction). Carbide Create allows one to draw lines as unclosed paths, by choosing either the Polyline (or Curve) tool:

![Carbide Create Polyline Tool.](<.gitbook/assets/carbide\_create\_screengrab\_polyline\_hl (4).png>)

clicking at the beginning (as well as if desired intermediary points) and end points:

![Carbide Create drawing line with Polyline tool.](<.gitbook/assets/carbide\_create\_interface\_create\_polyline (1).png>)

and then clicking on **Done**. Note that open lines on the default layer in Carbide Create will be indicated by being magenta when not selected, as opposed to the black of closed paths. The current selection is drawn in orange (for objects on the current layer).

Open polylines (or curves, see below) are not typically used in Carbide Create, instead one will usually re-work closed paths so that they have suitable geometry. There are commands for editing polylines when they are selected in addition to the normal transforms (see below) ― since the edits possible are a subset of those for the Curve tool, and the editing interface makes it possible to convert a polyline into a curve, this is discussed in the **Curve **tool section below.

Lines will be used to define Rectangles (which may be squares) and regular Polygons as described below.

## Arcs

Many CAD programs will allow the definition of arcs which are easily drawn and may be specified in several ways — an origin point, end point, and a point of rotation are typical. Carbide Create does not have an arc tool, but they may be made using Boolean operations as parts of circles and geometry based on circles (segments and so forth), as fillets when rounding the corners of a rectangle (see below), or drawn using the Curve tool (see below), though since they are represented as either curves or polylines will necessarily be approximations of an actual arc.

## Polylines

Polylines are made up of multiple points describing lines and are differentiated by being open or closed. Note that there are multiple ways to represent a given figure, and the capabilities and interface options will be different based on how it was created, and if it has been edited. For example, a square may have corner options if drawn using the **Rectangle **tool and may be changed to a rectangle by altering one dimension parameter or other, but if drawn with the regular **Polygon **tool, may be changed into another polygon or resized proportionally, and if drawn using the **Polyline **or **Curve **tool may only be resized proportionally or node-edited (which to a degree are possible with the other creation options).

### Open Paths

As noted above, toolpaths may be assigned to open paths, and the directionality will determine any offset if needed for a toolpath. Open paths are necessarily limited in the toolpaths which may be assigned, and it will typically not be possible to assign any but the most basic of operations to them. In Carbide Create, open paths may be converted to closed by using the Join Vectors command (see Curve Editing below) and it is also possible to combine two (or more) open paths drawn in Carbide Create into a single path, open or closed.&#x20;

Note that in build 527 Carbide Create gained a feature for adding all open paths to the current selection: [https://blog.carbide3d.com/2021/carbide-create-527/](https://blog.carbide3d.com/2021/carbide-create-527/)&#x20;

Edit | Select... | Select Open Vectors

### Closed Paths&#x20;

Closed paths meet back at the point of origin and open up additional operations in CAM tools. In Euclid’s _Elements: Book I: _[_Definition 13–14_ ](https://mathcs.clarku.edu/\~djoyce/java/elements/bookI/defI13.html)they are described as a defined boundary comprising a figure. They may be made up of lines, arcs, curves, or some combination. Often tools will have especial support for regular polygons, allowing their creation or definition quickly and efficiently. Carbide Create has specific support for **Circles**, **Rectangles **(which may be squares), and Regular **Polygons**.

#### Circles

Circles are defined in Euclid’s _Elements: Book I: _[_Definition 15–17_](https://mathcs.clarku.edu/\~djoyce/java/elements/bookI/defI15.html)_ _as a plane figure with one line equidistant from a point, _c.f._, [_Book III_](https://mathcs.clarku.edu/\~djoyce/java/elements/bookIII/bookIII.html). In Carbide Create one draws circles from the inside out, clicking first at the center point, then on a point at the perimeter to define the radius (and diameter):

![Carbide Create drawing a circle.](<.gitbook/assets/carbide\_create\_interface\_create\_circle (2).png>)

Note that the **Done** button allows one to cancel out of the circle drawing mode.

In Carbide Create, circles are defined as four Bézier curves (as opposed to using arcs) which is necessarily an approximation of a perfect circle, but one with an error so small as to not matter for machining purposes. Researching the math involved in this differentiation is left as an exercise for the interested reader.

Note that in build 527 Carbide Create gained a feature for adding all circles to the current selection: [https://blog.carbide3d.com/2021/carbide-create-527/](https://blog.carbide3d.com/2021/carbide-create-527/)&#x20;

Edit | Select... | Select Circles

![Carbide Create dialog for Select Circles ](<.gitbook/assets/image (73).png>)

One may select the minimum and maximum diameter for adding circles to the current selection which will include circles drawn with the native circle tool, circles drawn as Bézier curves, and polylines which approximate a circle.&#x20;

#### Rectangles and Squares

Named as quadrilaterals in Euclid’s _Elements: Book I: _[_Definition 19_](https://mathcs.clarku.edu/\~djoyce/java/elements/bookI/defI19.html), rectangles have a specific tool for their creation; squares may be defined by making height and width equal, and in Carbide Create they have a corner feature which other shapes do not. As circles are, they are drawn from the inside out in Carbide Create:

![Carbide Create drawing a rectangle.](<.gitbook/assets/carbide\_create\_interface\_create\_rectangle (1).png>)

Since Carbide Create draws from center out, shapes are often twice the desired dimensions, in such instances they may be easily scaled to half their size (this applies to other shapes and is often useful/expedient) so as to have them at the desired size.

### Polygons

Drawing programs often have support for regular polygons, as does Carbide Create. As with other objects in Carbide Create, Polygons are drawn from the center point out:

![Carbide Create drawing a hexagon.](<.gitbook/assets/carbide\_create\_interface\_create\_polygon (1).png>)

Once drawn, they may be adjusted in their dimensions, and for their number of sides, see below.

### Parameters

Once shapes have been drawn, they may be selected and changed or modified. The most basic change is simply modifying their dimensions, but other properties and features may be available.

#### Circle Parameters

For a circle, the size parameter adjustment may be done in terms of its overall size using the **Resize **tool (either **Width **or **Height**, only one may be adjusted, the other will be forced to match), or **Radius**:

![Carbide Create modifying circle parameters.](<.gitbook/assets/carbide\_create\_screengrab\_circle\_parameters (1).png>)

#### Rectangle Parameters

Rectangles may also be modified in their dimensions, but one is not limited to a regular square, Width and/or Height may be specified separately:

![Carbide Create modifying rectangle parameters.](<.gitbook/assets/carbide\_create\_interface\_parameters\_rectangle (3).png>)

Note that in addition to the dimensions, one may change the shaping/appearance of corners. The possible options are:

![Carbide Create corner treatments.](.gitbook/assets/carbidecreate\_corner\_treatments.png)

* _Square _(the default shown above)
* _Fillet_ (rounded corners which allow applying an arc to a given corner)
* _Chamfer _(45 degree angles)
* _Flipped fillet_ (quarter circles removed from corners)
* _Dogbone _(placing a circle up against the corner so as to ensure that after cutting with a round endmill a part with a right angle corner will still fit)
* _Tee _(placing a semicircle at a corner to ensure that a part with right angle corners will still fit ― note that orientation may not be specified, but by adding the feature, then rotating the part, this may be controlled)

Once a corner treatment is specified, one may set its dimension in terms of the radius/diameter/distance from the corner:

![Carbide Create modifying Rectangle corner parameters.](<.gitbook/assets/carbide\_create\_interface\_rectangle\_fillet\_parameters (2).png>)

#### Polygon Parameters

Polygons may be adjusted for Radius (since only regular polygons are supported, only one measurement need be specified) and number of sides:

![Carbide Create modifying Polygon parameters.](<.gitbook/assets/carbide\_create\_interface\_polygon\_parameters (4).png>)

## Transformations

Geometry may be adjusted in a number of ways:

* Moved to a different location in the drawing area
* Resized or scaled to a different size/proportion
* Rotated
* Flipped along an axis (Carbide Create affords tools for horizontal and vertical)
* Aligned, either to another piece of geometry or the defined Stock

Another option which drawing programs may afford is offsetting ― this is especially important for Carbide Create since it allows one to adjust the geometry in terms of the radius or diameter of the endmill (see below).

### Move

When selecting geometry in Carbide Create and selecting **Move**, the X and Y coordinates may be entered, and the reference point selected from the proxy point (indicated by the highlighted/selected circle), and will move the object so the referred corner is at that point when the Apply button is pressed:

![Carbide Create Move transform.](<.gitbook/assets/carbide\_create\_interface\_transform\_move (1).png>)

### Resize

In addition to moving, geometry may also be altered in size. Selections may be scaled symmetrically using the hollow square drag handles at the corners or by using the numeric interface  ― midpoints of the selection marquee afford asymmetric scaling by dragging instead (this is a simple way to create an ellipse/oval) but it is not possible to scale asymmetrically numerically (though such drag-scaling should snap to the grid):

![](<.gitbook/assets/carbide\_create\_interface\_transform\_scale (1).png>)

### Rotate

Objects may be rotated. This is often useful for decorative designs, and may be required to control part orientation when cutting or doing mechanical design, or to adjust for orientation of T-bones. Note that for some objects it may be better to alter their size rather than rotating them by 90 or −90 degrees in Carbide Create since in current versions the rotation operation will change the objects into Curve objects, removing the ability to interact with their formal parameters.

### Flip

Objects may be flipped (mirrored) horizontally or vertically. Useful for decorative designs, it also allows (for instance) the creation of reversed geometry for creating stamps or printing blocks or creating a mirror of a part for cutting it as an inlay.

### Align

Most, if not all CAD and design tools allow an option for aligning one or more objects. Typically if only one object is selected, the alignment is against the drawing area, in the case of Carbide Create, against the Stock. Alignment affords precision, and control, especially when one is using Rotation.

### Offset Path

Geometry may be selected and offset, either to the inside or outside:

![Carbide Create offset interface options](<.gitbook/assets/carbide\_create\_interface\_offsetpath (2).png>)

When offsetting paths to the outside in Carbide Create, corners are rounded off to match the distance specified as a radius. This allows one to instantiate as geometry the path which would be assigned to an endmill when cutting out a shape. If sharp corners are desired either draw the design at the largest possible size and inset only, or export to an SVG, do the offsetting operation in a 3rd party tool such as Inkscape, and then reimport, or, redraw the geometry.

### Boolean Operations

Booleans allow for the modification of geometry using existing geometry. Named for the British Mathematician George Boole: [https://www.britannica.com/biography/George-Boole](https://www.britannica.com/biography/George-Boole), they result in new figures based on a logical interaction of two or more figures, so the interface for them only appears when two or more objects are selected (the green indicates the geometry which will be produced by the operation, the black what is used and which is normally replaced by the result):

![Carbide Create Boolean options.](<.gitbook/assets/carbide\_create\_interface\_boolean (1).png>)

Depending on the selection, Carbide Create affords the following Boolean operations:

* **Union** ― the current selection (two or more objects) will be added together, creating a new object which is the outermost perimeter of the selection
* **Intersection **― only available when two objects are selected, the new object will be that area included within both objects
* **Subtraction** ― the key object (indicated by a dashed highlight) will be removed from each of the other object(s) in the selection

Note that in most programs, the selection is modified, so if the original geometry will be needed after, it may be necessary that the objects be duplicated and dragged back into alignment with the originals.

If a given operation does not have the desired result, undoing it in Carbide Create will change which object is the current key object (indicated by a dashed highlight) ― reattempting the operation will then do so based on that new aspect of the selection with different results than previously if applicable to the operation.

## Curves&#x20;

Curves are available in most vector drawing programs, and when present may be defined in several ways.&#x20;

### Bézier Curves&#x20;

The most common is Bézier curves which are defined by an on-curve point (the origin), a matching off-curve point, and an additional off-curve point paired with the ultimate (ending) on-curve point. Carbide Create uses Bézier curves in its Curve tool. Note that points are termed as Nodes in the various Curve tool options.

To create a curve, select that tool, then click or click-drag where one wants on-curve points (clicking creates sharp nodes, click-dragging creates smooth nodes, with the click placing the on-curve node, and the drag-release determining the position of the off-curve node ― either smooth or sharp nodes may be changed to the other, see below):

![Carbide Create drawing curve.](<.gitbook/assets/carbide\_create\_interface\_create\_curve (1).png>)

#### Open or Closed Paths

Once a Curve (or Polyline) is created it may be either open (indicated by being magenta when not selected), or closed (black). Open paths may be closed using the Join command:

![Carbide Create closing curve using Join command. ](<.gitbook/assets/carbide\_create\_interface\_join\_curve (2).png>)

Note that the beginning and ending nodes will be connected as directly as possible:

![Carbide Create curve closed using Join command.](<.gitbook/assets/carbide\_create\_interface\_join\_curve\_after (1).png>)

and it may be necessary to adjust the curve if the path crosses itself.

As of Carbide Create build 621 there is no way to change a closed path to being an open path. A work-around for this (other than the obvious one of exporting the geometry as an SVG, editing in a in 3rd party tool to effect the change, then reimporting) is to use off-setting and Boolean operations to create a closed geometry which describes where one wishes to cut: [https://community.carbide3d.com/t/deleting-line-help/32956](https://community.carbide3d.com/t/deleting-line-help/32956)&#x20;

#### Principles for Bézier Curves

Bézier Curves should be drawn following some basic principles unless a design dictates otherwise:

* on-curve nodes should be at extrema (north/south (top/bottom) or east/west (left/right)) and at points of inflection (where a shape changes direction, such as at the middle of an _S_ curve)
* curves are smoothest when off-curve nodes follow the “Rule of 30” and are approximately one-third (\~30 percent) of the distance towards the next on-curve node

#### Node Edit Mode

The underlying points of geometry may be modified by selecting it and choosing Node Edit Mode:

![Carbide Create Node Edit Mode.](<.gitbook/assets/carbide\_create\_interface\_node\_edit\_mode (1).png>)

As noted above, geometry is made up of lines and/or curves which are bounded by on-path nodes, and for curves, have a pair of off-path nodes which determine how the curve is drawn.

When in Node Edit Mode it is possible to right-click and:

* add an on-path node (by clicking on an part of the path which does not have nodes)
* delete an on-path node (when it is selected)
* toggle a node from smooth to sharp and vice-versa

Off-path nodes may be dragged to reshape paths, and by holding the Alt (Option) key, dragged without affecting the other off-path node for the associated on-path node creating a sharp node and asymmetry.

#### Drawing Tutorials

A very basic drawing task is to draw an oval. Originally this tutorial was available at: [http://community.carbide3d.com/t/lets-draw-an-ellipse-with-new-users/4194](http://community.carbide3d.com/t/lets-draw-an-ellipse-with-new-users/4194) — and is provided here in an updated form.

Start by launching Carbide Create — in Job Setup (gear icon) set the width of the drawing area to 20", the height to 15", and go into Job Setup | Document background | Edit Ensure the grid spacing is 0.50. Download the following file:

![](.gitbook/assets/cc\_diamond.png)

Placing it on the background layer scaled so that it fills the entire drawing area (scaling to 0.557 should work) and lines up with the grid. Ensure that Snap to Grid is enabled.

Select the Curve tool and click on each of the four points of the placed image, clicking again on the first to close the path.

Download and place the image below on the background scaled as before:

![](.gitbook/assets/cc\_ellipse.png)

Select the path and go into Node Edit Mode and right-click on each node and select "Toggle Smooth" (or press the "s" key) and drag the off-curve nodes to match the positioning of the background image.

The following additional drawing tutorials are available:

* [https://community.carbide3d.com/t/lets-make-a-b-for-anyone/14223](https://community.carbide3d.com/t/lets-make-a-b-for-anyone/14223) — drawing more complex forms with the Curve tool
* [https://community.carbide3d.com/t/how-to-draw-a-compass-rose/16170](https://community.carbide3d.com/t/how-to-draw-a-compass-rose/16170https://community.carbide3d.com/t/how-to-draw-a-star-carbide-create/16022)
* [https://community.carbide3d.com/t/how-to-draw-a-star-carbide-create/16022](https://community.carbide3d.com/t/how-to-draw-a-compass-rose/16170https://community.carbide3d.com/t/how-to-draw-a-star-carbide-create/16022)

and if one has difficulty drawing up anything, either post on the Carbide 3D community forums: [https://community.carbide3d.com/](https://community.carbide3d.com) or e-mail in to support@carbide3d.com and we will do our best to assist.

### Quadratic B-Splines

A curve which alternates on-curve and off-curve nodes, B-Splines are used for TrueType fonts, since their calculation is efficiently done, but are not used in typical CAD or Bézier curve drawing applications because of the difficulty in editing them. Note that when TrueType fonts are converted to paths, conversion from B-Splines to Bézier curves may result in odd node placement.

## Other Features

CAD and drawing programs may have a number of other features, depending on their intended use. Some of these include:

### Layers

Carbide Create supports layers since version 521. Available under Edit | Show Layers:

![](<.gitbook/assets/image (113) (1) (1).png>)

(or using the keyboard shortcut **L**)

it then affords the ability to create and name layers, as well as to color-code them:

![](<.gitbook/assets/image (114) (1) (1).png>)

and to move objects to specific layers and to hide/show, or lock/unlock layers.

## Geometry

When drawing and modeling it is often necessary to place parts relative to the original positioning based on a distance and possibly rotation determined by the dimensions of the parts. Geometry and trigonometry allow the calculation of such positioning, usually in terms of right triangles, or chords for elements based on circles or segments of circles.&#x20;

There are of course several different sorts of triangles depending on the specifics of their angles and the length of their sides.&#x20;

By length:

* scalene ― all sides are different lengths
* isosceles ― two sides are the same length
* equilateral ― all three sides are the same length

By angles:

* right triangle ― one angle is 90 degrees (may also be an isosceles or scalene triangle)
* oblique ― no angle is equal to 90 degrees
* obtuse ― one angle is greater than 90 degrees
* acute ― all angles are less than 90 degrees

Depending on the angles and the orientation of a given triangle, various labeling may be appropriate.&#x20;

For specific triangles, different formulae apply.&#x20;

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

* [http://docs.carbide3d.com/assembly/carbidecreate/userguide/](http://docs.carbide3d.com/assembly/carbidecreate/userguide/) (a web page)
* [https://carbide-downloads.website-us-east-1.linodeobjects.com/doc/UserManual\_Carbide\_20210718.pdf](https://carbide-downloads.website-us-east-1.linodeobjects.com/doc/UserManual\_Carbide\_20210718.pdf) (the official manual)
* [http://carbide3d.com/carbidecreate/video/](http://carbide3d.com/carbidecreate/video/) (a collection of tutorial videos)
* [http://community.carbide3d.com/c/software/carbide-create](http://community.carbide3d.com/c/software/carbide-create) (a community forum)
* [https://wiki.shapeoko.com/index.php/Carbide\_Create](https://wiki.shapeoko.com/index.php/Carbide\_Create) (a wiki page)

![](.gitbook/assets/carbide3d\_create\_motion\_keyboard\_shortcuts.png)

* [Carbide3D\_create\_motion\_keyboard\_shortcuts.pdf](https://community.carbide3d.com/uploads/default/original/3X/1/1/11767141a1e1d62246952219ec915572aae4c699.pdf) (available at: [https://community.carbide3d.com/t/keyboard-cheat-sheet-for-carbide-create-and-motion/7839](https://community.carbide3d.com/t/keyboard-cheat-sheet-for-carbide-create-and-motion/7839))

## Third Dimensional Shapes

Extending all of these into 3 dimensions becomes more complex with each additional element, each of which complicates the mathematics. Up through arcs and regular curves, these are usually manageable, as is expressed in constructive solid geometry (CSG), and OpenSCAD (and its Blockly derivative BlockSCAD) is essentially a scripting front-end for this. Extending arbitrary curves into 3 dimensional space involves complex geometric calculations which are the domain of 3 dimensional modeling tools such as Blender and various commercial programs. Fortunately, the regular polygons and extruded shapes of CSG afford one a very wide array of design options.
