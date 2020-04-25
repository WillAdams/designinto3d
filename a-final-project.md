---
description: A project which uses multiple materials and techniques
---

# A Final Project

While there are many guides for making coopered boxes, none of them discuss the underlying mathematics and algorithms. This project allows one to design a traditional chest made up of multiple boards, and straps of a different material \(the design will assume metal, but adapting the design to leather will also be covered\).

The first consideration is the necessary parameters. Rather than using absolute/specific dimensions, the height and length and width of the project will be defined in terms of the base width of the boards, so the first parameters would be to define:

* BoardWidth
* BoardThickness
* BoardGap

In keeping things proportional, it will also be expedient to use that last value as the gap for the metal parts, but since metalwork is normally more precise we will use one-fourth that dimension.

The actual size of the base of the box will be calculated from:

* BoxWidthinBoards
* BoxDepthinBoards
* BoxHeightinBoards

In addition we will provide the following options for styles of lid:

* Flat — a plain flat lid
* Faceted — a three-sided, Mansard-style lid
* Arched — a traditional coopered \(curved, multi-piece\) lid

In order to facilitate the strapping \(for simplicity's sake it is assumed the flat strapping is the same width and thickness as the angle profile\) it will be necessary to specify the dimensions for it:

* AngleWidth
* AngleThickness

Lastly we will need to fasten things with some sort of hardware which requires that a hole is placed through the strapping — for simplicity a matching hole will not be machined during manufacture, instead it is expected that the holes will be drilled during assembly. Similarly, the actual hardware used is not specified, only the diameter of the necessary hole:

* HardwareDiameter

This yields:

![](.gitbook/assets/blockscad-final-project-variables.PNG)







