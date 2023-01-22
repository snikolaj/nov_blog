---
title:  "Project Videosex Intro"
date:   2023-01-22 00:00:00 +0100
categories: "project-Videosex"
description: "Introducing Project Videosex"
---
<script src="https://cdn.jsdelivr.net/combine/npm/tone@14.7.58,npm/@magenta/music@1.22.1/es6/core.js,npm/focus-visible@5,npm/html-midi-player@1.4.0"></script>

## Project Videosex

For those who don’t understand the title – there’s a famous Slovene synthpop group from the 80s called Videosex. In my opinion – and that of my friends – they are one of the best synthpop groups ever, and it’s easy to see why. Compared to western synthpop groups, their songs are quite complicate in their arrangement and sound effects. Yet, outside of former Yugoslavia, they remain completely unknown. 

The aim for Project Videosex is to be a recreation of the Videosex sound from scratch. The goal is to deconstruct every song, find every instrument, and play them as if I were the band myself. This may sound ambitious – and it very much is – but I can’t help but see it as a challenge for myself and an opportunity to showcase my skills in both electronics and music. To this end, the project outline goes as follows:
- write down the sheet music for all the Videosex songs I like (playlist link) and possibly one more
- recreate all the instruments and samples used
- hopefully get to perform live

I actually started this project a couple of months ago and have finished some of the work so far. Out of the 8-9 songs I plan to recreate, I have 1 mostly done (Tko Je Zgazio Gospodju Mjesec) and 2 halfway done (Stakleno Nebo, Videosex). For me, it was most important to get the basslines transcribed, as the chords and melodies can be inferred from the bassline. The ones I think will take me the longest to finish are Stakleno nebo and Pejd ga pogledat anja – in general, the album Lacrimae Christi has more complex arrangements.

Below are some of the bassline transcriptions in MIDI (skip forward if they don't start playing):
<a href="{{ site.baseurl }}/midi/Videosex - Stakleno Nebo bas.mid">Stakleno nebo bassline (click to download)</a>
<midi-player src="{{ site.baseurl }}/midi/Videosex - Stakleno Nebo bas.mid" sound-font visualizer="#myVisualizer1">
</midi-player>
<midi-visualizer type="waterfall" id="myVisualizer1"></midi-visualizer>
<a href="{{ site.baseurl }}/midi/Videosex - Tko Je Zgazio Gospodju Mjesec bas.mid">Tko Je Zgazio Gospodju Mjesec bassline (click to download)</a>
<midi-player src="{{ site.baseurl }}/midi/Videosex - Tko Je Zgazio Gospodju Mjesec bas.mid" sound-font visualizer="#myVisualizer2">
</midi-player>
<midi-visualizer type="waterfall" id="myVisualizer2"></midi-visualizer>


### Equipment

The next step is finding out the instruments used, which was quite fun to do. Since Videosex was active in the mid 80s, they had an arsenal of then-modern synths at their disposal. As a vintage synth enthusiast myself, I was able to find out some of the synths they used through recognizing samples. So far, I have been able to discover:
- Yamaha DX7 Tubular Bells in Pejd ga pogledat anja (Lacrimae Christi)
- E-mu Emulator Choir in Stakleno nebo (Lacrimae Christi)
- Korg MonoPoly in Kako Bih Volio Da Si Tu (Videosex84)
- Korg PolySix in Kako Bih Volio Da Si Tu (Videosex84)

In one of the rare live performances of Videosex, the one of Kako Bih Volio Da Si Tu, they use at least 4 Korg analog synths, which are also heavily used in Lacrimae Christi (which I consider their best album). I’ve not been able to identify their drum machine(s) and sequencer – which they do actually use. It’s possible that the drum machine is a Linndrum, but it just sounds like any generic 80s lo-fi sample-based drum machine.


### Going DIY

I already have a DX7, but my ideas for the Emulator and PolySix are quite a bit more ambitious. Both synths are extremely expensive on the used market, but their mode of operation is actually pretty simple. My idea is to recreate both synths using newer electronics which would drastically simplify them. An Emulator can be recreated with practically one FPGA and the assorted analog filtering, while the PolySix uses a lot of digital controls which can all be replaced with a single microcontroller. Its famous analog chorus section can also be simplified by using microcontrollers to drive the BBDs. However, I would need a lot of time and resources to recreate these, and a simpler way to do this would be to take the case of one of those synths, smack in a laptop motherboard and automatically load the respective VSTs on it. Then, have a board with a PIC16F1459 as a MIDI controller which maps the potentiometers and switches directly to the VST. An x86 SBC would also do the job. For the sequencer, a laptop with FL Studio would work just fine.

For the hardware part some effort has been made already. I’ve built a USB-MIDI converter based on the Raspberry Pi Pico to control my synths from a PC and vice versa, while my analog and digital design skills have improved considerably. I now feel very confident in analysing the circuits of these vintage synths and can generally optimize wherever needed. I’ve designed a PIC16F1705 sample and hold circuit and I’m in the process of building a PIC12F1501 BBD clock driver. These are essential for the PolySix project, while on the Emulator side, I’ve been learning VHDL on and off, mainly due to lack of FPGA. It may not be necessary, but I’ve also built 5 audio amplifiers of varying power, as well as linear power supplies. If needed, I could also build the necessary stage lighting and have the whole setup be completely mine. Still, the main bottleneck remains the funding, even though it’s a fun challenge to overcome. I’d still like all this to be finished by summer 2023. 


### Longing...

I can play all the songs through either my keyboards or VSTs, have a sequencer accompany me while I play two keyboards, and everything will be fine on that end, however I also need to find someone to sing. The appeal of Videosex was the main singer – Anja Rupel. In her late teens at the time, she was provocative, she was cool, she was sexual and she openly talked about it in a culture that would rather have pretended sex didn’t exist if it wasn’t done to make more cannon fodder for the state. I know someone who fits this profile well, though the issue of actually getting all my work done on time is definitely the main problem at the moment. I might forgo the process of building the synths myself and rather use the VST idea combined with the synths I already have. I might even go for a hybrid approach, as long as I can get this done on time. I also hope that my DX7 will survive until then, as it’s an early model and it’s been regularly used for almost 40 years. I fear for its long-term health, even though it’s been serviced over the years.

Regardless, this project has been a massive learning opportunity for me and I’ve learned a ton from it. It’s amazing how applicable the lessons of analog and digital synth design are in other fields – since it’s basically just signal conditioning, measurement and generation. On the way, I’ve gotten to experience and enjoy the best synthpop Yugoslavia had to offer, while expanding my skills in the hobbies I love. Even though this year has been going pretty badly so far, I hope I can get this project done!