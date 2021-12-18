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

