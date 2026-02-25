# MegaGB

A fully functional cycle accurate emulator for the Gameboy and Gameboy Color consoles in C, with pixel FIFO emulation for high accuracy and precision. This was done as a hobby project from scratch, using only hardware documentation. This was integrated with a Graphical-User-Interface (IMGUI) in C++ to show internal information, disassembly support and allow configurations.

The process involved implementing every CPU, Memory and Graphics related component of the console in software, keeping in mind intricate functioning and interplay of the components. This had to be done to a level of precision where the games/software dedicated to the Gameboy ran identically on the emulator, as on the real hardware. 

### Key Design Highlights and Features:

• The core emulator (without GUI), i.e CPU, Memory, PPU, Timers, Hardware Registers are a challenge to emulate as they run in parallel on the real hardware. All these components in the emulator run on a single thread. Syncing, scheduling and context switching is done intelligently and at high frequency such that its seamless for software running and the end-user.<br>

• Every CPU instruction was implemented manually in code, keeping in mind read/write timings and syncing with other hardware components like the Hardware Timers, Registers and Pixel Processing Unit, at a sub-instructional level. <br>

• Additionally, for emulating the graphics, the entire Pixel First-In-First-Out (FIFO) hardware mechanism was emulated, to get maximum accuracy. This replicated changes to display at a sub-scanline level, matching very closely to how the actual hardware does it. Every pixel is processed and pushed individually as part of this FIFO and this is intertwined with the CPU Instructions running on the same thread. <br>

### ROM Showcase and GUI

![alt text](https://github.com/astrobits1/MegaGB/raw/master/img1.jpg
![alt text](https://github.com/astrobits1/MegaGB/raw/master/img2.jpg
![alt text](https://github.com/astrobits1/MegaGB/raw/master/img3.jpg

