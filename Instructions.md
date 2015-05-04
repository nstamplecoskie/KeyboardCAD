### These instructions will help you to quickly generate a FreeCAD file with this script.

1.  If you have not already done so, download and install the latest version of FreeCAD.

2.  Copy the raw data from your http://www.keyboard-layout-editor.com/ to a new text document anywhere on your computer. Do not forget the label parameters:
    *   !r! for rotating a switch with cutouts or alps compatibility by 90 degrees (so that cutouts are on the top and bottom)
    *   !c! for toggling cut-out type for that switch to be the H shape (Standard Cherry square with cut-outs for switch disassembly)
    *   !a! for toggling cut-out type for that switch to be alps-compatible. This takes precedence over !c! if you have both in the same labelOf course, there's an option for adding these settings for all keys, so don't add them to the label of every key. Also, you may have to encode the file to ANSI (this is easy to do in notepad++). Certain encodings will cause the layout to not be read correctly, or not at all (Thanks to /u/WalrusPorn for reporting this).

3.  Open up KeyboardCAD.py in a text editor. You will have to modify the lines found in the user parameters section at the very top of the script. This includes the size of the plate, location where you saved the layout data and the file name you will save the document as. Perhaps most important is the switchHoleType:
    *   0 for standard square holes
    *   1 for the "H" shape with cutouts for switch disassembly
    *   2 for Alps compatible (with switch disassembly for cherry possible)

4.  Once your user parameters are all correct, review the code in the measurements section. The values in that section are all defaults that I derived from various sources. It is likely that you won't have to change anything if you are making a board with standard spacing. Note that the stabilizer width values (LONGSTABILIZERPOSTTOPOST) match the stabilizers and the keycaps you want to use.

5.  If you are not running the script using the python file included in the FreeCAD bin folder, then you will have to give values to the two variables in the PATHS section

6.  (Optional) Populate the screw hole list if you know the x, y coordinates of each hole on the plate. This is more useful if you plan on making a bottom plate too. By using a blank keyboard layout, the script will make a plate with the same dimensions and screw holes, but no switches; therefore, a back plate.

7.  Save changes to the script and make note of its location on your computer.

8.  Time to run the script! There are multiple ways to this if you have python installed on your system. If you don't have python 2.7 installed, then do the following:
    *   Open up a command or terminal window
    *   Change directory to the FreeCAD bin folder
    *   Enter a command to call the python program with the path to the KeyboardCAD.py as a parameter, thus executing it. For example, with windows in cmd: python.exe d:\Users\Nick\Documents\Dev\KeyboardCAD\KeyboardCAD.py
    *   You may notice an error message saying that a module was not found. Ignore it as it is a bug in FreeCAD

9.  Once it says that it saved successfully, you have a 3D model of your custom keyboard plate. Open it up and take a look. All the parts will probably be invisible at first. Ctrl + a will select all objects and space will make them visible.

10.  The program should be prompting you to join the parts together. This is not done automatically since it takes 5-10 for your computer to complete. Before you enter "y", or something equivalent, make sure that everything on the plate turned out as expected. If you enter "n", or something equivalent, you will have to do this operation manually later. To do this:
    *   Go to the part workbench in the dropdown menu near the top taskbar.
    *   Select all the pockets (and the pad, but it's not necessary) with ctrl + a and click on the intersection (common) function.
    *   If an error dialogue pops up, it's because you had something other than the pockets and pad selected (such as a sketch). Click beside the parts list in the tree and try again.
    *   Waiting time varies by your computer's performance and the complexity of your plate, but expect it to be 5-20 minutes. Check out http://www.freecadweb.org/wiki/index.php?title=Part_Module if you can't find any of the operations mentioned above.

11.  The single result part should be called "common". It should be straight forward to export it to various formats. Exporting to .svg with a template may be something you want to do, but it requires a couple extra steps.

### Notes:

### 

The main limitation of the script at the moment is that it assumes that the switch is always in the exact middle of the key, according to the x, y, w, h values in the raw data. Keep this in mind when using non-rectangular keys or stepped keys, as they add secondary values which will be ignored. Despite this, switch placement seems to be correct for big-ass enter keys as well as ISO enter keys, since the templates of these keys included in the editor have proper x,y,w,h values. The assumed switch position may seem like a big problem for certain cases, but with clever manipulation of your layout, any possible plate can be made.

#### Here are some tips for dealing with some situations you may encounter:

1.  If you want cutouts on all four sides of the switch, copy all keys in the layout and place "!r!" in the label of each key in the copy layout. Then move the copy to overlap the original exactly. This way, the script will make two switch cuts for each key, and one will be rotated and thus you will have cutouts on all four sides of the switch.
2.  You may want a switch hole to be wide so as to accept multiple key positions or stem locations. For example, you want to accommodate spacebars with different non-standard stem positions, or you may want the plate to accept keys of multiple widths in one position. To accomplish this, add multiple 1x1 keys in the editor to widen the hole.
3.  Similarly, you may want to use keys with off-center stems such as a stepped caps lock key. To accommodate this, simply position the keys in the editor according to where you want the switch to be, not what the final appearance of the keyboard will be.