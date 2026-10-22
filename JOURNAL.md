# journal

## October 19, 2026

10 hours

Devlog 01: sequencer circuit

started the arpeggiator for music week. i'm making it with analog circuits and logic chips, with no microcontroller. settled on 12 note switches and a selector that repeats the chosen notes across one, two or three octaves. set up the repo and Half Life project too

drew the sequencer in KiCad, including the switch inputs, clocks, counters, octave selection, start/stop and note LEDs. one clock sets the tempo and a much faster one searches for the next enabled note. a separate register holds the sounding note steady while that search happens

added a settling step before triggering each note, then put the trigger through a register so a brief glitch from the state decoder won't become an extra note. also added reset and mute behaviour for an empty selection or an invalid state

checked the exported connections and tested the clocked model with every note-switch combination and octave range. also checked changing the selection, stopping during a search and restarting. ERC is clean for this section. these are circuit and model checks, not physical tests

looked into the pitch-voltage parts too. ordinary analog switches can leak enough current to affect the tuning, so i'm planning a precision switch and 0.1% resistors for that section. the sound circuit, main supply, PCB and case are next. nothing built yet

![sequencer](https://halflife.hackclub-assets.com/hackclub-half-life/sessions/6gi99sjgqS9PS6AP7HOtnbXmi9NgjIY3/5c3d950de13fef77f24d30623af3024cae4abf79afe6e5b7342f8184f6bb63a6.png)

![note-switches](https://halflife.hackclub-assets.com/hackclub-half-life/sessions/6gi99sjgqS9PS6AP7HOtnbXmi9NgjIY3/1a594df704688a5b3df4a3c2c8dca755027ba572a2cd86128f698aab9bcb33f8.png)

![arpeggiator-03_clock_range](https://halflife.hackclub-assets.com/hackclub-half-life/sessions/6gi99sjgqS9PS6AP7HOtnbXmi9NgjIY3/b80c8514bacc6f287c7672f53e72dcb51e569ef7c5832f44623d1ea9c07ead62.png)

![arpeggiator-04_input_registers](https://halflife.hackclub-assets.com/hackclub-half-life/sessions/6gi99sjgqS9PS6AP7HOtnbXmi9NgjIY3/3325a934afd82361caca34aca01ed8aee9c72ef0ef8ac352c0c51c16db71aea2.png)

![arpeggiator-06_pitch_register](https://halflife.hackclub-assets.com/hackclub-half-life/sessions/6gi99sjgqS9PS6AP7HOtnbXmi9NgjIY3/05098a8e2c084688202670edd1dfd551351f5b6a798bc1853a1a9771a3f3cea7.png)

![arpeggiator-events](https://halflife.hackclub-assets.com/hackclub-half-life/sessions/6gi99sjgqS9PS6AP7HOtnbXmi9NgjIY3/f5b78b88bb8a5bd824eeb858d9fd6be8338eac2e7d79deb91dad2ea27cb15c56.png)

![arpeggiator-logic_02](https://halflife.hackclub-assets.com/hackclub-half-life/sessions/6gi99sjgqS9PS6AP7HOtnbXmi9NgjIY3/283208d0361607374004e7c90265a232f37a49c441f6f8b9898593fc57d98d4c.png)

![arpeggiator-logic_03](https://halflife.hackclub-assets.com/hackclub-half-life/sessions/6gi99sjgqS9PS6AP7HOtnbXmi9NgjIY3/d183b213f6ce65c6747667813022765f616a14ba2152cfbd2e26fc3711453b0a.png)

![arpeggiator-logic_05](https://halflife.hackclub-assets.com/hackclub-half-life/sessions/6gi99sjgqS9PS6AP7HOtnbXmi9NgjIY3/2e96a1fdc59e3134bceac272b534890ca64b199a6d6bed82a7cd14eeb40fbfe2.png)

![arpeggiator-logic_06](https://halflife.hackclub-assets.com/hackclub-half-life/sessions/6gi99sjgqS9PS6AP7HOtnbXmi9NgjIY3/7dee605eb502951ddd9abf63b8deae53fa63481804465bd96e2485126c97b93c.png)

## October 19, 2026

4 hours

Devlog 02: pitch and sound circuit

added the part that turns the note numbers into sound. the note register selects a voltage from the resistor ladder, and a second switch selects the octave. both go into the AS3340A oscillator, with trimmers for tuning and tracking

the saw and pulse outputs feed an LM13700 amplifier. each note charges an envelope capacitor, then the decay knob controls how quickly it fades. stop discharges that capacitor too. after the amplifier there is a simple tone control, volume knob and a mono line output

i checked the reference and resistor values, and ran models of the envelope and amplifier current source. i also went back through the sequencer checks with the sound circuit connected. the schematic passes ERC. the oscillator will still need tuning and checking once the board exists

next is finishing the power supply and choosing the actual controls and parts before laying out the PCB

![arpeggiator-10_oscillator](https://halflife.hackclub-assets.com/hackclub-half-life/sessions/6gi99sjgqS9PS6AP7HOtnbXmi9NgjIY3/5bab5607ed1cafcc0af53510267b00c73ed498d59be1f3e56925a7780158311f.png)

![arpeggiator-11_envelope](https://halflife.hackclub-assets.com/hackclub-half-life/sessions/6gi99sjgqS9PS6AP7HOtnbXmi9NgjIY3/7beec83c31ef23782737abcae0466e96fe464cb95045156b4d98abc053dc0add.png)

![arpeggiator-12_amplifier](https://halflife.hackclub-assets.com/hackclub-half-life/sessions/6gi99sjgqS9PS6AP7HOtnbXmi9NgjIY3/6f09bcc8a226bab84e07c7f3538d816fd879706715352afc52755cfc94dbd909.png)

![arpeggiator-08_reference](https://halflife.hackclub-assets.com/hackclub-half-life/sessions/6gi99sjgqS9PS6AP7HOtnbXmi9NgjIY3/4422dca6d49914f7962e57559342c27781d8f3708900a712ffeabb2d0b5f53d7.png)

## October 20, 2026

8 hours

Devlog 03: power supply and reset

added the power supply. the 12 V input has a fuse and reverse-polarity protection. a 7805 supplies the logic, and an LT1054 charge pump feeds a 7905 for the negative analog rail

added checks for the input voltage and negative rail alongside the existing 5 V reset. the sequencer stays reset until the supplies are ready. a switch mutes the line output while stopped, and the envelope discharge circuit now runs from 12 V so it still works if 5 V disappears

checked the current and heat estimates and reset thresholds, and ran models of a few startup and power-loss cases. also checked stopping partway through the envelope's charge pulse and restarting without an extra note. the sequencer checks still pass and ERC is clean. the switching supply and startup behaviour still need checking on the real board

started the BOM and found sources for the main chips and calibration parts. the AS3340A will use a DIP package, which should be easier to solder and replace. the front controls, a few capacitors and their footprints are next, then PCB placement

![arpeggiator-15_input_power](https://halflife.hackclub-assets.com/hackclub-half-life/sessions/6gi99sjgqS9PS6AP7HOtnbXmi9NgjIY3/f50ef49e945bdad348842ec502f81468a8e66bae65f8fc4c75fab42bb9e29e3b.png)

![arpeggiator-16_negative_supply](https://halflife.hackclub-assets.com/hackclub-half-life/sessions/6gi99sjgqS9PS6AP7HOtnbXmi9NgjIY3/e0fde0ace1f0c04a7e49872f1b97824ca7c0d8c27958c778b57cc2724a81eacf.png)

![arpeggiator-17_negative_monitor](https://halflife.hackclub-assets.com/hackclub-half-life/sessions/6gi99sjgqS9PS6AP7HOtnbXmi9NgjIY3/636c4eb3daaf48815080ba7652c8ab976aa370900ee7965f8e162b8d9af06aa4.png)

![arpeggiator-18_input_monitor](https://halflife.hackclub-assets.com/hackclub-half-life/sessions/6gi99sjgqS9PS6AP7HOtnbXmi9NgjIY3/3ade83e2e5f28bfea5e24a91f7b15248669a27e8a476eb42547a6c99cbb8f57d.png)

![arpeggiator-19_reset_output](https://halflife.hackclub-assets.com/hackclub-half-life/sessions/6gi99sjgqS9PS6AP7HOtnbXmi9NgjIY3/525372d6761e2710cc0c26f53c5683271351f1b72b82012fd06a2f68435d2e14.png)

![arpeggiator-13_line_output](https://halflife.hackclub-assets.com/hackclub-half-life/sessions/6gi99sjgqS9PS6AP7HOtnbXmi9NgjIY3/198f803fa44ece243822d13664c7f574c6b14bd1fa4b723a5868be44bf71f1af.png)

![arpeggiator-14_analog_power](https://halflife.hackclub-assets.com/hackclub-half-life/sessions/6gi99sjgqS9PS6AP7HOtnbXmi9NgjIY3/7929b9fdf7af5a387d7b738c1dfa5ed854fb42b0122a98155c06f6b6b1fd3986.png)

![arpeggiator-10_oscillator](https://halflife.hackclub-assets.com/hackclub-half-life/sessions/6gi99sjgqS9PS6AP7HOtnbXmi9NgjIY3/4f4f061a44c2efcb1fd14aaf8ec614e3ade9b1835135bb8b9761813f937bf0bf.png)

## October 20, 2026

8 hours

Devlog 04: controls and first PCB placement

picked the switches, pots, jack and film capacitors and finished their footprints. checked the knob directions too. clockwise now means faster tempo, higher pitch, longer decay, brighter tone and more volume. the note switches select a note when pushed up

the octave selector has exactly three positions. it uses two poles to encode the range, with the other two left open. the tempo pot is 250k with a resistor across it to keep the nominal range around 38-240 BPM

started the PCB. it is 220 x 170 mm with two copper layers and four mounting holes. the controls are on the front in two piano-style rows, with most of the small circuit parts on the back. the supply parts are grouped at the rear, away from the controls

made a footprint for the mute switch using TI's recommended land pattern. the wider pads in the generic footprint were too close for the board's clearance setting. also checked the switch commons, jack contacts and the pot support tabs against their drawings

the schematic passes ERC and the sequencer checks still pass. the board is only a first placement, with no routed tracks yet. routing and the case are next, and the physical fits will still need checking when the parts arrive

![pcb-front](https://halflife.hackclub-assets.com/hackclub-half-life/sessions/6gi99sjgqS9PS6AP7HOtnbXmi9NgjIY3/d1430bd60abe9f16a4ff80788b6ddac7b1d13c56b76134d916b561e98d895fd1.png)

![pcb-back](https://halflife.hackclub-assets.com/hackclub-half-life/sessions/6gi99sjgqS9PS6AP7HOtnbXmi9NgjIY3/be67c89e98d06269851a886d34f120a06b1119de495c2ecc61106ef87632ab73.png)

![arpeggiator-01_controls_a](https://halflife.hackclub-assets.com/hackclub-half-life/sessions/6gi99sjgqS9PS6AP7HOtnbXmi9NgjIY3/d9acd6562ebefc1cd68ed6f564b808aafabb5981d954aeaf7366dd43a90a8edf.png)

![arpeggiator-03_clock_range](https://halflife.hackclub-assets.com/hackclub-half-life/sessions/6gi99sjgqS9PS6AP7HOtnbXmi9NgjIY3/3a093d27f9f737c21df968a8f4e31fabd56738ed4908a8fc8222f5a8b8fba5fb.png)

![arpeggiator-13_line_output](https://halflife.hackclub-assets.com/hackclub-half-life/sessions/6gi99sjgqS9PS6AP7HOtnbXmi9NgjIY3/2422564696796e6ec03cdd001a613b74614bd8a3df5ee146bc4b75705dc3d640.png)

![SW_Alpha_SR2612F_4P3T](https://halflife.hackclub-assets.com/hackclub-half-life/sessions/6gi99sjgqS9PS6AP7HOtnbXmi9NgjIY3/b41c6427348492d015bf67428a205c4193071bc58343033a9fbf72713d888c98.png)

![VSSOP-8_DGK0008A_TI](https://halflife.hackclub-assets.com/hackclub-half-life/sessions/6gi99sjgqS9PS6AP7HOtnbXmi9NgjIY3/10f372be477f54509234188033f5feb86e3a66e521318592169102adc819470b.png)

![Jack_PJ-3001F_Vertical](https://halflife.hackclub-assets.com/hackclub-half-life/sessions/6gi99sjgqS9PS6AP7HOtnbXmi9NgjIY3/15e063576e81efe703225acb3939c4bf910327c5263569e24ecb896f5e9fcda2.png)

## October 22, 2026

15 hours

Devlog 05: routing the board

finally got the PCB routed. the power section and analog circuit went in first, followed by all the connections between the logic chips. kept the note switches and the rest of the controls where they were

i started with two layers, but the ground connections were getting stuck between all the signal tracks. changed it to four layers, with both inner layers used for ground. that sorted out the remaining connections without having to move everything around again

the board passes DRC now. next is making a case for it, then getting the parts and board ordered

![routed PCB, front](images/pcb-front.png)

![routed PCB, back](images/pcb-back.png)

![5v supply](images/routing/5v-supply.png)

![clock and start](images/routing/clock-and-start.png)

![envelope and vca](images/routing/envelope-and-vca.png)

![input power](images/routing/input-power.png)

![input registers](images/routing/input-registers.png)

![line output](images/routing/line-output.png)

![negative supply](images/routing/negative-supply.png)

![note multiplexer](images/routing/note-multiplexer.png)

![oscillator](images/routing/oscillator.png)

![pitch reference](images/routing/pitch-reference.png)

![rail monitors](images/routing/rail-monitors.png)

![search counters](images/routing/search-counters.png)

![switch inputs](images/routing/switch-inputs.png)

