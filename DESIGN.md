# design

## playing it

the 12 note switches cover C through B. the selected notes play from low to high. the octave selector chooses a span of one, two or three octaves. after the highest selected note in the highest octave, the pattern wraps to the lowest selected note in the lowest octave

one selected note repeats on every step. with more than one octave selected, it moves through those octaves. switching every note off mutes the output

start begins at the lowest selected note in the lowest octave. stop mutes the output. changing the octave range restarts the pattern on the next step. note switch changes take effect on the next step, without moving the pitch partway through a sounding note

the tempo target is roughly 40-240 BPM with two notes per beat. the knob scale will be approximate. the base pitch target is C3 through B3, extending to B5 with three octaves selected. the tune knob shifts the whole instrument together

## circuit

use a regulated 5 V rail for HC logic. a fast internal clock runs the note search independently of the tempo clock. counter changes and note capture must happen on separate clock phases so the switch multiplexer has time to settle

at each step, capture the note switch states and octave range. advance the search counter until it reaches an enabled note. then copy the note and octave into the output register. the pitch multiplexer and note LEDs use this register, not the searching counter

the search is bounded. it must finish in less than 2 ms at the slowest allowed internal clock. no notes selected, invalid states, stop and power-up must all leave the amplifier muted. another tempo edge during a search must not trigger a second note

use 1 V per octave for the pitch control. the 12 pitch choices are 0, 1/12, 2/12 through 11/12 V. add 0, 1 or 2 V for the octave. a high-input-impedance buffer keeps the analog switch from loading the resistor ladder. provide tuning and scale trimmers, plus pitch and reference test points

the sound circuit uses an analog oscillator with sawtooth and pulse outputs, a decay envelope, a voltage-controlled amplifier, a simple low-pass tone control and an AC-coupled output buffer. the jack is a line output for powered speakers, an amplifier or an audio interface

the sequencer uses 74HC163 counters and HC registers, with a 74HC4067 reading the note switches. pitch selection uses an ADG706, a buffered resistor ladder and a separate octave switch. the oscillator is an AS3340A. each step charges the envelope capacitor, then it decays through the decay knob. the LM13700 controls the volume before the tone control and line buffer

the ladder resistors are 0.1%. the reference divider and pitch input ratios use 0.01% resistors. the oscillator has coarse, scale, temperature-compensation and high-frequency tracking trimmers. these need setting on the finished board, starting at C3 and checking each octave. the front-panel tune knob covers about two semitones in total

this is still unbuilt. the envelope and amplifier have been checked with circuit models, but the oscillator has not been measured or calibrated. the next schematic work is the main power supply and connector protection. the controls, film capacitors and jack still need exact parts and footprints

## power and case

use an external regulated 12 V DC adapter with a centre-positive barrel connector. use +12 V and -5 V for the analog circuits, with a separate 5 V logic rail. the negative-rail circuit still needs a load and noise calculation. include reverse-polarity protection, decoupling and a power-on reset

one custom PCB carries the circuit and controls. put the audio and power connectors at the back, the note switches in a piano arrangement, and the knobs above them. the case needs screw mounting, knob clearance and access to the calibration trimmers. PLA or PETG on the P1S
