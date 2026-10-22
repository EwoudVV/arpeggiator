# design

i want this to be a small desktop instrument that plays a chord as a repeating pattern. no computer or programming needed

## playing it

the 12 switches select notes from C to B. it plays the selected notes from low to high, then repeats. the octave selector makes it go through one, two or three octaves

start begins at the lowest selected note. stop mutes it. changing the notes takes effect on the next step, and changing the octave range restarts the pattern. with every note switched off, it stays quiet

the knobs control tempo, tuning, decay, tone and volume. there is also a saw/pulse switch. the output goes to powered speakers, an amplifier or an audio interface

## inside

a slow clock sets the tempo. a faster clock searches for the next selected note, and a register holds that note while it sounds

a resistor ladder sets the pitch voltage for an AS3340A oscillator. the octave switch adds a voltage offset. an envelope and LM13700 control the volume of each note, followed by the tone and volume controls

the PCB is 220 x 170 mm with four layers. the two inner layers are ground. most of the small parts are on the back, leaving the controls on the front

## case and power

the case will have a removable panel and room above the taller supply parts at the back. the switches and knobs stay in their current layout

it takes regulated 12 V DC through a centre-positive 5.5/2.1 mm connector. the board makes its own 5 V and -5 V supplies. the two regulator tabs are on different nets, so they can't share bare metal mounting hardware

once it's assembled, i'll tune the oscillator from C3 and check the notes across all three octaves
