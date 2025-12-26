# MicroPython Driver for the Waveshare Pico OLED 1.3

A MicroPython driver for the [Waveshare Pico-Oled-1.3](https://www.waveshare.com/product/pico-oled-1.3.htm) derived from the one provided by Waveshare, forked from [samveen](https://github.com/samveen/pico-oled-1.3-driver)

## Features

- Derived from the MicroPython Driver for the pico OLED 1.3 by Waveshare.
- Initialization and access to the state of `key0` and `key1` via the display object.
- Better character display capabilities:
  - Better fixed and variable width fonts than the build-in font provided by `framebuf`.
  - Better `text` function:
    - Automatic wrapping of text.
    - Returns endpoint coordinates of last written character.

Improvements on my fork

- Much faster display updating (improved from ~11hz to ~60hz with a simple loop)
- Auto clearing of the display between uses of `display.show()`

## Usage

- Connect the display to the Raspberry Pi Pico.
- Flash the Pico W with the latest MicroPython.
- Copy the codebase to the Raspberry Pi Pico /lib folder to a folder named `PicoOled13`.
- Use as below:

```
import PicoOled13

display=PicoOled13.get()
display.clear()

if display.is_pressed(display.KEY0):
    display.text("Key0 pressed",0,0,0xffff)
elif display.is_pressed(display.KEY1):
    display.text("Key1 pressed",0,0,0xffff)
else:
    display.text("No key pressed",0,0,0xffff)

display.show()

```

You can directly use any of the commands built into [framebuf](https://docs.micropython.org/en/latest/library/framebuf.html) via the display object, e.g.

```
import PicoOled13
import array
display=PicoOled13.get()

display.rect(5,5,10,10,0xffff,True)
display.ellipse(100,20,5,5,0xffff)

myData = array.array('I', [0,0,20,30,30,23])
display.poly(5, 30, myData, 0xffff)

display.show()
```

## Acknowledgements

- Samveen's [original code](https://github.com/samveen/pico-oled-1.3-driver) this was forked from

- Pico-oled-1.3 driver by [Waveshare](https://www.waveshare.com/wiki/Pico-OLED-1.3#Examples)

- [Much nicer fonts](https://github.com/markwinap/Pycom-SH1107-I2C/blob/master/lib/SH1107.py) as compared to the [blox](https://github.com/micropython/micropython/blob/master/extmod/font_petme128_8x8.h) provided by framebuf.
