---
title: "Responsive bias lighting (Ambilight) with WLED"
date: 2020-01-21T16:27:29+05:30
draft: false
tags: 
  - WLED
  - HomeAutomation
  - ESP8266
  - WS2812B
  - Ambilight
---
Building a what now? 

{{< youtube N5P_1TaypYo >}}

Convinced? Great.

*Note - This is not for complete beginners, I do not explain basic concepts here. However, there is nothing here that you can't learn with google-fu and reading*

## Overview
This setup is slightly different than the usual tutorials you might find out there. I wanted to achieve two things from my setup. A bias lighting setup, obviously, but also an integration with [Home Assistant](https://www.home-assistant.io/), so I can control it just like another "light". It's quite cheap to set this up, it's cost me ~₹2000 or $28 for the whole setup.

## Limitations
This particular tutorial is not for television sets, it will only work with a computer. I'm using Windows, but this should technically work on MacOS / Linux.

## What you need
*These aren't affiliate links nor am I in cahoots with the manufacturers, you can find alternatives to the parts mentioned below.*
- **A ESP8266 Board** ([What I got](https://www.amazon.in/gp/product/B07262H53W))
- **A WS2812B RGB LED strip** ([What I got](https://www.amazon.in/gp/product/B07V9RN95V))
  - *I got a 1m / 60 LED strip for my 24-inch monitor. You can get a longer one / with more LEDs, however, your power usage will increase accordingly*
- **Jumper Wires** ([What I got](https://www.amazon.in/Electrobot-Jumper-Wires-120-Pieces/dp/B071VQLQQQ))
  - *You probably don't need so many, just grab a set of assorted jumper wires from Amazon [like these](https://www.amazon.in/ApTechDeals-Jumper-Female-breadboard-jumper/dp/B074J9CPV3/).*
- **USB Power Supply + Micro USB Cable**
  - *I use my monitor's integrated USB port to power the LED Strip. While this works in my case, it might not work for you. You might want to buy a dedicated power source [like this](https://www.amazon.in/gp/product/B07RW8RQC5).*

## Okay, I have no idea what I just bought
Fret not. Things will come to light. Here's a quick overview -
- **Your PC** will gather screen edge data and send it to the Controller
- **Controller (ESP8266)** will receive this data and send it to the LED Strip
- **Your LED Strip (WS2812B)** will receive this data and do the actual... lighting.
- **Jumper Wires** will be used to connect the controller to the LED Strip

## Setting up your LED Strip

I'm outsourcing this to a [really well-written blog post](https://tynick.com/blog/11-03-2019/getting-started-with-wled-on-esp8266/) that will also explain a lot of the jargon.

Some notes - 
- The cable colours for LED Strip may not be the same as the ones mentioned in the post. Your LED Strip will have come with a manual, refer to that to figure out which colour is what cable.
- Once you have the LED Strip lighting up, you might not have all the LEDs lighting up. It's okay, you can fix this by logging into WLED's web UI by accessing it's IP Address (find this in your router admin), go to Settings > LED Settings and change "LED Count" to the number of LEDs your strip has.
- I'd recommend reserving an IP Address for your LED Strip on your router. 

If you follow through the entire tutorial, you should end up with a functioning LED Strip! You can use WLED's Web UI / App to control your strip manually. You can also connect it to Home Assistant. 

*Don't stick the strip to the back of your monitor yet, it will get more difficult to troubleshoot.*
## Setting up the PC side of things 

We need *two* things here. 
### Prismatik - [Download from here](https://github.com/psieg/Lightpack/releases)
  - This is what does the screen capturing, but this can't directly communicate with our WLED Strip
  - Download, install and run the latest release. You'll be asked to go through the configuration wizard. 
  - Select "Setup another device" and then pick "Virtual LED Device)
  - You'll get to the "Zone placement section" make sure to set 60 LEDs and then select one of Andromedia, Cassiopeia, Pegasus
  - Rest of the wizard steps are self-explanatory, so I won't go through them
  - You can re-run the configuration wizard from the "Devices" section


### Prismaik-WLED-WiFi - [Download from here](https://github.com/Lord-FEAR/Prismatik-WLED-WiFi)
  - This is a script someone wrote to be able to communicate between WLED and the Prismatik software
  - Follow the instructions in the README to set it up.
  - In the ini file, set 

This is how data moves in this setup - 

> Prismatik > Prismatik-WLED Script > Controller > LED Strip

The Prismatik-WLED readme mentions that it should be dropped into the "Plugins" folder of Prismatik. I had some trouble with that, so I just ran the script manually from a different folder (just make sure the .ini file is in the same directory), it worked just fine. You need this script running if you want Prismatik to be able to communicate with your LED Strip. Just get it to automatically run at startup and you're gold. 

If you've set up everything correctly, your LED Strips should now change colours according to your monitor! Hard to tell if you haven't taped it on the back of your monitor, so I'd recommend testing it by playing a video [like this](https://www.youtube.com/watch?v=8u4UzzJZAUg)

## Configuration Tips & Tricks 
- Set the "Grab Frequency" in Prismatik to the FPS that matches your screen's refresh rate
  - *This might be a bit much, but I'm not seeing a significant performance hit even when playing video games*
- Update the FPS in the Prismatik-WLED configuration accordingly
- Try out the Mood Lamp and Sound Visualization mode in Prismatik, they're pretty cool
- For the Sound Viz mode to work properly, make sure to select the correct sound device's "loopback" option
  - Also, I prefer the "Twin Peaks" preset for Sound Viz as compared to the default one
- Prismatik will override whatever WLED configuration you may have set, so make sure to kill the Prismatik-WLED script when you only want the WLED effects / colours.

## Wrapping Up
Because I wanted both WLED and Prismatik, I had to go with a more roundabout approach, but I'm quite happy with it as I get the best of both worlds.

It works with games too! 
{{< youtube Eglks2tT_64 >}}
