## Plots on the Command Line with gnuplot

Sometimes, plotting within a terminal window is required. gnuplot supports two different kind of devives:
* [real graphics output](#graphics-output) with the terminals kittycairo, kittygd, sixelgd, or sixeltek,
* [pseudo-graphics output](#pseudo-graphics-output) with the terminal dumb, block, or caca
Which one is the most suited, for one depends on the capabilities of the terminal program you are using, and your own preferences of course. 

## Pseudo-Graphics Output

### block terminal 

### dumb terminal

### caca terminal


## Graphics Output
Today, many terminal emulator programs support some sort of graphical inline output. Historically, [sixel graphics] was supported by some [DEC terminals](https://vt100.net/docs/vt3xx-gp/chapter14.html). The kitty* terminals support the newer graphics interface introduced by the [KiTTY terminal](https://sw.kovidgoyal.net/kitty/). Both formats are supported by a growing number of terminal emulators.

### kittycairo and kittygd terminals

### sixelgd and sixeltek terminals

The sixelgd and sixeltek gnuplot terminals create sixel graphics output. Internally, they use either the superior [libgd library](https://libgd.github.io/), or gnuplot's own bitmap routines. For the status of sixel support in terminal emulators see [https://www.arewesixelyet.com/](https://www.arewesixelyet.com/). 


