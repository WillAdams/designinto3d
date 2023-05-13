---
description: Putting everything together to make parts and projects
---

# Machine Operation

Ideally everything for operating a machine would be covered at: [https://my.carbide3d.com/](https://my.carbide3d.com/) as well as: [https://shapeokoenthusiasts.gitbook.io/shapeoko-cnc-a-to-z/](https://shapeokoenthusiasts.gitbook.io/shapeoko-cnc-a-to-z/) with the specifics of Carbide Create covered in [2D Drawing](2d-drawing.md), [Toolpaths](toolpaths.md), and (for folks with Pro licenses) [3D Modeling from 2D Geometry](3d-modeling-from-2d-geometry.md), and Carbide Motion covered in [Machine Motion](machine-motion.md). This chapter will function as an overview of the entire process of making a part or project.

## Design

Design will be done in either a 2D (e.g, Carbide Create as shown in [2D Drawing](2d-drawing.md)), or 3D program (such as Alibre Atom 3D, FreeCAD, \&c.). Design elements may be completely contained within the geometry of the part/project, or may define the perimeter/structure of the part/project. Once a final appearance is arrived at, Toolpaths may be set up.

## Toolpaths

Toolpaths will be created or assigned in a suitable CAM program (or by directly creating toolpaths by hand-coding G-code or directly programming), and like the design, will be either 2D or 3D. Note that it is possible to assign 3D toolpaths to 2D elements and vice-versa (cutting a 3D part free with a 2D perimeter cut). Toolpaths should be added/adjusted until the 3D preview of the toolpaths is correct.

## Stock

The raw material is referred to as the stock. Depending on the nature of the cut, it may be necessary to have the stock precisely measured and entered accurately into the design file, or not. It will be necessary that the stock is securely clamped in place (see Workholding below) and the zero set relative to the stock so as to match how this is set in the G-code file.

## Workholding

The stock must be securely held in place in the working area of the machine so that the origin may be set relative to it. There are myriad products and approaches. Considerations include:

* access of the tool to the work and the ability of the tool to clear the workholding if need be
* efficient usage of the stock
* distorting the stock, or having it collapse in on the part as material is removed

## Machine Operating Checklist

1. Be safe — wear appropriate safety equipment (esp. eyes (safety glasses/goggles), and ears (hearing protection — at least foam ear plugs)), ensure clothing, hair and jewelry cannot become caught up in the machine. If necessary, arrange for dust collection and proper ventilation (if necessary, use respiratory gear suitable to the dust particles of the material being milled). Consider the possibility of the spindle starting a fire by friction and take suitable precautions (having a fire extinguisher handy, and other suitable precautions).
2. Check the machine (all bolts and set screws tight, V-rails in good condition with no nicks or other damage, belts tight and in good shape, linear rails and ballscrews well lubricated, wiring in good condition with continuity and securely fastened, and nothing frayed or broken, everything clear and safe). The bolted down, inverted belts which result when using the belt anchor clips make this somewhat difficult — use a mirror to examine the belts while moving the machine along its full range of movement. Note that it is especially important to check the machine after a crash or a failed cut or one which induces chatter or excessive vibration.
3. Secure the workpiece (right-side up and in the desired orientation) to the worksurface using a technique appropriate to the material (see Workholding). After securing the workpiece, be certain that the machine is still able to move — this is especially important on the Nomad where the through holes on the table create the possibility of a too-long bolt locking the table to the machine base.
4. Mount an appropriate spindle and ensure that it is vertical and square to the machine and well-secured.
5. Examine the End mill to ensure that it is sharp and in good condition and not chipped (this is best done with a loupe or magnifying glass), install it per the spindle manufacturer's directions so that it projects at least as much as the deepest intended cutting depth, check to make certain that everything is clean with no foreign material (which can cause runout or even break endmills), the collet is tight and will not work loose during operation (it needs to be more than hand-tight --- the machine will take no notice or care if it works loose) and the entire assembly is in good condition and spins truly.&#x20;
6. Ensure the work area is clear and all cables, wires, etc. run without interference, and that they will not interfere with the machine motion, esp. when homing. Especially check that there is nothing beneath the rails which might interfere with the wheels.
7. Connect the machine to the computer (power up PC, connect the USB cable, wait until the micro-controller boots up, start the comm/control program, turn on power for the machine (this may just be plugging it in (usually a light will glow on the power supply), some power supplies may have a power switch, or a switch between 110 and 220V, check, once switched on there should be a steady light on the control board which you should be able to see the glow of (other lights (homing switches, communication) will flicker on and off) --- if you cannot see the glow, check the power supply and cable and so forth for switches), open the connection to the machine). If necessary, home the tool to the proper place in relation to the workpiece. (In the absence of limit switches, machine origin will be the location when Grbl powers up.)
8. If using a Probe be certain to remove the ground clip and secure it safely outside of the machine's working area. Ensure that nothing has been left in the work area. (Optional: Traverse the working boundary of the job as a final check.)
9. Browse for the NC file which you have created, double check the preview, and send it to the machine, following all prompts for tool changes and starting the spindle as required and setting it to the correct speed.
10. Monitor the machine while it operates, ensuring there is no build-up of dust, debris or fumes, and that nothing works loose, keeping clear of the work area. Do not reach into the machine’s working envelope, nor insert any object into it while the machine is operating. Once the job is complete, turn off the spindle, return the gantry to the home position, or a known offset from home and ensure the end mill has stopped spinning before removing the finished piece and any waste. Store endmills carefully when not in use so as to protect the edges. Collets and accessories should be cleaned between uses — wiped off with a suitable solvent such as isopropyl alcohol.

One should keep a log of machine usage and note when adjustments are made, or a fastener is (re)tightened, as well as keeping a tally of usage time, including for specific bits, so as to determine when parts need to be lubricated, or bits should be relegated to rough work or resharpened or recycled and replaced. Similarly, one should record machine settings and the specifics of each tool chain which is used with the machine.

### Safety and Precautions

The Shapeoko is a machine tool, and requires the same caution which should be exercised around any power tool. For its typical configuration of a trim router cutting wood and plastic, the same sort of safety gear advocated for the trim router is suggested:

* Eye protection — safety glasses or goggles which are suitably impact resistant
* Hearing protection — ear plugs or muffs, for long jobs doubling these up may be desirable. Hearing damage is cumulative and irreversible, so one should err on the side of caution
* Respiratory protection — a filter or respiratory mask suited to the dust generated by the material being cut should be worn
* Ensure clothing, hair, and/or jewelry cannot become caught in the machine, never reach into the machine’s working envelope while it is running — long sleeved shirts and pants and suitable footwear is suggested, when doing metal-working, gloves and an apron are recommended

Additionally

* Use care when handling endmills, both to avoid being cut, and to avoid damaging them. Handling them with suitable gloves, or using a cloth to avoid contaminating them is recommended. Inspect them carefully before each use and ensure that they are securely held by the collet.
* Never leave the machine running unattended/unsupervised.
* Always inform someone before operating the machine and check in with them after successfully completing work.
* Safely dispose of milling debris — recycle or safely dispose of milling debris and dust, keeping in mind flammability, (potential) spontaneous combustion, and chemical considerations. Even natural materials can have surprising implications for disposing of them, _e.g._, walnut wood dust is aleopathic (inhibits plant growth) and an irritant to the skin and breathing tract and potentially poisonous to some animals in addition to the typical spontaneous combustion hazard which sawdust poses.

