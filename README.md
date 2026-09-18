![Doppel-1 Current Status](/img/doppel1status.png)
Doppel-1 As of 2026/09/18

# About the "Doppel-1"
This repository contains the "Doppel-1", an Apple-1 Replica PCB. It is unique among clone boards in that the source design files are completely open-source, and It is built in standard EDA fashion, where each component on the board is linked to a symbol on a full schematic of the apple-1. This also allows for generating gerber files at the source, easy modification, and the ability to highlight trace sets on the board via the net selector. This makes it very useful when diagnosing build issues. It also features a near full set of 3d components, which allows an accurate step file to be exported.

![Doppel-1 3D](/img/d13d.png)
Doppel-1 within KiCad 3D Viewer

Great care has been taken to create a custom library of footprints that match the original apple-1. In fact, every symbol on the board is custom. This preserves the aesthetics of the pads and silkscreens while allowing for pin-pin linkage from the schematic.

Clarifying remarks have been made to ensure that the PCB is being fabricated to make a reasonable replica. If you desire to make your own board from these files, please read the Manufacturing Notes below.

## History
This project started by importing the gerber files for the "PCB-11" replica that I found on [Applefritter Forums](https://www.applefritter.com/content/apple-1-replica-gerber-files), which were posted originally on a facebook group. It is the only clone board that I know of where the gerber files have been made publicly available. Little by little, I began replacing gerber features with native KiCad features, until there was almost nothing left of the original gerber (see "Open Issues..." Below). A theseus ship of sorts, but improved.



## Open Issues of the Doppel-1

* All board silkscreen text is contained within the top board layer. I have decided that there is no font matched well enough at this time to rely on a font alone. Only shapes have been redrawn at the footprint level.
* Need to fix issues with a few improper diode silkscreen arrow placements
* Proper widths and clearances still need assigned to all traces, ensuring proper spacing from all solder pads and enforcing a more rigorous Design Rules Check.
* I am still not entirely certain the board mounting holes are in the correct position. I had modified it slightly see point 7 below.
* a few remaining schematic parity errors.
* some copper layer graphics are still drawn as tracks from the gerber import. These need converted to graphic shapes to satisfy DRC warnings
* the edge connector fingers still contain gerber fill tracks instead of native kicad filled shapes. this needs to be created and turned into a footprint.
* some footprints still don't have 3d models assigned. I think at this time only the molex 4-pin and 6-pin
* I would like to develop a custom font based off the text on this board, so it can be applied as text elements rather than drawn shapes.

## Design Notes And Changes
I have made some remarks about my observations so far:

1) The silkscreen text on the Apple-1 PCB is extremely difficult to reproduce. By all accounts it was hand-stenciled, and I have spent more time than I care to admit comparing uniform-stroke technical typefaces that are meant to replicate leroy lettering or other technical stencil packages that are freely available online, but none of them have quite matched what I have seen on the PCB-11 and on other clones. I have messed around with the font "Routed Gothic" and found it to be closest but kerning is not quite there, and it still does not match with the characters aforementioned. I can hack my way to passable kerning by adjusting the height-width ratio of the text boxes but it is not ideal. I believe Iwater GMaru Gothic Pro is a better match to the original, however that is a paid font that I am unwilling to obtain due to licensing. For any future work on a custom font for this computer, I have included a character "Proof Area" in the PCB file which contains every character on the board.

2) The solder pads on the DIP sockets and breadboard area on "PCB-11" are round on both front and back layers, while on original units, the solderpads were actually different on the back side vs the front. On the back they were a squashed oval (basically an obround but the end arcs share a center point with the rectangle's center point), and on the front they were smaller, tangent obrounds. This was most likely done to make it easy to solder while leaving room for trace paths on the front. This is something a lot of replicas miss.

3) The trace leading to the positive lead between B&C @16 has been adjusted to match the Mimeo-1

4) The trace between C&D @15 leeting to the via below IN914 diode at a 45 degree angle has been moved down slightly to match the Mimeo-1

5) silkscreen outlines for DIP sockets has been increased to a width of 10mils to match what is expected

6) In the original manual's schematics, as well as the ones made by Nicolas, there is an error in the pinouts listed for the TO-220 diodes (REG1,REG3,REG4/LM320 MP-5/LM320 MP-12/LM340 MP-12). LM320 has ground at pin 1, while in and out are pins 2&3, respectively.LM340 has ground at 2 and in/out at 1/3 like a more standard diode in this package. This was discovered by DRC error checking.

