![Doppel-1 Current Status](/img/doppel1status.png)

# About the "Doppel-1"
This repository contains the "Doppel-1", an Apple-1 Replica PCB that is somewhat unique among clone boards floating around the internet. This is being done by working off of an imported copy of gerber files for the "PCB-11" replica that I found on [Applefritter Forums](https://www.applefritter.com/content/apple-1-replica-gerber-files), which were posted originally on a facebook group. The "PCB-11" is, I believe, the most common replica board you will see pictures of online as this is the only replica (that I know of) where the gerbers have been made publicly available. These are often marked on the back in the bottom right with "Apple 1 replica 2012-2016" in soldermasked copper. If a replica board was purchased post-2020, it is likely that it is based on these gerber files, as the Mimeo-1 has been out of production since that time and up unto the time of writing.

The Doppel-1 can be considered a complete native rebuilding of "PCB-11" in KiCad, whereby the board has its own set of custom footprints that are unique to the apple-1, 3d models, native KiCad filled zones, rule areas, text elements (where possible), traces, and netclasses, as well as error fixes and fabrication notes for a production-ready PCB. Notable mistakes from the original vary from the file itself, to the schematics, to fabrication choices by the customer or the manufacturer. Clarifying remarks have been made to ensure that the PCB is being fabricated to make a reasonable replica. 

## Status of the Doppel-1

* All footprints have been designed, linked, and placed on the board
* All board text is contained within the top board layer. I have decided that there is no font matched well enough at this time to rely on a font alone. Only shapes have been redrawn at the footprint level.
* Need to fix issues with a few improper diode silkscreen arrow placements
* Proper trace widths and clearances still need assigned to all traces, ensuring proper spacing from all solder pads and enforcing a more rigorous Design Rules Check.
* a few remaining schematic parity errors.

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

## Manufacturing Notes:

If you are going to get your own replica board manufactured, read this first:

1) Normally the green finish provided by PCB manufacturers is way too dark. It has become clear to me that it will be almost impossible to replicate near-exact finishes for small volume with any direct-to-customer fabricators. If the fabricator does allow for lighter green finishes and/or matte green, these colors should be selected instead of a "Standard" green.

2) Boards that are finished with hard gold or using an ENIG process (i.e. full-board gold plating) are unable to also accomodate silkscreening on top of non-soldermasked copper. This is extremely evident in the top-right corner of the board where diode markings are missing where the gold is plated over the copper. It is understandable to desire gold for the longevity of the board, but doing so will produce a poor replica. Gold plating should be confined to the edge fingers only, with the rest done in HAL SnPb.

## Why?

Why did I do this? as Mike Willegal said, If you have to ask that question, this project isn't for you. I have had a strange fascination for the Apple-1 ever since I was a kid. I've been drawn to the technical artistry of the board, the simplicity of it, and find the assembly process and case design around it a very cool method of self-expression.

# Contributing
1) To properly view some of the pcb file's text elements, please download and install "Routed Gothic" font located in `/doc/`. This is the closest match I have found to the original PCB lettering in font form and is based on the Leroy stenciling system common with draftsman before computer fonts.

2) I have a near certain guess that the original apple-1 pcb was designed using mils. Thus, I would strongly encourage any user working on this board to set their units to mils and not mm. The original PCB-11 file was most likely not made by an American, as there are many metric dimensions scattered throughout the document. However building in nice round mil numbers should be the standard for this project

3) please submit a pull request listing in detail all changes you have made or would like to make, preferably with pictures. This can help avoid any duplicate work

4) Issues can also be raised, which I also enthusiastically accept. If you spot issues with the design of the board, please post an issue to the repository.

5) I am looking also for some more specific input on trace clearance. Since resizing the dip solderpads, clearance has been the biggest DRC issue. I would like to know what spacing was used on the original board so I can preserve that. Current clearance is set at 5 mils.

# Other Things to check out

[Erik's Ponderings - Building an Apple-1](https://blog.bruchez.name/posts/apple-1-reproduction-part-1-components/) - Erik Bruchez documented his process of building an exceptional Apple-1 clone in great detail, including some great tips for power supply building, adding more decoupling capacitors, mechanical tips, and more. Really neat to check out, especially before you build one of your own