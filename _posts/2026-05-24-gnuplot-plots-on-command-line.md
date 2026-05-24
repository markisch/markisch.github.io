## Plots on the Command Line with gnuplot

Sometimes, plotting within a terminal window is required. gnuplot supports two different kind of devices:
* [real graphics output](#graphics-output) with the terminals kittycairo, kittygd, sixelgd, or sixeltek,
* [pseudo-graphics output](#pseudo-graphics-output) with the terminal dumb, block, or caca
Which one is the most suited, for one depends on the capabilities of the terminal program you are using, and your own preferences of course. 

## Pseudo-Graphics Output

All of the terminals in this section are capable of producing some pseudo-graphic text output. The [dumb terminal](dumb-terminal) is the oldest and makes use of the full character cell for every "pixel". The same is true for the [caca terminal](caca-terminal), but it can make use of a much larger character reportoire. The block terminal makes use of block or Braille characters to increase the resolution. 

All these terminal accept the `size` option to change the size of the output in characters.

### block terminal 

The block terminal generates pseudo-graphic output using Unicode block or Braille characters to increase the resolution. It requires a UTF-8 capable terminal or viewer. Drawing uses the simple internal bitmap code. It was introduced with gnuplot version 6.0. The output characters can be selected with the following options:
* `dots`: simple dots -- no enhancement of the resolution
* `half`: half-block characters increase the vertical resolution by two and are available in most fonts. In particular they are also available in the cp437 and cp850 encodings. Default on DOS and OS/2.
* `quadrants`: quadrant block characters yield double resolution in both directions. They are available since [Unicode 3.2](https://www.unicode.org/charts/PDF/Unicode-3.2/U32-2580.pdf) and with most fonts. This the default.
* `sextantants`: 2x3 block characters are available only since [Unicode 13](https://www.unicode.org/charts/PDF/Unicode-13.0/U130-1FB00.pdf). Font support is limited.
* `octants`: 2x4 block characters are available since [Unicode 16.0](https://www.unicode.org/charts/PDF/Unicode-16.0/U160-1CC00.pdf). Font support is limited.
* `braille`: 2x4 improvement in resolution using Braille characters. Available since [Unicode 3.0](https://www.unicode.org/versions/Unicode3.0.0/). Moderate font support.

The `sextpua` and `octpua` variants are special in that the make use of the characters in [Fairfax HD](https://www.kreativekorp.com/software/fonts/fairfaxhd/)'s PUA range. They only work with this font and also support terminal emulators which have problems with non-BMP characters (outside Plane 0).  

Support for colored output is shared with the dumb terminal. 

Below is an example from `simple.dem` using `octants mono size 100,30`:
```
  1.5 𜶖𜶙𜴳𜴳𜴳𜴳𜴳𜴳𜴳𜴳𜴳𜴳𜴳𜴳𜴳𜴳𜴳𜴳𜴳𜴳𜴳𜵎𜴆𜴔𜴆𜴆𜴆𜴆𜴆𜴆𜴆𜴆𜴆𜴆𜴆𜴆𜴆𜴆𜴆𜴆𜴆𜴆𜴆𜴆𜴆𜴣𜴆𜴆𜴆𜴆𜴆𜴆𜴆𜴆𜴆𜴆𜴆𜴆𜴆𜴆𜴆𜴆𜴆𜴆𜴆𜴆𜴆𜴣𜴆𜴆𜴆𜴆𜴆𜴆𜴆𜴆𜴆𜵁𜵁𜵁𜵁𜵁𜵁𜵁𜴔𜴔𜴔𜴔𜴔𜴔𜵈   
      ▐▐      sin(x) 𜴘𜴧𜴧𜴧𜴧𜴉▌                                        𜺣𜺣𜴉𜴉𜴉𜴉𜴀𜴀𜴀𜺨𜺨𜺨𜺨𜺨𜺨             ▌   
      ▐▐     atan(x) 𜴘𜴘𜴘𜴘𜴘 ▌                                  𜺣𜴉𜴀𜴀𜺨𜺨                            ▌   
      ▐▐cos(atan(x)) 𜴘𜴉𜴘𜴉𜴘𜴉▌                                𜴉𜴀                                  ▌   
    1 ▐𜴥𜴧𜴧𜴧𜴧𜴧𜴧𜴧𜴧𜴧𜴧𜴧𜴧𜴧𜴧𜴧𜴧𜴧𜴧𜴧𜴍 𜵑𜴜▂                  𜴘𜴉𜺠    𜵑𜴧𜴨𜺣                        ▂𜴧𜶀       𜴃▌   
      ▐                    𜺠𜴎   𜴠𜺣              𜴘𜴀   𜺨𜺠 𜵩𜺨  𜴄▖                     𜺠𜴒   𜴝𜺣      ▌   
      ▐                   𜺠𜴎     𜴠𜺣            𜴐       𜵬𜴶    ▝▖                   𜺠𜴎     𜴠𜺣     ▌   
      ▐                   𜵉       ▚          𜴘𜴀       𜵫𜺨𜺫𜺠    ▚                   𜵛       𜶗     ▌   
  0.5 ▐▖                 𜶖𜺨       ▝▖      𜺣𜴃𜺨        𜶖𜺨   𜺨𜴘𜺣 ▝▖                 𜺠𜴍        𜶅   𜴘▌   
      ▐𜶗                 𜵉         ▚  𜺣𜴘𜴉𜺫          𜺠𜴏       𜴃𜴀𜶗𜺣                ▞         ▝▖   ▌   
      ▐𜺫𜵈               𜵛    𜺠𜺣𜺠𜺣𜴘𜴉▝𜵈𜺫              ▞           𜶅𜺫𜴀𜴃𜴉𜺠𜺣𜺠𜺣       𜶖𜺨          𜶗   ▌   
      ▐𜺠𜷕𜴘𜴉𜴘𜴉𜴘𜴉𜴘𜴉𜴘𜴉𜴃𜴀𜴃𜴀𜵸𜴍𜴃𜺨𜺫𜺨       𜶗              ▗▘           ▝▖       𜺫𜺨𜺫𜺨𜴃𜴀𜴃𜵉𜴃𜴀𜴃𜴉𜴘𜴉𜴘𜴉𜴘𜴉𜴘𜴋𜶿𜺣𜺠▌   
    0 ▐𜴉 ▌             ▞             ▌             𜵛             𜶗             𜵛             𜶗 𜴘▌   
      ▐  ▐            𜶖𜺨             𜴡𜺣           𜺠𜴍             𜺫𜵈           ▗▘             𜺫𜵈 ▌   
      ▐   ▌           ▌               ▚           𜵛               ▐           ▞               𜶗 ▌   
      ▐   𜴡𜺣         𜵛                𜺫𜵈         ▗▘                𜶅         𜶖𜺨                ▌▌   
 -0.5 ▐𜴉   ▚        ▗▘                 𜴡𜺣        𜵊                 𜴡𜺣        ▌                 𜴡▌   
      ▐    𜺫𜶄       ▞                   𜶅       𜵫                   𜶅       ▐                   ▌   
      ▐     𜺫𜶄     ▗▘                   𜴡𜺣     𜵫𜺨                   𜺫𜶄     ▗▘                   ▌   
      ▐      𜺫𜶄   𜵑▘                     𜴠𜺣   𜵫𜺨                     𜺫𜶄   ▗▘                    ▌   
   -1 ▐𜺣       𜴝𜴐𜴆𜺨                       ▝𜴧𜴧𜴒𜺨                       𜺫𜴜𜶀𜴐𜺨                    𜺠▌   
      ▐                                  𜺠𜴘𜺫                                                    ▌   
      ▐                             𜺠𜺠𜴘𜴘𜴃                                                       ▌   
      ▐                   𜺠𜺠𜺠𜴘𜴘𜴘𜴘𜴃𜴃𜺫                                                            ▌   
 -1.5 ▐𜷋𜷋𜷋𜷋𜷋𜷋𜶳𜶳𜶳𜶳𜶳𜶳𜶳𜶭𜶭𜶭𜶭𜶭𜶭▂▂▂𜶻▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂𜷋▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂𜷋▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▌   
     -10                    -5                     0                     5                     10  
```
### dumb terminal

The dumb terminal was introduced way back in gnuplot version 3.0 to support "dumb" terminals without graphical capabilities. It received support for enhanced text in version 4.0, for UTF-8 characters in version 4.6, and color support in version 5.2. Color support requires the support of [ANSI escape sequences for colors](https://en.wikipedia.org/wiki/ANSI_escape_code#Colors). 

### caca terminal


## Graphics Output
Today, many terminal emulator programs support some sort of graphical inline output. Historically, [sixel graphics] was supported by some [DEC terminals](https://vt100.net/docs/vt3xx-gp/chapter14.html). The kitty* terminals support the newer graphics interface introduced by the [KiTTY terminal](https://sw.kovidgoyal.net/kitty/). Both formats are supported by a growing number of terminal emulators.

### kittycairo and kittygd terminals

### sixelgd and sixeltek terminals

The sixelgd and sixeltek gnuplot terminals create sixel graphics output. Internally, they use either the superior [libgd library](https://libgd.github.io/), or gnuplot's own bitmap routines. For the status of sixel support in terminal emulators see [https://www.arewesixelyet.com/](https://www.arewesixelyet.com/). 