7) The top right mounting via has been moved right 100mils to match Mike Willegal's case dimension [here](https://www.willegal.net/appleii/apple1-enclosure.htm). My assumption is that these are truer than what were originally on the board

8) The original applefritter post had a user comment that noted the following issues. My comments are appended to the original marks:
- The original has a matte finish, this one has a sligtly brighter green - This is a fabrication preference/availability, not with the design of the board. see "Manufacturing Notes".
- The silkscreen doesn't cover the plated areas without soldermask.
- The DIP and breadboard solder pads should be wider although it only really matters in the breadboard area. - See point 2 above, much scrutiny went into the shape of the dip pads on this board.
- The video adjustment pot pads are  narrower by 0.025", making it difficult to insert the trimpot. - The 100 Ohm pot has been replaced with a standard footprint that should rectify the issue

9) the LM323 footprint has been moved slightly to the left, on the original and observed builds, the heatsink would hang slightly over the board.

## Manufacturing Notes:

If you are going to get your own replica board manufactured, read this first:

0) Boards are to be purchased at your own risk. I do not take responsibility for any defects, design or otherwise, contained within your finished boards.

1) Normally the green finish provided by PCB manufacturers is way too dark. It has become clear to me that it will be almost impossible to replicate near-exact finishes for small volume with any direct-to-customer fabricators. If the fabricator does allow for lighter green finishes and/or matte green, these colors should be selected instead of a "Standard" green.

2) Boards that are finished with an ENIG process (i.e. full-board gold plating) are unable to also accomodate silkscreening on top of non-soldermasked copper. This is extremely evident in the top-right corner of the board where diode markings are missing where the gold is plated over the copper. It is understandable to desire gold for the longevity of the board, but doing so will produce a poor replica. ENIG is also not sufficient for edge fingers; since ENIG is a softer finish, it will wear just as if it were plated like a standard PCB. Hard Gold plating (not ENIG) is best for edge fingers, and should be confined to the edge fingers only, with the rest done in HAL SnPb.

3) I request that anyone exporting their own gerbers to not remove the replica signifying text on the bottom right on the back of the board. This board contains "Doppel-1 Rev. 2026" on the back copper layer underneath a silkscreen, so it is very discrete. While I think that there are many people out there that can detect replica boards without an unambiguous stamp on the board, I request all reading to preserve the marking to avoid the perception or attempts at counterfeiting.

## Why?
I have had a strange fascination for the Apple-1 ever since I was a kid. Even though I am not a competent electronics hobbyist or electrical engineer, I've been drawn to the technical artistry of the board, and find the assembly process and case design around it a very cool method of self-expression. I suppose also there is a love of historical artifact that comes with people who love these computers too, and I am very much in that camp.

# Contributing
1) To properly view some of the pcb file's text elements, you may need to  download and install "Routed Gothic" font located in `/doc/`. This is the closest match I have found to the original PCB lettering in font form and is based on the Leroy stenciling system common with draftsman before computer fonts.

2) I have a near certain guess that the original apple-1 pcb was designed using mils. Thus, I would strongly encourage any user working on this board to set their units to mils and not mm. The original PCB-11 file was most likely not made by an American, as there are many metric dimensions scattered throughout the document. However building in nice round mil numbers should be the standard for this project

3) please submit a pull request listing in detail all changes you have made or would like to make, preferably with pictures. This can help avoid any duplicate work. I can infer many changes by inspecting the changed files as text, but a more human-readable explanation helps.

4) Issues can also be raised, which I also enthusiastically accept. If you spot issues with the design of the board, please post an issue to the repository.

5) I am looking also for some more specific input on trace clearance. Since resizing the dip solderpads, clearance has been the biggest DRC issue. I would like to know what spacing was used on the original board so I can preserve that. Current clearance is set at 5 mils.

# Other Things to check out

[Erik's Ponderings - Building an Apple-1](https://blog.bruchez.name/posts/apple-1-reproduction-part-1-components/) - Erik Bruchez documented his process of building an exceptional Apple-1 clone in great detail, including some great tips for power supply building, adding more decoupling capacitors, mechanical tips, and more. Really neat to check out, especially before you build one of your own