---
description: Cutting box (finger) joints vertically in boards at the front of the machine
---

# Box (Finger) Joints

Starting with the box design template from the previous chapter: [https://www.blockscad3d.com/community/projects/1012246](https://www.blockscad3d.com/community/projects/1012246) it is a simple matter of adding cuts for joinery along the corners of the box. Box joints are notable since they can be implemented along all edges of a box and with a bit of a relief can be cut flat on the machine simplifying fixturing and making manufacture more efficient, but the traditional technique of box joints at the box corner with the top and bottom in rabbeted grooves is simpler to calculate, and is discussed at: [https://community.carbide3d.com/t/cnc-finger-joint-box/8880](https://community.carbide3d.com/t/cnc-finger-joint-box/8880) and will be worked out in detail below. For further details, see: [https://en.wikipedia.org/wiki/Box\_joint](https://en.wikipedia.org/wiki/Box\_joint)

Note that while they may be colloquially termed Finger Joints, that term should properly be limited to the angled joints used for joining two pieces of wood (usually along their length). [https://en.wikipedia.org/wiki/Finger\_joint](https://en.wikipedia.org/wiki/Finger\_joint)

Necessary additional variables are:

* Endmill Diameter
* Thickness of top/bottom grooves (or possibly rabbets for reducing board thickness along edges to fit into grooves)
* (optional) a number to influence how many iterations of the joint features will be cut
* Some sort of option for the lid ― options include a sliding lid, a rabbet along the edge for the lid to fit onto, or a through cut after glue-up and a suitable hinge

If box joints are cut in sheet goods with the boards flat, it is necessarily more complex

The interplay of the geometry of the board being flat and the cutter being round requires certain options and accommodations in the module for cutting the joints. It is necessary to specify:

* Endmill Diameter
* Whether the cut should be adjusted for endmill diameter
* Whether the cut should be relieved for endmill diameter
* If the cut should be adjusted at its beginning or end for the thickness of the material

Setting up a box design for this we duplicate the project from the previous chapter as: [https://www.blockscad3d.com/community/projects/1052045](https://www.blockscad3d.com/community/projects/1052045) and update it with the desired dimensions:

* 10 in wide
* 8 in deep
* 3.5 in high
* 0.25" thick stock
* 0.21653543" (5.5mm) thick top and bottom
* 0.375" part spacing

As OpenSCAD code, this has the file beginning as:

```
//!OpenSCAD

Height = 3.5;
Width = 10;
Depth = 8;
Stock_Thickness = 0.25;
Top_Bottom_Thickness = 0.21653543;
Part_Spacing = 0.375;
//(millimeters or inches)
Units = 1; //[1:millimeters, 25.4:inches]
Preview_3D = true;
Joinery_Cut = false;
Generate_DXF = false;
Endmill_Diameter = 0.125;
```

With all of the variables set up, it is necessary to scale for units:

```
h = Height * Units;
w = Width * Units;
d = Depth * Units;
st = Stock_Thickness * Units;
tbt = Top_Bottom_Thickness * Units;
ps = Part_Spacing * Units;
cd = Endmill_Diameter * Units;
fjcount = (ceil(Height / Stock_Thickness) / 2) * 2 + 1;
fjsize = h / fjcount;
```

as shown below:

![BlockSCAD: Box joints: Vertical: Variables](<.gitbook/assets/blockscad fingerjoint vertical variables.PNG>)

Add code to cut grooves for the lid and for the box joints themselves --- this will want a module for modeling the endmill:

```
module em() {
  cylinder(r1=(cd / 2), r2=(cd / 2), h=(cd + st), center=false);
}
```

which is then used in a module which makes a cut as a pocket:

```
module cut(cbx, cby, cex, cey, abx, aby, aex, aey, sd, ed) {
  translate([0, 0, (sd - ed)]){
    hull(){
      translate([cbx, cby, 0]){
        em();
      }
      translate([cex, cey, 0]){
        em();
      }
      translate([abx, aby, 0]){
        em();
      }
      translate([aex, aey, 0]){
        em();
      }
    }
  }
}
```

![BlockSCAD: Box joints: Vertical: Features](<.gitbook/assets/blockscad fingerjoint vertical features.PNG>)

&#x20;A legacy of the prototype box file used is that there is a module for modeling a board:

```
module board(ht, wd, dpth) {
  cube([wd, dpth, ht], center=false);
}
```

At some point in the future that may be used as a control point for modifying how the file is previewed or rendered.

That module is then used for additional modules for each sort of part needed. Quite simple for the top and bottom:

```
module topbottom() {
  board(tbt, w - st, d - st);
}
```

But requiring various calculations for the grooves and box joints for the sides:

```
module sides() {
  difference() {
    board(st, h, d);

    cut(st / 2 + cd / 2, st / 2, st / 2 + cd / 2, d - st / 2, (st / 2 + tbt) - cd / 2, st / 2, (st / 2 + tbt) - cd / 2, d - st / 2, st, st / 2);
    translate([(h - st * 2), 0, 0]){
      cut(st / 2 + cd / 2, st / 2, st / 2 + cd / 2, d - st / 2, (st / 2 + tbt) - cd / 2, st / 2, (st / 2 + tbt) - cd / 2, d - st / 2, st, st / 2);
    }
    if (Generate_DXF == false) {
      union(){
        translate([0, (-cd), (-st)]){
          for (i = [1 : abs(2) : fjcount]) {
            translate([(i * fjsize), 0, 0]){
              cube([fjsize, (cd + st), (st * 3)], center=false);
            }
          }

        }
        translate([0, (d - st), (-st)]){
          for (i = [1 : abs(2) : fjcount]) {
            translate([(i * fjsize), 0, 0]){
              cube([fjsize, (cd + st), (st * 3)], center=false);
            }
          }

        }
      }
    }

  }
}
```

&#x20;and front/back:

```
module frontback() {
  difference() {
    board(st, w, h);

    cut(st / 2, st / 2 + cd / 2, w - st / 2, st / 2 + cd / 2, st / 2, (st / 2 + tbt) - cd / 2, w - st / 2, (st / 2 + tbt) - cd / 2, st, st / 2);
    translate([0, (h - st * 2), 0]){
      cut(st / 2, st / 2 + cd / 2, w - st / 2, st / 2 + cd / 2, st / 2, (st / 2 + tbt) - cd / 2, w - st / 2, (st / 2 + tbt) - cd / 2, st, st / 2);
    }
    if (Generate_DXF == false) {
      union(){
        translate([(-cd), 0, (-st)]){
          for (i = [0 : abs(2) : fjcount - 1]) {
            translate([0, (i * fjsize), 0]){
              cube([(cd + st), fjsize, (st * 3)], center=false);
            }
          }

        }
        translate([(w - st), 0, (-st)]){
          for (i = [0 : abs(2) : fjcount - 1]) {
            translate([0, (i * fjsize), 0]){
              cube([(cd + st), fjsize, (st * 3)], center=false);
            }
          }

        }
      }
    }

  }
}
```

In particular note the halving and then doubling of the number of box joints before adding 1 so as to ensure that an odd number is used for one set.

As well as laying out the parts for cutting:

![BlockSCAD: Box joints: Vertical: DXF](<.gitbook/assets/blockscad fingerjoint vertical DXF.PNG>)

The final aspect is cutting the joints ― the boards need to be offset from each other:

![BlockSCAD: Box joints: Vertical: Boards](<.gitbook/assets/blockscad fingerjoint vertical Boards.PNG>)

and cut in at least pairs (cutting all four at once will halve the number of operations):

![BlockSCAD: Box joints: Vertical: Cuts](<.gitbook/assets/blockscad fingerjoint vertical cuts.PNG>)

See: [https://www.blockscad3d.com/community/projects/1053568](https://www.blockscad3d.com/community/projects/1053568)

Export to OpenSCAD from BlockSCAD and then customize the file in OpenSCAD to allow exporting SVGs:

![OpenSCAD: Box joints: Vertical: Parts](<.gitbook/assets/openscad fingerjoint vertical parts.PNG>)

![OpenSCAD: Box joints: Vertical: Cuts](<.gitbook/assets/openscad fingerjoint vertical cuts.PNG>)

The final code is using the checkboxes to control how the parts are rendered as discussed above:

```
if (Preview_3D == false) {
    projection(cut = true)
    {
  union(){
    translate([0, (h + ps), -st*0.9]){
      sides();
    }
    translate([(h + ps), 0, -st*0.9]){
      frontback();
    }
    translate([((h + ps) + st / 2), ((h + ps) + st / 2), 0]){
      topbottom();
    }
    translate([(h + ps), ((h + ps) + (d + ps)), -st*0.9]){
      frontback();
    }
    translate([((h + ps) + (w + ps)), (h + ps), -st*0.9]){
      sides();
    }
  }
}} else {
  if (Joinery_Cut == false) {
    union(){
      translate([0, ps, (h + ps)]){
        rotate([0, 90, 0]){
          sides();
        }
      }
      translate([0, 0, 0]){
        mirror([0,1,0]){
          translate([ps, 0, ps]){
            rotate([90, 0, 0]){
              frontback();
            }
          }
        }
      }
      translate([(ps + st / 2), (ps + st / 2), (st / 2)]){
        topbottom();
      }
      translate([(ps + st / 2), (ps + st / 2), ((h + ps * 2) - st * 1.5)]){
        topbottom();
      }
      translate([((w + ps * 2) - 0), ps, (h + ps)]){
        rotate([0, 90, 0]){
          mirror([0,0,1]){
            sides();
          }
        }
      }
      translate([ps, (d + ps * 2), ps]){
        rotate([90, 0, 0]){
          frontback();
        }
      }
    }
  } else {
    if (Generate_DXF == true) {
        projection(){
      union(){
        cube([(cd / 2), (cd / 2), (cd / 2)], center=false);
        translate([fjsize, (-(cd / 2)), 0]){
          for (j = [0 : abs(2) : fjcount]) {
            translate([(j * fjsize), 0, 0]){
              cube([fjsize, ((st * 4 + ps * 3) + cd), (st * 2)], center=false);
            }
          }

        }
      }
    }} else {
      difference() {
        union(){
          translate([0, st, (st - d)]){
            rotate([90, 0, 0]){
              union(){
                sides();
                translate([0, 0, (-(st + ps))]){
                  sides();
                }
              }
            }
          }
          translate([fjsize, ((st + ps) * 2 + st), st]){
            rotate([90, 90, 0]){
              union(){
                frontback();
                translate([0, 0, (-(st + ps))]){
                  frontback();
                }
              }
            }
          }
        }

        translate([fjsize, (-(cd / 2)), 0]){
          for (j = [0 : abs(2) : fjcount]) {
            translate([(j * fjsize), 0, 0]){
              cube([fjsize, ((st * 4 + ps * 3) + cd), (st * 2)], center=false);
            }
          }

        }
      }
    }
  }
}

```

The OpenSCAD file is available at: [https://github.com/WillAdams/Design\_Into\_3D/blob/master/box/fingerjoint/vertical/Box\_%20Fingerjoint\_%20Vertical.scad](https://github.com/WillAdams/Design\_Into\_3D/blob/master/box/fingerjoint/vertical/Box\_%20Fingerjoint\_%20Vertical.scad)

Export each view and import into Carbide Create files:

![Carbide Create: Box joints: Vertical: Parts](<.gitbook/assets/carbidecreate fingerjoint vertical parts.PNG>)

![Carbide Create: Box joints: Vertical: Cuts](<.gitbook/assets/carbidecreate fingerjoint vertical cuts.PNG>)

Once imported, it will be helpful for the Cuts file to set the stock size to match the boards being used, and to draw in rectangles representing the boards --- this will help to make clear how they are to be positioned for cutting and how the toolpaths will interact. The 3D preview of the toolpaths shows the cuts which will be made which is accurate save for the excess stock shown at the upper left and lower right corners (areas not encompassed by the orange highlighted boards in the image above):

![Carbide Create: Box joints: Vertical: Cut 3D Preview](<.gitbook/assets/carbidecreate fingerjoint vertical cut preview.PNG>)

A desirable improvement is to trim the right-most geometry so that it only cuts the rearmost boards:

![Carbide Create: Box joints: Vertical: Cuts trimmed](<.gitbook/assets/carbidecreate fingerjoint vertical parts trim.PNG>)

For the Parts file, it is only necessary at first to cut one side, and a single instance of the front/back part --- the parts need to be positioned in-line and separated by at least the endmill diameter plus 10%. The top/bottom will be measured for from the actual box after it is cut and dry fit. A further consideration here is the matter of accessing the interior of the box --- we will draw in a rectangle which may be cut with a narrow endmill (or one may do the traditional cutting apart with a bandsaw or hand saw):

![Carbide Create: Box joints: Vertical: Parts in-line](<.gitbook/assets/carbidecreate fingerjoint vertical parts inline.PNG>)

Since the parts will be cut from an S4S board which is the correct size, it will only be necessary to machine the grooves for the top/bottom, the groove with tabs separating the lid from the base of the box (import a copy of the box joint cuts and rotate 90 degrees to allow for placement), and pockets at the ends of each board to cut them to length. To eliminate the need for tabs and the attendant post-processing, work-holding will be two-stage:

* normal clamps outside the cutting area as well as a sacrificial caul clamp across the gap between the parts
* additional cauls added after cutting the grooves to secure the stock and ensure the parts do not move once cut free

To ensure the board is square to the machine the first operation will be to machine a pocket in which to register the board, then the board will be secured and the grooves cut, then the additional cauls put in place, and the last operation will be cutting the pockets which cut the part to length.

![Carbide Create: Box joints: Vertical: Toolpaths](<.gitbook/assets/carbidecreate fingerjoint vertical parts toolpaths.PNG>)

Verify the preview:

![Carbide Create: Box joints: Vertical: Parts Preview](<.gitbook/assets/carbidecreate fingerjoint vertical parts preview.PNG>)

Then cut the parts:

![Carbide Create: Box joints: Vertical: Cutting Parts](.gitbook/assets/WIN\_20201127\_16\_23\_47\_Pro.jpg)

Then mount them in a fixture such as: [https://cutrocket.com/p/5cb25f3380844/](https://cutrocket.com/p/5cb25f3380844/) and cut the joints

![Carbide Create: Box joints: Vertical: Setup for Joints](.gitbook/assets/WIN\_20201128\_13\_38\_27\_Pro.jpg)

![Carbide Create: Box joints: Vertical: Clamping for Joints](.gitbook/assets/WIN\_20201128\_13\_41\_20\_Pro.jpg)

![Carbide Create: Box joints: Vertical: Measuring Joints](.gitbook/assets/WIN\_20201128\_15\_50\_57\_Pro.jpg)

Then dry-fit to measure for cutting the top/bottom (or just cut the top/bottom based on the initial CAD measurement):

![Carbide Create: Box joints: Vertical: Joints Test Fit](.gitbook/assets/20201129\_143144\[1].jpg)

The cut the top and bottom and glue and clamp up:

![Carbide Create: Box joints: Vertical: Joint Glue Up](.gitbook/assets/WIN\_20201129\_19\_06\_39\_Pro.jpg)

Last cut apart, clean up edges, finish, and install hardware:

![Carbide Create: Box joints: Vertical: Assembled and Glued](.gitbook/assets/WIN\_20201129\_20\_33\_53\_Pro.jpg)

![Carbide Create: Box joints: Vertical: Cut Apart](.gitbook/assets/WIN\_20201130\_10\_15\_33\_Pro.jpg)

![Carbide Create: Box joints: Vertical: Ready for finishing and hardware](.gitbook/assets/WIN\_20201130\_23\_50\_55\_Pro.jpg)

![Finished box with box joints and installed hardware](.gitbook/assets/20201210\_213240\[1].jpg)

While it is possible to do traditional box joints on a CNC, the tedium of multiple setups can be avoided on a CNC, which will be explored in the next chapter.

The files for the above box are available at: [https://community.carbide3d.com/t/cnc-finger-joint-box/8880/133](https://community.carbide3d.com/t/cnc-finger-joint-box/8880/133)

For more on the vertical fixture, see https://community.carbide3d.com/t/sharing-carbide-create-dovetail-files/9371/24

Basically it's just a pair of boards which you can secure to the machine bed which then projects and you put a pair of nuts in it which you screw the threaded rod into. The rods then hang down at the front of the machine and you use speed nuts to make it possible to move a bar up and down along them:

https://community.carbide3d.com/t/cnc-box-finger-joint-box/8880/48

https://community.carbide3d.com/t/cnc-box-finger-joint-box/8880/50

https://community.carbide3d.com/t/cnc-box-finger-joint-box/8880/58
