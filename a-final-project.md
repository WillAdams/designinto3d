---
description: A project which uses multiple materials and techniques
---

# A Final Project

While there are many guides for making coopered boxes, none of them discuss the underlying mathematics and algorithms. This project allows one to design a traditional chest made up of multiple boards, and straps of a different material \(the design will assume metal, but adapting the design to leather will also be covered\).

The first consideration is the necessary parameters. Rather than using absolute/specific dimensions, the height and length and width of the project will be defined in terms of the base width of the boards, so the first parameters would be to define:

* boardwidth
* boardthickness
* boardgap

In keeping things proportional, it will also be expedient to use that last value as the gap for the metal parts, but since metalwork is normally more precise we will use one-fourth that dimension.

The actual size of the base of the box will be calculated from:



