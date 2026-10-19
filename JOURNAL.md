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
