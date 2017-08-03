---
modal-id: shell_commands_assistant
date: 2017-08-02
img:
alt: image-alt
project-date: August 2017
category: Home Automation
title: Run shell commands and boot your computer using voice commands
excerpt: Combining Google Assistant, IFTTT and Home Assistant provides us access to a powerful tool&#58; Voice-activated shell commands. No more getting up from the couch and physically control devices. Calories have rights too and we should stop burning them. Let's go!
---

{% include toc title="Contents" icon="list" %}

Combining Google Assistant, IFTTT and Home Assistant provides us access to a powerful tool: Voice-activated shell commands. No more getting up from the couch and physically control devices. Calories have rights too and we should stop burning them. Let's go!  

IFTTT stands for "If This Then That" and is a web-based service which enables a large variety of applications to communicate with each other. Conveniently for us, it supports both Google Assistant and Home Assistant - an open-source platform which you can as a server on your computer (at the time of writing it supports Linux, Windows, OS X, FreeBSD) and is able to monitor and control your home automation devices. But the main feature of interest for us in this post is the ability to run [shell commands](https://home-assistant.io/components/shell_command/).  

The implementation of the Home Assistant wasn't quite intuitive, so I will provide a clear step-by-step guide to the best of my writing skills. If you are running a Debian-based OS like I do (Raspbian), this guide should be a perfect fit for you. I haven't tried this setup on other OSs but it should work on everything that can run Python 3. Alright, enough with the introduction, our homes are eagerly waiting to be made alive!

### Overview
Needed for this project:
- Computer which runs the Google Assistant and can run Home Assistant, e.g. Raspberry Pi 3 running Raspbian Jessie. Additionally, internet access and peripherals to record and play audio
- (Optional) A computer that supports [Wake-on-LAN](https://en.wikipedia.org/wiki/Wake-on-LAN) for booting from the network  

The second computer is for me to demonstrate the functionality of the shell command feature. But also since its base unit is cramped somewhere under my desk guarded by a cable clutter and a potential army of spiders, I might as well have a small upgrade in quality of living. Naturally you can use any other shell command such as `touch ~/test.txt` to test the functionality.

### Step 0: Prerequisites
You first need a device running Google Assistant. Google provides a great guide on how to install it. You can take a look at [this post]({{ site.baseurl }}/home%20automation/assistant-on-pi/) for more details - I guarantee it wont bite!

### Step 1: Install Home Assistant
Similar to the Google Assistant installation, I will install the Home Assistant in a Python virtual environment again so it wont mess with any existing Python installments. If you prefer a different installation method, check out [this page](https://home-assistant.io/docs/installation/).

[IMAGE: screenshot of Home Assistant installation in Terminal]

As usual, we start by getting all packages up-to-date from the command line:
```sh
sudo apt-get update && sudo apt-get upgrade
```  

Install & update **Python 3**, **pip** and the **virtualenv** tool afterwards:
```sh
sudo apt-get install python-pip python3-dev
sudo pip install --upgrade virtualenv
```  

The Home Assistant server will be constantly connected to the internet, so it is a good idea to create a separate user for it to limit its permissions. This part could introduce complications to the implementation, but security is a value worth fighting for!  
Add a system user and a group to your system:
```sh
sudo adduser --system homeassistant
sudo addgroup homeassistant
```  

[More coming soon: finish Home Assistant installation, link it with IFTTT and Google Assistant, trigger shell command service by Google Assistant. Bed time!]
