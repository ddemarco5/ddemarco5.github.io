<img src="images/me.png" width="300">

## Hi There!

Welcome! One way or another, you've stumbled upon my projects github.io page! 
My name is Dominic DeMarco, my education background is a BS in Computer Science, and I currently work in the industry as a software engineer.

In my free time I enjoy exploring anything technical, and I often find myself reading up on the odd technological tidbit.

But reading will only get you so far! I try to commit a healthy portion of my spare time into practicing my interests.
On this page you'll see the results of that practice.

I've organized my projects in reverse chronological order. I'll add and related links and provide a short description for your perusing pleasure.

These links will bring you to the associated headings to save your scroll wheel the trouble  
[Radio Board](#radio-board)  
[Serial over LoRA](#serial-over-lora)  
[Python Racing Game Bot](#python-racing-game-bot)  
[Pascal-like Compiler](#pascal-like-compiler)  
[Sensor Movement Classification](#sensor-movement-classification)  

---
  
### Radio Board
<img src="images/pcb_image.png" width="200">


**Circuit Design and PCB:** [https://github.com/ddemarco5/design-pcb](https://github.com/ddemarco5/design-pcb)  
**Code:** [https://github.com/ddemarco5/RadioCode](https://github.com/ddemarco5/RadioCode)  
  
My first foray into circuit design and construction, and my current work in progress. The design was largely based around what parts I had gathered in my dragon's nest of electronics. Before this, the most advanced I had gotten was a little breadboard tinkering and Arduino work.
The general idea is to have a single board with 3 chips. A MAX7221 to drive the display, a SI4734-D60 to act as the radio, and an ATTINY861 to control the other 2. There's a rotary encoder to enable control, and a 3.5mm jack to allow for audio output.

A couple goals motivated this project. I wanted to:
1. Experiment with circuit design software and processes.
2. Practice soldering SMD (There's a .6mm pitch on one of those chips)
3. Try AVR programming from scratch. No arduino libs.
4. Get more experience with on-chip communication protocols. SPI, I2C, etc.
5. Practice hardware debugging. I got more practice than I would've liked...
6. Polish up my C++ by writing necessary code from scratch 
7. Program in a memory constrained environment (8k program storage, 512 bytes SRAM)
8. Watch a cool old red bubble LED display live again

I'm still actively working on this one and it's taught me a truly incredible amount about hardware and circuit design.

If I were to do it again I would've spend more time in the prototyping stage (but I'm limited by tools and space), as the first revision had some design errors in some of the more complex things I attempted (hardware debouncing with RC filter circuits, etc). I ended up having to frankenstein a portion of the traces and rework the design into something functional without having to rebuild the entire board.

As far as programming goes, at the time of writing, I am properly driving the MAX7221 via a software SPI implementation. I'm currently trying to get the (much more complicated) radio chip to respond.  

---
  
### Serial over LoRA

<img src="https://cdn.hackaday.io/images/6317041498596792862.jpg" width="200"> <img src="https://cdn.hackaday.io/images/9159631498596820878.jpg" width="200">  

**Hackaday link:** [https://hackaday.io/project/25677-chirppp-serial-over-lora](https://hackaday.io/project/25677-chirppp-serial-over-lora)  
**Radio Driver:** [https://github.com/ddemarco5/lora_driver](https://github.com/ddemarco5/lora_driver)  
**Serial Emulator:** [https://github.com/ddemarco5/chirppp](https://github.com/ddemarco5/chirppp)  
  
To date this is one of my favorite projects. The idea was to leverage posix standards to communicate and drive a pair of LoRA radio modules and expose a functional serial device to an end user of the system.

The things I wanted to accomplish in this project were:
1. Learn and practice the Rust programming language
2. Use a hobbyist site (hackaday) to log and reflect on progress made
3. Practice UNIX environment programming by using sysfs and pty (pseudoterminal) syscalls
4. Get more practice with cross compilation (ARMv6, ARMv7, MIPSEL)
5. Develop an executable for OpenWRT

This was a really fun project to work on, it touched on a lot of diverse areas so it hardly ever got stale.\

I got to learn the modern systems programming language [Rust](https://www.rust-lang.org/en-US/)! I highly recommend trying it out if you ever get the chance. 

I learned about the entire (and surprisingly outdated) tty system in the typical unix stack, and about how sysfs works.

In the end, I was able to reliably use sysfs to communicate with and drive the LoRA modules on each of the platforms I compiled the program for. After I was sending packets back and forth, I was able to create a psuedoterminal pair that piped its input into the portion of the program that emulated a full duplex serial connection (the radios are packet based and there is no receving while transmitting!). In the end what this accomplished was a software device, typically /dev/pty0 or something of the sort, that a user could write to or read from. All traffic would appear on the pseudoterminal of the other computer, acting as if the two were connected via a wire.

Once I had serial communication between the two devices, I was able to use the old point to point protocol to send TCP/IP traffic between the two devices. 

I had achieved a rudimentary wifi that at best could achieve a several kilometer range! Woohoo!  ... at least in theory. 

In practice though, the radio devices at max speed had barely enough bandwidth to maintain a tcp/ip connection, let alone a usable one. It was also hampered by the fact the the (admittedly cheap) radio modules I bought suffer from frequent false positives when receiving packets. I might revisit this project to try and further debug the problem, or at the very least work around it.  

---
  
### Python Racing Game Bot

**Code:** [https://github.com/ddemarco5/Redline](https://github.com/ddemarco5/Redline])  

A simple project I decided to write when a drag racing game I was playing at the time got a little too repetitive.

This is a much smaller project than some of the others. The idea behind this one was to use python to try and interface with WinAPI to find the game's window and its dimensions, emulate keypresses, and capture image data from the screen.

The actual logic behind the bot's decisions were simple pixel triggers, the focus was more on getting some experience with the WinAPI.  

---
  
### Pascal-like Compiler

**Code:** [https://github.com/ddemarco5/pascal_compiler](https://github.com/ddemarco5/pascal_compiler)  

One of the last projects done in my college career.

Written in C, we had to create a compiler for a Pascal-like language that was defined in class.
We used lex and yacc to generate the lexiacal analyzer and parser, but codegen was up to us.
I unfortunately had to stop working on the project before codegen was 100% completed. It didn't construct proper loops, but it worked for simple calculator-esque evaluation and assignment statements.  

---
  
### Sensor Movement Classification
**Code:** [https://github.com/ddemarco5/SensorMovementClassification](https://github.com/ddemarco5/SensorMovementClassification)  

An android application written for an independent study done in college.
The app allowed a user to train on movement and later recognize those movements. The intention was to use it in a larger project where software would be able to recognize what its user was doing. Standing, sitting, running, etc.
