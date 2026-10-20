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

the controls and connectors will fit into a printed desktop case. the plan is one custom two-layer PCB, with through-hole controls and larger surface-mount parts where practical

## progress

the sequencer, sound circuit and power supply are drawn. the supply has a fuse, reverse-polarity protection and separate 5 V and -5 V regulators. the logic stays in reset until the input and both rails are ready, and a switch mutes the line output while stopped

i checked the rail loads, regulator heat and reset thresholds, then ran the sequencer and envelope checks again. ERC is clean. nothing has been built or tuned yet

[BOM.csv](BOM.csv) is the current parts list. the chips and calibration parts are selected. the front controls, a few capacitors and their footprints still need finishing, and prices have not been quoted yet

![Sequencer schematic](images/sequencer.png)

![Pitch reference and ladder](images/pitch-reference.png)

![Oscillator schematic](images/oscillator.png)

![Input power and 5 V supply](images/power-supply.png)

## files

open [arpeggiator.kicad_pro](arpeggiator.kicad_pro) in KiCad. the [main schematic](arpeggiator.kicad_sch) links the circuit sheets in [schematic](schematic)

the files are still a schematic design in progress. there is no PCB layout, case or fabrication package yet

[design notes](DESIGN.md)

[journal](JOURNAL.md)

[Half Life project](https://halflife.hackclub.com/projects/cmvfhc9ih000001o8aysnkf0b)

*made for Hack Club Half Life, music week*
