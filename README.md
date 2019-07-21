GPIO Multiplexer with registers
================================

 * 1x32 bit buffer (AHCT245) to buffer all 28 GPIO bits plus 4 user bits
 * 2x32 bit registers (AHCT574) with user-choice of clock.
 * 6 NOT gates that can be used to create delays (e.g. to clock a register
   from a single GPIO write)

![](img/board-render.png)
![](img/schematic.png)

