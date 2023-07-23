---
description: Software to move a machine around
---

# Machine Motion

Once a design has been created and toolpaths made for it, it must be cut on a machine, which means using the software which controls it. This software is generally referred to as Machine Control Software. The machine control software from Carbide 3D is Carbide Motion, which may be downloaded from: [https://carbide3d.com/carbidemotion/download](https://carbide3d.com/carbidemotion/download)

Basically, such software is the control panel of your CNC machine, allowing you to jog your machine, initialize (home) it, load and preview G-code, set the origin relative to the stock, and interact directly with the firmware (Grbl) using the MDI.

Carbide Motion is only compatible with CNC machines from Carbide3D, but other manufacturers have similar software, or electronics which afford similar controls.

Upon launch, Carbide Motion will present a screen which notes it is **Not Connected**, and afford one the chance to connect:

<figure><img src=".gitbook/assets/image (34).png" alt=""><figcaption></figcaption></figure>

If you have not yet setup your machine on the computer Carbide Motion is running on, click **Setup New Machine** (and see below), otherwise, click **Connect Cutter** to connect to your machine. The screen will update to reflect this if it is successful (if it is not, contact [support@carbide3d.com](mailto:support@carbide3d.com)):

<figure><img src=".gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

When one first connects a copy of Carbide Motion to a machine it will be necessary to go to **Settings** which has several tabs and configure for the specific machine type, type of Z-axis, the size of the machine, and any accessories as noted in the assembly/installation instructions. See the relevant documentation at: [https://my.carbide3d.com/](https://my.carbide3d.com/) and [https://my.carbide3d.com/docs/shapeoko-setup/](https://my.carbide3d.com/docs/shapeoko-setup/) as well as: [https://community.carbide3d.com/t/setting-grbl-configuration-in-cm-517-and-later/27681](https://community.carbide3d.com/t/setting-grbl-configuration-in-cm-517-and-later/27681) and in the event of any difficulties, write in to [support@carbide3d.com](mailto:support@carbide3d.com).

Once the software is connected press **Initialize Machine** to home your machine:

<figure><img src=".gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

Note that while doing so, it will display a BUSY status in the green menu bar.

Initialization will have the machine find the machine origin at the right (**X+**), back (**Y+**), top (**Z+**) corner of your machine. Note that the origin being there is a traditional choice for machining which has its basis in safety considerations --- positive moves should be away from the operator/material, so it is negative motions which are most concerning from a safety standpoint.

If you have a BitSetter (see below) it will also measure the tool offset once it has been confirmed that a tool was loaded. When using a BitSetter note that it is important that the tool only be changed when prompted, or using the command **Load New Tool** (see below) to do so. See: [https://carbide3d.com/blog/unexpected-z-axis-plunges/](https://carbide3d.com/blog/unexpected-z-axis-plunges/) for further details.

Once your machine is initialized, you’ll be presented with the **Job Info** screen (which is selected by the **Run** tab in the top menu bar) and the Jog menu will appear, so that the possible screens are:

* **Run**/Job Info&#x20;
* **Jog**/Position
* **MDI** (Manual Data Input)
* (Machine) **Settings**

## Run/Job Info

<figure><img src=".gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

This will afford the chance to load a project at this time, or it may be returned to and a file loaded later. The options are:

* **Load New File** --- When you load a file, a normal file selection dialog for your OS will be brought up to allow selecting a file.&#x20;
* **Load New Tool** (if you have a BitSetter) --- this will allow changing the currently loaded tool and then measuring its offset relative to the first tool which was measured
* **Start Job** --- this will start a job once loaded
* **Quick Actions** --- this allows storing G-code snippets/commands for repetitive tasks

The usual workflow is to first load a file --- doing so will bring up an information/G-code preview screen with several views:

### Info

<figure><img src=".gitbook/assets/image (9) (2).png" alt=""><figcaption></figcaption></figure>

### Top View

<figure><img src=".gitbook/assets/image (150).png" alt=""><figcaption></figcaption></figure>

### Front View

<figure><img src=".gitbook/assets/image (152).png" alt=""><figcaption></figcaption></figure>

### ISO View

<figure><img src=".gitbook/assets/image (158).png" alt=""><figcaption></figcaption></figure>

### G-code

<figure><img src=".gitbook/assets/image (143).png" alt=""><figcaption></figcaption></figure>

and two possible options:

* **Save G-code to File** --- this will allow extracting the G-code from a .c2d file and saving it as a .nc file
* **Done** --- this will load the G-code from the file into Carbide Motion in preparation for sending it to the machine

Once a file has loaded the **Run**/**Job Info** window will update to reflect this:

<figure><img src=".gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

And will show the name, note the time the file was loaded, and the first tool needed, and will add a **Preview** button which will again bring up the information/preview screens.

Note that it is not critical at this time to have the first tool which a file needs installed --- often a probing pin will be installed for use with a BitZero, or the tool from a previous job may still be loaded --- there will be a prompt when starting a file to load the correct tool.

Once a file has been loaded and zero set relative to the stock by jogging (see below) one may press the **Start Job** button and follow the prompts to actually cut the job.

While a job is running there will be a **Pause** button in addition to the **Stop** button. **Pause** will slow the machine down to a controlled halt and then lift and turn off the spindle. The Feed-Hold button on machines so equip should function similarly. **Stop** will attempt to stop more abruptly, but in the event of any sort of emergency, the power to the machine, spindle and vacuum should all be turned off using a suitable Emergency Stop button or switch.

## Jog/Position

Each time you click on the **Jog** or **Run** or other menu buttons there may be a prompt:

<figure><img src=".gitbook/assets/image (8) (2).png" alt=""><figcaption></figcaption></figure>

If you have changed the tool without using the appropriate command, use this reminder to measure the tool, (note that depending on version, there may be an additional prompt noting the existence of this prompt and offering further information/options) otherwise **Continue** which will bring one to:

<figure><img src=".gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

which allows one to control the machine, jogging it around using [Cartesian coordinates](https://en.wikipedia.org/wiki/Cartesian\_coordinate\_system) (left--right: **X-**/**X+** , front--back: **Y-**/**Y+**, and up/down: **Z+**/**Z-**) and setting various options.

There are keyboard shortcuts for jogging set up so that a numeric keypad may be used for moving the machine, so that the arrow keys control **X-** and **Y-**axes, while **+** and **-** control the Z-axis (Page Up and Page Down may also be used). Alternately, a gaming controller with joysticks may be used: [https://community.carbide3d.com/t/using-a-game-controller-with-cm513-and-later/21867](https://community.carbide3d.com/t/using-a-game-controller-with-cm513-and-later/21867) another option is to remap buttons on a game pad: [https://community.carbide3d.com/t/a-different-sort-of-pendant/22503](https://community.carbide3d.com/t/a-different-sort-of-pendant/22503) c.f., [https://community.carbide3d.com/t/keyboard-shortcut-cheat-sheet-for-carbide-create-and-motion/7839](https://community.carbide3d.com/t/keyboard-shortcut-cheat-sheet-for-carbide-create-and-motion/7839)

### Jog Speed Increment

The first option is the current jog speed Increment --- **Increment +** and **Increment -** buttons afford one the ability to change the jog speeds/increments (the values show are in metric, determining the equivalent Imperial values is left as an exercise for the reader):

* **0.025 mm** (keyboard shortcut 1) --- the default, note that it is too small an increment to be readily perceptible
* **0.25 mm** (keyboard shortcut 2)
* **1 mm** (keyboard shortcut 3)
* **Fast** (keyboard shortcut 4) --- this is the most used, and allows navigating the working area of even a large machine with a bit of patience, alternately, see the **Rapid Position** command below

### Spindle On/Off

This button will allow toggling the spindle on/off if one has a Nomad (with integrated spindle), BitRunner (which affords on/off automatic control of a spindle), or VFD Spindle (which allows speed control in addition to on/off). The state of the button will update to reflect the current status.

### Set Zero

Once the machine has been moved/jogged so that the tip of the spindle is at the desired position relative to the stock, then pressing this button will bring up a window which allows setting one or more axes to zero.

<figure><img src=".gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

**Zero All** will set all 3 axes with a single button press, while the **Zero X**, **Zero Y**, and **Zero Z** commands allow setting individual axes. **Clear all offsets** will restore the coordinates to their defaults for the current coordinate system, but should not normally need to be used. **Done** will return to the Jog screen once the zero has been set.

<figure><img src=".gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

### Rapid Position

This screen affords an interface for rapidly positioning the machine at cardinal points and the approximate center of the working area:

<figure><img src=".gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

as well as to **Rapid to Current XY** (zero) and to **Rapid to Current Z + 6mm** (or some reasonable equivalent in inches). The actual coordinates of the various rapid positions is determined by the physical position of the home switches, the distance which Grbl is set to pull off of them, and the Travel Dimensions for the machine. For more on this see: [http://community.carbide3d.com/t/notes-on-rapid-positions-and-wasteboard-leveling/8131](http://community.carbide3d.com/t/notes-on-rapid-positions-and-wasteboard-leveling/8131)

### Probe

If you have a BitZero and have it enabled in the Settings | Options pane, then there will be an option for Probing with it so as to set zero using it:

<figure><img src=".gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

There are four options:

* **Corner**, which probes all 3 axes and requires that the unit be registered at the lower-left corner of the stock
* **Z**, which probes for Z only and requires that the unit be fully supported on the top of the stock
* **X**, which probes for that single axis, and requires that the BitZero be positioned either at a corner (v2), or along the left edge (v1)
* **Y**, which probes for that single axis, and requires that the BitZero be positioned either at a corner (v2), or along the front edge (v1)

Note that there are two versions of BitZero and it is important that the correct type is selected --- if need be, use the button for Change BitZero Type. When probing, various windows/prompts will be presented, select the correct options which match the probing operation which you wish to do.

**Note:** It is possible to probe for all three axes at a Corner, and then overwrite for example the Z-axis zero thus set by probing for Z, say at the surface of the wasteboard which the stock is positioned on.

See: [https://community.carbide3d.com/t/using-verifying-the-bitzero/34662](https://community.carbide3d.com/t/using-verifying-the-bitzero/34662) for further details.

### Position

There is a persistent display at the left of the application window which shows the current machine position.&#x20;

The title is also a button which when pressed, changes the display coordinates into Machine Position which will show the coordinates relative to the machine origin which is set once the machine is homed:

<figure><img src=".gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

Pressing it again will toggle back the current/job coordinate system.

## Manual Data Input (MDI)

The Manual Data Input or MDI, (also known as a Manual Digital Interface) affords a text box into which a line of G-code or commands for Grbl may be entered and then sent to the machine:

<figure><img src=".gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

Note that any commands entered will be parsed by Carbide Motion unless prefaced with a /.&#x20;

Normal operation should not require using the MDI. For information on commands which may be used see the Grbl documentation: [https://github.com/gnea/grbl/wiki/Grbl-v1.1-Commands](https://github.com/gnea/grbl/wiki/Grbl-v1.1-Commands)

## Quick Actions

In addition to the MDI it is also possible to enter G-code commands for the machine using Quick Actions, accessed from the button for them on the Run/Job Info pane:

<figure><img src=".gitbook/assets/image (138).png" alt=""><figcaption></figcaption></figure>

There are two sets, Built-In (shown above), and User:

<figure><img src=".gitbook/assets/image (154).png" alt=""><figcaption></figcaption></figure>

The Edit User Macros button allows one to create or modify User Macros/Quick Actions:

<figure><img src=".gitbook/assets/image (74).png" alt=""><figcaption></figcaption></figure>

Quick Actions are made up of G-code, but only that which Grbl supports, plus those commands which Carbide Motion interprets. Unfortunately, no loops, variables, or other programming niceties.

## (Machine) Settings

The Machine Settings window has three tabs:

### Options

<figure><img src=".gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

For the specifics of settings for a Shapeoko 3, 4, or Pro in CM5 see: [https://community.carbide3d.com/t/setting-grbl-configuration-in-cm-517-and-later/27681](https://community.carbide3d.com/t/setting-grbl-configuration-in-cm-517-and-later/27681)

The Options pane allows enabling or disabling the BitSetter.

The accessories which may be attached to a machine include:

* BitSetter --- allows measuring tools for tool changes [https://my.carbide3d.com/pdf/bitsetter-v2.pdf](https://my.carbide3d.com/pdf/bitsetter-v2.pdf) (standard on the Nomad and Pro models)
* BitRunner --- affords on/off of a trim router used as a spindle [https://my.carbide3d.com/manuals/bitrunner-v2](https://my.carbide3d.com/manuals/bitrunner-v2) and is enabled or disabled using the setup wizard (see below)
* BitZero --- allows probing so as to set the origin relative to rectangular stock [https://my.carbide3d.com/manuals/shapeoko-bitzero-v2](https://my.carbide3d.com/manuals/shapeoko-bitzero-v2) which type is connected is selected in the Probing window as noted above

### Maintenance

The Maintenance pane shows information about the machine usage and affords the option to clear the counters.

<figure><img src=".gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

### Debug

<figure><img src=".gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

The Debug pane shows information on the firmware, the current state of the homing switches and BitZero/BitSetter accessores, and displays the current Machine Settings and affords an option to copy them to the clipboard for pasting (say into an e-mail to support@carbide3d.com).

#### Show Log/Log Window

The button **Show Log** brings up the **Log Window**:

<figure><img src=".gitbook/assets/image (155).png" alt=""><figcaption></figcaption></figure>

Which has a checkbox to **Hide Status Reports**, preventing the machine's reporting its current position from cluttering things up, and buttons to **Copy All** and **Clear**. Note that leaving it open will have a deleterious effect of machine performance.

If the MDI is used to send commands, their results/output will be shown here, e.g., \$$ for showing the current Grbl configuration:

<figure><img src=".gitbook/assets/image (142).png" alt=""><figcaption></figcaption></figure>

## Setup New Machine

When first setting up Carbide Motion on a new computer, it will be necessary to choose this option. Version 6 of Carbide Motion adds a setup wizard:

<figure><img src=".gitbook/assets/image (116).png" alt=""><figcaption></figcaption></figure>

click Next

Power up your machine as prompted:

<figure><img src=".gitbook/assets/image (103).png" alt=""><figcaption></figcaption></figure>

click Next

<figure><img src=".gitbook/assets/image (45).png" alt=""><figcaption></figcaption></figure>

click Connect to Machine

<figure><img src=".gitbook/assets/image (86).png" alt=""><figcaption></figcaption></figure>

click Next

<figure><img src=".gitbook/assets/image (69).png" alt=""><figcaption></figcaption></figure>

select your machine type and size from the drop-down menu and click "Download"

<figure><img src=".gitbook/assets/image (41).png" alt=""><figcaption></figcaption></figure>

&#x20;click Next

<figure><img src=".gitbook/assets/image (94).png" alt=""><figcaption></figcaption></figure>

If desired, test the homing switches, then Initialize Machine. Once the machine has finished initializing by moving to the homing switches at the top, back, right corner, click Next:

<figure><img src=".gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>

If desired, test machine motion, click Next

<figure><img src=".gitbook/assets/image (47).png" alt=""><figcaption></figcaption></figure>

If your machine has a BitSetter check the box to enable it, press the button to test that it is properly connected and working

<figure><img src=".gitbook/assets/image (21).png" alt=""><figcaption></figcaption></figure>

click Move to default position to move the machine close to where the BitSetter is by default, monitoring that the machine does not lose steps

<figure><img src=".gitbook/assets/image (90).png" alt=""><figcaption></figcaption></figure>

click Next

<figure><img src=".gitbook/assets/image (76).png" alt=""><figcaption></figcaption></figure>

Use the buttons to jog the machine to as close to the center of the BitSetter as is possible

<figure><img src=".gitbook/assets/image (28).png" alt=""><figcaption></figcaption></figure>

click Save BitSetter Configuration, click Next

<figure><img src=".gitbook/assets/image (43).png" alt=""><figcaption></figcaption></figure>

Select the options appropriate to your machine/configuration

<figure><img src=".gitbook/assets/image (65).png" alt=""><figcaption></figcaption></figure>

click Save Changes if necessary, then, click Next

<figure><img src=".gitbook/assets/image (82).png" alt=""><figcaption></figcaption></figure>

adjust Machine Options as desired

<figure><img src=".gitbook/assets/image (32).png" alt=""><figcaption></figcaption></figure>

If necessary, click Save Changes, then click Next

<figure><img src=".gitbook/assets/image (67).png" alt=""><figcaption></figcaption></figure>

click Finish.

<figure><img src=".gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>

Click Connect to Cutter and see above.
