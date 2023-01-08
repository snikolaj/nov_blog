---
title:  "Crafting the USB-MIDI converter of my dreams!"
date:   2023-01-08 00:00:00 +0100
categories: "electronics-projects"
description: "A year and one hour in the making..."
---

I love music and I love synthesizers. I’ve already written this introduction in a previous blog post. At the time of writing, I have five synthesizers – Yamaha DX7, Korg M1, Yamaha Reface CS, E-mu Proteus/1 XR and Korg Volca Drum (it counts). Most of them are very old and made before the time computer-synthesizer communication was seen as societally acceptable. In fact, the DX7 technically came out before MIDI existed, meaning that its MIDI implementation is a bit strange. USB? Forget about it. The DX7, temporally, is as far from USB as it is from the PDP-11. 

However, I can’t play five synthesizers at once. Usually, people use a MIDI sequencer for this, like the Arturia BeatStep Pro (like one of my favorite youtuber/musicians Look Mum No Computer, who uses many of them), but they’re 300$ each and I’d need multiple. So, as always, to the workbench I go.

Honestly, I’ve been trying to crack the issue of USB-MIDI communication for almost a year now. It’s not that I haven’t done it, it’s just that all of my previous attempts were somehow limited. The farthest I got is with the PIC16F1459 (a favorite over here), where I had practically everything working, but eventually gave up because of it having only one MIDI (UART) connection. I couldn’t emulate another UART since the anemic PIC architecture was already being pushed to its limits by my processing code. 

I was in the city where the only two electronics stores in the country are, visiting some close friends, and decided to randomly buy a Raspberry Pi Pico. When I returned and looked for a problem to fix with my solution, I found out that Adafruit (the guys who make most of the notable Arduino libraries) had actually made a USB MIDI library for the Pico, in Python. Now, I hadn’t used Python in a month, but just strolling through the mediocre documentation and two examples, I instantly managed to get code up and running for one MIDI channel, in around 20 lines of code. In comparison, the PIC code that took around a month to write had many thousands of lines of code, of which I personally wrote around 1000 and the rest is incomprehensible USB library code. 

```python
import board
import busio

import time
import usb_midi
import adafruit_midi

from adafruit_midi.timing_clock import TimingClock
from adafruit_midi.channel_pressure import ChannelPressure
from adafruit_midi.control_change import ControlChange
from adafruit_midi.note_off import NoteOff
from adafruit_midi.note_on import NoteOn
from adafruit_midi.pitch_bend import PitchBend
from adafruit_midi.polyphonic_key_pressure import PolyphonicKeyPressure
from adafruit_midi.program_change import ProgramChange
from adafruit_midi.start import Start
from adafruit_midi.stop import Stop
from adafruit_midi.system_exclusive import SystemExclusive
from adafruit_midi.midi_message import MIDIUnknownEvent

uart_1 = busio.UART(tx=board.GP0, rx=board.GP1, baudrate=31250, timeout=0)
uart_2 = busio.UART(tx=board.GP4, rx=board.GP5, baudrate=31250, timeout=0)

usb_midi = adafruit_midi.MIDI(midi_in=usb_midi.ports[0], in_channel=None, midi_out=usb_midi.ports[1], out_channel=0, in_buf_size=1024)

uart_midi_1 = adafruit_midi.MIDI(midi_in=uart_1, in_channel=0, midi_out=uart_1, out_channel=0, in_buf_size=1024)
uart_midi_2 = adafruit_midi.MIDI(midi_in=uart_2, in_channel=1, midi_out=uart_2, out_channel=1, in_buf_size=1024)

while True:
    usb_msg = usb_midi.receive()
    if usb_msg is not None and isinstance(usb_msg, MIDIUnknownEvent) is False:
        if usb_msg.channel == 0:
            print("Received on USB 1:", usb_msg, "at", time.monotonic())
            uart_midi_1.send(usb_msg)
        if usb_msg.channel == 1:
            print("Received on USB 2:", usb_msg, "at", time.monotonic())
            uart_midi_2.send(usb_msg)

    uart_msg_1 = uart_midi_1.receive()
    if uart_msg_1 is not None and isinstance(uart_msg_1, MIDIUnknownEvent) is False:
        print("Received on UART 1:", uart_msg_1, "at", time.monotonic())
        usb_midi.send(uart_msg_1)

    uart_msg_2 = uart_midi_2.receive()
    if uart_msg_2 is not None and isinstance(uart_msg_2, MIDIUnknownEvent) is False:
        print("Received on UART 2:", uart_msg_2, "at", time.monotonic())
        usb_midi.send(uart_msg_2)
```

Emboldened by this initial success, I went and built a board to house the Pico, two MIDI channels and associated circuitry. I used fully standard, MIDI spec circuits and components, except for the optocouplers – which were 6N137 instead of 6N138, which should allegedly be worse but I’ve never had them malfunction. At least not at the very slow 31250 baud midi rate. I built the MIDI output circuit with an NPN transistor since I wanted my circuit to be compact and an entire DIP inverter IC does not fit into that definition. However, the NPN transistors invert the signal, while CircuitPython has no way of inverting the UART, even though that’s present in practically every modern microcontroller. As a result, I had to add a bodge transistor inverter, which means that I probably could have fit a DIP inverter in there regardless. In the end, it turned out fine. I promptly added interfacing circuitry for another MIDI channel and everything worked perfectly.

<img src="{{ site.baseurl }}/images/pi_pico_midi_schematic.webp" alt="Schematic of the Pico MIDI" style="display:block;margin:auto;">

One issue I had during the code writing was a significant delay between pressing notes on the keyboard and them appearing on the screen. From USB → UART there was no delay, but UART → had a one second delay. This wasn’t actually between the microcontroller and the PC, as often happens (due to operating system overhead) – it was actually between UART reception and microcontroller. It turns out that the library had its own timeout function for the UART which defaulted to one second. Fixing this made it work perfectly, with a total delay of around 30ms – as good as any other USB-MIDI converter on the market. 

<img src="{{ site.baseurl }}/images/pi_pico_midi.webp" alt="Image of the finished build" style="display:block;margin:auto;">

Now, all that’s left to do is to add more UART channels using the PIO, which should allow me to make more MIDI channels than I have synthesizers. Due to the simplicity of the output circuitry, all I would need are more connectors and board space, while the extremely fast Pi Pico plus PIO handles everything else. So far, I’m extremely impressed by the Pico and plan on buying many more – I just need to find a good source.

[Link to the Github repository](https://github.com/snikolaj/pico_midician)

One interesting thought is how previously I planned on turning my PIC16F1459-based project into something much more complex in order to expand its capabilities. I designed a bus system with multiple 8051s handling UARTs and buffering and timing and eeeeverything. Now, one tiny chip – cheaper than the PIC alone – replaced all of that, using an even slower programming language. Technology truly is amazing. Yet, it’s scary how fast something like a PIC can become obsolete. Even though PICs are very old in technological terms, they’re still only 40 years old. I can’t imagine equipment built in the 1380s becoming obsolete in the 1420s, and even recently weapons and technology from WW1 saw use in WW2, some are even still in use today. Yet, it depends on the technology as well. I can’t wait to see what the future holds, if this is how far we have gone – even though I’m very scared as well.