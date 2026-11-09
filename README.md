# MegaGB

A cycle accurate emulator for the Gameboy and Gameboy Color consoles in C, with pixel FIFO emulation for high accuracy and emulation precision. This was done as a hobby project from scratch, using only hardware documentation. This was integrated with ImGUI in C++ to show internal information, disassembly support and allow configurations.

The process involved implementing every CPU, Memory and Graphics related component of the console in software, keeping in mind intricate functioning and interplay of the components. This had to be done to a level of precision where the games/software dedicated to the Gameboy ran identically on the emulator, as on the real hardware. 

## Key Design Highlights and Features

• The core emulator (without GUI), i.e CPU, Memory, PPU, Timers, Hardware Registers are a challenge to emulate as they run in parallel on the real hardware. All these components in the emulator run on a single thread. Syncing, scheduling and context switching is done, often times several times per CPU instruction, such that these parallel components running together are emulated at a very high accuracy.<br>

• Every CPU instruction was implemented manually in code, keeping in mind read/write timings and syncing with other hardware components like the Hardware Timers, Registers and Pixel Processing Unit, at CPU cycle granularity. <br>

• Additionally, for emulating the graphics, the entire Pixel First-In-First-Out (FIFO) hardware mechanism was emulated, to get maximum accuracy. This replicated changes to display accurately at dot and instructional level granularity (for example: Mid-scanline writes to video memory are replicated correctly at the CPU cycle level), matching very closely to how the actual hardware does it. Every pixel is processed and pushed individually as part of this FIFO and this is intertwined with the CPU Instructions running on the same thread. <br>

## Benchmarks of accuracy and completion

• Passes all of [Blargg's](https://github.com/retrio/gb-test-roms) CPU Instruction, Instruction timing, Interrupt and Memory timing test ROMs.<br>
• Passes [dmg_acid2](https://github.com/mattcurrie/dmg-acid2) and [cgb_acid2](https://github.com/mattcurrie/cgb-acid2) PPU tests.<br>
• Passes halt, call, ret, ei, div, timer and many more quirk tests in the [Mooneye test suite](https://github.com/Gekkio/mooneye-test-suite).<br>

## Development Timeline
• <i>September 2021 - December 2021</i> : CPU instruction set implementation, cycle accuracy and timing, interrupt handling, hardware registers and timer.<br>
• <i>May 2022 - August 2022</i> : PPU Pixel FIFO design and implementation, completion of essential components, memory bank controllers.<br>
• <i>December 2024</i> : Debug menu addition using ImGUI.<br>

## ROM Showcase
### Gameboy

| | | |
:---:|:---:|:---:
<img src="images/tetris.png" width="90%"> <br><b>Tetris</b> | <img src="images/alien3.png" width="90%"/> <br><b>Alien 3</b> | <img src="images/legendofzelda.png" width="90%"/> <br><b>Legend of Zelda - Link's Awakening</b>
<img src="images/pokemonblue.png" width="90%"/> <br><b>Pokemon Blue</b> | <img src="images/bioniccommando.png" width="90%"/> <br><b>Bionic Commando</b> | <img src="images/kirby.png" width="90%"/> <br><b>Kirby's Dream Land</b>
<img src="images/pinballdeluxe.png" width="90%"/> <br><b>Pinball Deluxe</b> | <img src="images/drmario.png" width="90%"/> <br><b>Dr. Mario</b> | <img src="images/donkeykong.png" width="90%"/> <br><b>Donkey Kong</b>

### Gameboy Color (Most features have been implemented)

| | | |
:---:|:---:|:---:
<img src="images/tetrisdx.png" width="90%"> <br><b>Tetris DX</b> | <img src="images/pokemoncrystal.png" width="90%"/> <br><b>Pokemon Crystal</b> | <img src="images/mariogolf.png" width="90%"/> <br><b>Mario Golf</b>
<img src="images/supermariobros.png" width="90%"/> <br><b>Super Mario Bros</b> | <img src="images/pokemongold.png" width="90%"/> <br><b>Pokemon Gold</b> | <img src="images/tetrisdxplay.png" width="90%"/> <br><b>Tetris DX Playthrough</b>

### Real time execution state viewer and color palette selector
<img src="images/palettedisplay.png" width="80%">
<p>ROM: <i>Is that a demo in your pocket?</i></p>

## Current State
Currently the project is out of active development as it has reached a stable stage of functionality. However there are pending improvements that could be made
over the years as and when I feel like working on them:

• Adding more memory bank controller support to expand to more runnable games<br>
• Complete Gameboy color residual support<br>
• Add audio emulation<br>
• Better debugging UI and infrastructure<br>

## AI Usage Disclosure
The core emulator was developed before the public availability of modern generative AI tools and LLM-based coding assistants.<br>
No generative AI was used in the design, implementation, debugging, testing, or documentation of this project.

## References
• [Gameboy Pandocs](https://gbdev.io/pandocs/) - For hardware documentation and quirks <br>
• [izik1's Gameboy CPU opcode table](https://izik1.github.io/gbops/) - CPU Instruction encoding

