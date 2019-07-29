GPIO Multiplexer with registers
================================

 * 1x32 bit buffer (AHCT245) to buffer all 28 GPIO bits plus 4 user bits
 * 2x32 bit registers (AHCT574) with user-choice of clock.
 * 6 NOT gates that can be used to create delays (e.g. to clock a register
   from a single GPIO write)

The chip packages are [DHVQFN20], which allows for compact design and is
still somewhat easy to solder if you use a stencil.

The clocks (`J6` and `J7`) of the registers are not connected by default, so
it allows you to choose any GPIO output or other signal to clock in the
registers. One way is to send a GPIO through a NOT gate as a delay, so a
single write to GPIO will allow to correctly save that state.

Using the NOT gates, you can also invert the clock signal to 'dual-data rate'
register storing: each write write will store one datum. Using the NOT gates as
delay line and inverter, no separate cycle is needed, each swing of the
clock generates a store.

So with three writes (which are [fairly quick] with > 130Mhz on the Rasperry Pi4
and about 65Mhz on the Pi3), you can output three register outputs with 28 bits
minus one used up for clock.

The buffer and registers are for 32 bits, but we only have 28 GPIO outputs.
The remaining bits are passed through as user bits (`U1` ... `U4`) from inputs
on the `J2` 'Raw' header.

PCB is [shared on OshPark].

![](img/board-render.png)
![](img/schematic.png)

[fairly quick]: https://github.com/hzeller/rpi-gpio-dma-demo
[DHVQFN20]: https://www.nexperia.com/packages/SOT764-1.html
[shared on OshPark]: https://oshpark.com/shared_projects/xJGfE6Gh