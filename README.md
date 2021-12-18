# ti-calc-20yr
Nostalgicly playing with a TI-83+ calculator 20yrs later

Twenty years or so ago when I was in high school we had to buy a TI-83+ calculator for use in course work. This year I got the itch to buy a new one(my old one had broken eventually) and play around with it, apply my software engineering skills to it a bit. This repo is an attempt to document the process and collect information. Note that beause this is such an old subject I doubt much of what I write will be truly new. Much of it is collecting resources, avoiding broken links, and working out how to run the old tools on a modern system.

I'm running all of these steps on my ubuntu 20.04 laptop in 2021. I'm sure things will continue to change, and your mileage may vary greatly from mine if you're reading this a few years later.

## Getting started

### Purchase

To start with I went on Amazon and ordered a TI-83+ Silver edition(for the extra storage) and a TI Graphlink USB cable so I could connect it to my PC. Easy enough. They still sell this model of calculator for schools, so there were some in stock that I could get pretty quickly.

### Communication

To get the calculator to communicate with my laptop I installed TiLP2(`sudo apt install tilp2`), plugged in the cable, and launched it. I then went to File->Change Device and selected the following options:
* Cable: DirectLink
* Port: #1
* Calc: TI-83+

Works beautifully. Yay

### Update OS

To update the OS I went to [TI's website](https://education.ti.com/en/software/search/ti-83-plus-family#!view=handheld-operating-system), downloaded firmware 1.19. It took a request to TI, which was weird to fill out. Many of the options didn't make sense for someone doing this nostalgically years later. Ah well, I did my best to be honest with my answers and a few minutes later got an email with a link to the OS update image. I can't share the OS update for licensing reasons, so hopefully TI continues to host the images on their servers.

Once I had the image it was as easy as opening TiLP2 and selecting File->Send Files and selecting the `TI83Plus_OS119.8Xu` file that I had just downloaded. A few minutes later it was updated. Note that updating does clear all RAM, so back up anything you want to keep before doing this, or do it early enough that nothing is on the calculator yet.

## Emulation

Of course I'd love to be able to emulate my calculator on my laptop both for convenience and so I can test programs without risk of bricking the real calculator.

### Install emulator

For emulation I decided to go with tilem, which is easily installed on ubuntu(`sudo apt install tilem`) and seems to work well.

### Get ROM image

TI's ROM images are licensed tightly, so you won't find any legally posted online(and don't ask me for them). Instead you'll need to either feed tilem an OS update package or dump the ROM from your own calculator. I chose the latter, although in hindsight I think it would have been easier to do the OS update package method. I wanted to get the ROM for _my_ calculator though, and it was fun.

TiLP2 has support for ROM dumping under Tools->Dump ROM and it almost works out of the box. Except, due to debian package rules they patch TiLP2 to not contain the ROM dump program that gets loaded on the calculator to read out the ROM. So I had to build a version of TiLP2 with the ROM dumping support reenabled. To do this, I found a clue [here](https://sourceforge.net/p/tilp/bugs/217/) and rebuilt the tilp package without the patch to get it working.

Roughly the steps were:
```
apt-get source libticalcs
cd libticalcs-1.1.9+dfsg/
vi debian/patches/series   # Delete the one line describing the patch
patch --reverse -i debian/patches/ticalcs2-external-rom-dumpers.patch -p1
dch --local qypea
debuild -us -uc
cd ..
sudo apt install ./libticalcs2-12_1.1.9+dfsg-2qypea2_amd64.deb
```

After this I closed and opened TiLP2, ran Tools->Dump ROM, and sat back until the file was downloaded. At that point I opened `tilem`, opened the ROM image I had dumped, right-clicked and selected Preferences.
* Emulation Speed: Limit to actual...
* Display: Emulate grayscale, Use smooth scaling, Use skin: `/usr/share/tilem2/skins/ti83p.skn`

### Skinning

Hey, that's a calculator. Not quite _my_ calculator though. Lets make a skin for it so it looks like _my_ calculator.

To create a skin for my calculator I started by taking a picture of my calculator from straight down, copying it over to my computer. I then cropped the image down, resized it to the same size as the basic TI-83+ skin(320px wide as I recall). I then ran `skinedit`, created a new skin for my calculator based on that image.

In SkinEdit I needed to define where the screen and all the buttons are. To do this select Edit->LCD Position, draw a box, then right-click. Then select Edit->Key Positions, select a key, draw a box, then right-click. Note that you have to right-click each time to save the box. I went through this all twice; not right clicking the first time and wondering where they went. Once I had that done I saved the skin, selected it in tilem. It worked, Yay

![Screenshot_2021-12-18_09-36-54](https://user-images.githubusercontent.com/1694406/146650555-e97848d6-eab1-4ea7-b08a-438b95969f56.png)

I've included my skin file in this repo as [ti83psilver.skn](ti83psilver.skn).

## Writing and compiling assembly

Being a software engineer by day, I want to program this thing. It'll be fun(I know, I'm sick that way). I downloaded the [Learn TI-83 Plus Assembly In 28 Days v2.0](https://www.ticalc.org/pub/text/z80/83pa28d.zip) tutorial and am trying to follow it along.

### Assembler

Day 01 lesson and I've already hit a snag. TASM is in theory available for linux, but the shareware binaries posted on ticalc and similar sites are all for windows/dos. I've sent some emails to Tom Anderson to see if I can still purchase the full version by mailing him a check, but will have to see how that works out. Its almost 20 years since the release of version 3.2, so who knows if he's still at that address or even has the sources any more. I'll update this doc as I learn more.

### Assembler in wine

I'm currently trying to run the TASM assembler in wine, see if I can get that working. Will update as it goes.
