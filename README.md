# Arpeggiator

a standalone arpeggiator made from analog circuits and logic chips. no microcontroller or firmware

there are 12 note switches, arranged like one octave of a piano. turn on the notes in a chord and it plays them in ascending order. a 1/2/3-octave selector sets how many octaves it plays before repeating

with C, E and G selected, the two-octave setting plays C, E, G, then the same notes an octave higher, then starts again

## controls

- 12 latching note switches and note LEDs
- 1/2/3-octave range selector
- tempo knob and start/stop button
- tuning, decay, tone and volume knobs
- sawtooth/pulse waveform switch
- mono line output on a 3.5 mm jack
- external DC power

## how it works

a clock sets the pace. a counter and logic circuit find the next selected note, skipping notes that are switched off. the note and octave are saved in a register so the pitch stays steady between steps

a precision voltage reference and resistor ladder set the note voltages. the selected voltage, plus an octave offset, controls an analog oscillator. an envelope controls each note's volume, followed by the tone control and output buffer

the controls and connectors will fit into a printed desktop case. the plan is one custom four-layer PCB, with through-hole controls and larger surface-mount parts where practical

## progress

the PCB is routed. it's 220 x 170 mm, with four layers. the controls are on the front and most of the circuit is on the back

i started with two layers, but fitting all the ground connections around the signal tracks was getting awkward. the two inner ground planes made that much easier

the printed case is drawn too, with a removable rear cover for tuning. board and parts quotes are next

[parts list](BOM.csv)

![case](images/case-assembly.png)

![PCB render, front](images/pcb-front.png)

![PCB render, back](images/pcb-back.png)

some of the controls don't have 3D models yet

![Sequencer schematic](images/sequencer.png)

![Pitch reference and ladder](images/pitch-reference.png)

![Oscillator schematic](images/oscillator.png)

![Input power and 5 V supply](images/power-supply.png)

## files

open [arpeggiator.kicad_pro](arpeggiator.kicad_pro) in KiCad. the [main schematic](arpeggiator.kicad_sch) links the circuit sheets in [schematic](schematic)

[arpeggiator.kicad_pcb](arpeggiator.kicad_pcb) is the routed board. the [case files and assembly notes](case) include the FreeCAD model, STEP assembly and printable STLs

[design notes](DESIGN.md)

[journal](JOURNAL.md)

[Half Life project](https://halflife.hackclub.com/projects/cmvfhc9ih000001o8aysnkf0b)

*made for Hack Club Half Life, music week*
