---
layout: default
date: 2017-07-24
img:
project-date: July 2017
category: Home Automation
title: Home Automation with Voice Commands
---

With the Google Assistant SDK being released, speech-based home projects received a powerful new component in its arsenal and with this I thought it's about time for me to jump on the home assistant hype train!
The Google Assistant will be implemented on a Raspberry Pi, which makes it a potentially more powerful and much cheaper system than the Google Home device and along with fun and joy we will hopefully learn a thing or two.

This project contains a wide variety of features among which are:
- Google Assistant running on a Raspberry Pi
- use a bluetooth remote to initiate request to Google Assistant
- execute shell commands with Google Assistant, IFTTT and Home Assistant
- switch on/off devices connect directly to wall plug and ceiling lights using relay modules

If you want to use this post as a guide or inspiration for your own projects, I am going to assume that you are already somewhat familiar with Linux systems and the Raspberry Pi, although I will try to mention all important details on what I did. Alright, let's get right to it!

[IMAGE: google assistant + raspberry pi]

A quick overview on what components I used for this setup:
- Raspberry Pi 3 Model B running Raspbian Jessie
- Speakers with 3.5mm jack
- Microphone with 3.5mm jack
- 3.5mm to USB audio adapter to plug the mic into the Raspberry Pi
- Notebook running OSX 10.11
- at least one finger

### Step 1: Preparation & SSH connection
To start off, we first need to install the Google Assistant on a Raspberry Pi which will be the main focus of this post. Google provides a great guide for the installation, I started off [here](https://developers.google.com/assistant/sdk/develop/python/hardware/setup).
Conveniently, I already have a Raspberry Pi 3 Model B with Raspbian Jessie installed which I use for my home surveillance system. I will access my headless Raspberry Pi via [SSH](https://www.raspberrypi.org/documentation/remote-access/ssh/), so except for the power supply no additional wiring will be necessary for now, when using the WiFi connection - gotta save the cable clutter for later!
With the option to comfortably controll the Raspberry Pi from my notebook, I connect to it via SSH in Terminal.

### Step 2: 







Feel free to post questions/comments/suggestions, I'm excited to hear from you!
