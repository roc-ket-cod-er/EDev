---
title: "EDev"
author: "Madhav"
description: "An ESP32 devboard, with built-in battery holders."
created_at: "2025-07-24"
---

Hours: 4.5

## Day 1: Core Board (7/24)

First things first, time to do some planning.

I am thinking of using the ESP32, because it is a simple enough board to use, and I might as well go a bit simple as time to finish projects under Hackclub's Highway is running out. I also want to have just a simple board, however it must be protected, in case someone doesn't know how to use it. It must be that you can have both the USB and the Battery in at the same time, even if they are different voltages.

<img width="450" height="284" alt="image" src="https://github.com/user-attachments/assets/b441830d-382f-4416-ba6b-215f0c49a5b8" />

So I got to designing. I chose to power it off of 2x CR2032s, as they are quite commonly availible, and still hold quite a bit of power, nice for a devboard that spends most of its time asleep, occasionally wakes up, and then goes back to sleep. As each battery holds arond 120mah, x2, that means that they will be fully drained in an hour of maximum power draw, however if we use the above mentioned use case, it should be just fine.

So then to the designing!

---

First thing is first, which ESP32 module should I use? I have many different options, however I am limited by what JLCPCB can assemble without using standard assembly. As this thing must be a cheap board, preferably under $50 for the 2 set, it must not use advanced assembly. So, here I go!

A bit later

After some research, I have come up with 2 different modules. I can either go with the ESP32-WROOM-32D-N16, $4.xx

![download](https://github.com/user-attachments/assets/380a7459-d953-4ffc-ae5e-68bd129a7a55)

or the ESP32-S3-MINI-1-N4R2 for $3.xx

![download](https://github.com/user-attachments/assets/5068a02b-26c1-4ebb-aa12-8de110121119)

Time to go Datasheet-Diving!

---

A bit of Datasheet-Diving later, I have found some key differences. Let me explane them to you.

In the code, there are a few important numbers.

The number after the N signifies how much storage the module has. If the it says N4, it means 4 megabyetes, and if it says 16, it means 16MB.

Off the bat, the ESP32-WROOM looks like the better choice. But that is about its only benifit.

Not only is the S3 smaller and cheaper, but it has much more ram. The number after the H signifies the amount of PSRAM, if any. The S3 has a *2MB* of PSRAM, compared to the WROOM's 0.

As I mentioned, it is quite smaller, and it is also having significantly more GPIO. As far as I can tell, it is the optimal choice for sure.

---

### A bit of designing later

Well that was quick. Thanks to my experience with the S3, I managed to do the entire routing,

<img width="1172" height="733" alt="image" src="https://github.com/user-attachments/assets/67499a98-2585-472b-a8d8-82692910f534" />

in just over 2.5 Hrs.

Some key notes in case you are also trying to replicate the set up, the board only really needs a bit 10uf and 0.1uf

<img width="737" height="542" alt="image" src="https://github.com/user-attachments/assets/3883dadd-607e-4756-a125-b44424e353b0" />

However, I chose to use an extra 1uf capacitor, as I had heard that sometimes it can benefit some stability.

In terms of power, often an LDO is the simplest option, and thus that is what I ended up using.

<img width="906" height="582" alt="image" src="https://github.com/user-attachments/assets/86f968c6-3d3c-43de-bed7-90438c6f7b96" />

It might not have enought power to get everything to start up itself, however, and thus when the board is first powered up, its is ideal for it to be connected to USB.

The LDO's datasheet said 10uf on input and output, thus that is what I used.

<img width="957" height="790" alt="image" src="https://github.com/user-attachments/assets/4fb3cc8a-654a-4c3e-b941-e8bb70d74c57" />

I also chose to use a usb-c connector, as I felt that most devices these days use it, so why not mine?

It is a bit more complicated than other forms of USB, however I think that it should be ok.



In terms of GPIO, I chose to use a female header setup:

<img width="651" height="466" alt="image" src="https://github.com/user-attachments/assets/bdb7449a-9250-45e9-9c68-f9328fbf2342" />

There are a total of 52 pins, out of which 26 are ground pins. It makes running a small sensor, push button, or LED just so much easier with a ground pin next to every GPIO.

There are also 18 accessible GPIO, 3x 3.3V lines and one battery input line. As long as the CR2032s are not in, you can connect upto 20V of power to the esp32f from, for example, a lipo (for high-power applications).

---

Well, yeah! That's how you speedrun and ESP32 based board. I am just going to add 2 LEDs --> one on the USB line, and one on the 3.3V line.

---

There we go!

LEDs added!

<img width="1288" height="742" alt="image" src="https://github.com/user-attachments/assets/2b8ef703-b831-4f65-a135-c6e17cc2dafa" />

I think it might just be me, but this board is looking *sick*!

### HOURS: 4.5

Day 2: Copper Keep Out (7.28)

Today, I just spent like 2 minutes adding a copper keepout zone underneath the antenna.

### HOURS: 0 / 4.5
