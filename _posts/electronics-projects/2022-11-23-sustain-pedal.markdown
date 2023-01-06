---
title:  "Building a sustain pedal (for my Yamaha DX7)"
date:   2022-11-23 00:00:00 +0100
categories: "electronics-projects"
description: "I have a Yamaha DX7."
---

I am a proud owner of a Yamaha DX7 digital synthesizer from 1984. It's essential that I mention that. Because the DX7 is a digital synthesizer, it does not naturally have the expression pedals of a physical acoustic piano. Compared to a real piano, the DX7 (and most other synthesizers) uses electronic expression pedals, which are just a simple switch. For example, take the sustain pedal. When it's activated, all notes played are "sustained", which is useful for playing chords. They can either be normally-closed or normally-open sustain pedals, which refers to their state when nothing is pressed. A normally-open switch will be disconnected when not pressed, and connected when pressed, while a normally-closed switch is the opposite. When the synthesizer outputs a signal, it checks whether the signal it outputs is the same as the signal it receives through the loop. The simplest way to do this is with an open-drain signal, where a resistor pulls up an input pin, and if the switch is closed, it connects it to ground. This way, it's easy to determine whether a switch is closed without any complex circuitry – many microcontrollers have open-drain and pullup capability built in.

<img src="{{ site.baseurl }}/images/sustain_connector.webp" alt="Image of the connector" style="display:block;margin:auto;">

Since I don't have a sustain pedal, and official Yamaha sustain pedals are currently around 80$, I decided to build one myself. In my parts bin I have a footpedal that I bought on a trip to Austria which has both a normally-closed and a normally-open output. This appeared like a perfect choice for me, as I  could add a switch to change the polarity of the pedal and use it for any synthesizer I want. So, I took around five minutes and built up the circuit using the pedal, some wires, a small DPDT switch, and a 3.5mm output jack. Connecting it to my Yamaha DX7, it worked immediately. Not only that, but I found out that when changing the polarity, I can have the sustain be turned on when the sustain is not pressed, while I can press the pedal to turn the sustain on. This is really useful, since I can play chords and have them sustained automatically, while I play a melody on another synthesizer. The total price in parts came out to be a tenth of the official price, and I get more satisfaction knowing I designed and built it myself. 

<img src="{{ site.baseurl }}/images/sustain_whole_pedal.webp" alt="Image of the pedal" style="display:block;margin:auto;padding-bottom:10px;">
<img src="{{ site.baseurl }}/images/sustain_DX7.webp" alt="Image of the pedal and the DX7" style="display:block;margin:auto;">

I have a Yamaha DX7.