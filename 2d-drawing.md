---
description: Drawing in 2 dimensions to make 3 dimensional parts
---

# 2D Drawing

First though, one must define the geometry of the design. This is done using classic geometric constructs, and possibly some curves defined by fancy math \(but usually drawn up in a CAD or Bézier curve drawing program. We will use Carbide Create as a specific example, but the concepts would apply to any vector drawing program, so will be explored first.

![Carbide Create interface.](.gitbook/assets/carbide_create_screengrab_fh11.png)

## Points

The most basic geometric construct as noted by Euclid in [_Elements_](https://mathcs.clarku.edu/~djoyce/java/elements/elements.html)_:_ [_Book 1_](https://mathcs.clarku.edu/~djoyce/java/elements/bookI/bookI.html)_:_ [_Definition 1_](https://mathcs.clarku.edu/~djoyce/java/elements/bookI/defI1.html) is a point in coordinate space ― some CAM tools allow one to assign a drilling operation at a point, but many vector editors disallow a point as an individual stand-alone entity, instead, they are used as a building block for everything else. Carbide Create does not allow the creation of single points, so one would create a circle to define the perimeter of the circle which one wished to machine \(see below\).

## Lines

Straight lines are the fundamental building blocks of vector drawing and are of course defined as the shortest distance between two points \(Euclid’s _Elements: Book 1:_ [_Definitions 2–5_](https://mathcs.clarku.edu/~djoyce/java/elements/bookI/bookI.html#defs). Some CAM tools \(including Carbide Create\) will allow one to assign various toolpaths to lines, and if not directly on the line, the offset will be determined by which point is the origin and which is the final point \(path direction\). Carbide Create allows one to draw lines as unclosed paths, by choosing either the Polyline \(or Curve\) tool:

![Carbide Create Polyline Tool.](.gitbook/assets/carbide_create_screengrab_polyline_hl%20%281%29.png)

clicking at the beginning and end points:

![Carbide Create drawing line with polyline tool.](.gitbook/assets/carbide_create_interface_create_polyline.png)

and then clicking on "Done". Note that open lines in Carbide Create will be indicated by being magenta.

Due to the limited toolpath support, open polylines \(or curves, see below\) are not typically used in Carbide Create, instead .one will re-work closed paths so that they have suitable geometry.

## Arcs

Many CAD programs will allow the definition of arcs which are easily drawn and may be specified in several ways — an origin point, end point, and a point of rotation are typical. Carbide Create does not have an arc tool, but they may be made using Boolean operations as parts of circles, or drawn using the Curve tool \(see below\).

## Polylines

Polylines are made up of multiple points, and/or lines/arcs/curves and are differentiated by being open or closed. 

### Open Paths

As noted above, toolpaths may be assigned to open paths, and the directionality will determine any offset. Open paths are necessarily limited in the toolpaths which may be assigned, and it will typically not be possible to assign any but the most basic of operations to them. 

### Closed Paths 

Closed paths meet back at the point of origin and open up additional operations in CAM tools. In Euclid’s _Elements: Book 1:_ [_Definition 13–14_ ](https://mathcs.clarku.edu/~djoyce/java/elements/bookI/defI13.html)they are described as a defined boundary comprising a figure. They may be made up of lines, arcs, curves, or some combination. Often tools will have especial support for regular polygons, allowing their creation or definition quickly and efficiently. Carbide Create has specific support for Circles, Rectangles \(which may be squares\), and Regular Polygons.

#### Circles

Circle are defined in Euclid’s _Elements: Book 1:_ [_Definition 15–17_](https://mathcs.clarku.edu/~djoyce/java/elements/bookI/defI15.html) __as a plane figure with one line equidistant from a point. In Carbide Create one draws circles from the inside out, clicking first at the center point, then on a point at the perimeter to define the diameter:



## Curves 

Curves are omitted from some vector drawing programs, and when present may be defined in several ways. 

### Bézier Curves 

The most common is Bézier curves which are defined by an on-curve point \(the origin\), a matching off-curve point, and an additional off-curve point paired with the ending on-curve point. Carbide Create uses Bézier curves in its Curve tool.

### Quadratic B-Splines

A curve which alternates on-curve and off-curve nodes, B-Splines are used for TrueType fonts, since their calculation is efficiently done.

## Third Dimensional Shapes

Extending all of these into 3 dimensions becomes more complex with each additional element, each of which complicates the mathematics. Up through arcs and regular curves, these are usually manageable, as is expressed in constructive solid geometry \(CSG\), and OpenSCAD is essentially a scripting front-end for this. Extending arbitrary curves into 3 dimensional space involves complex geometric calculations which are the domain of 3 dimensional modeling tools such as Blender and various commercial programs. Fortunately, the regular polygons and extruded shapes of CSG afford one a very wide array of design options.

