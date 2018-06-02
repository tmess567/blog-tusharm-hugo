---
title: Remote Access to RPi
author: tusharm
type: post
date: '2018-06-02'
image: /wp-content/uploads/imageedit_2_7104417219.png
categories:
  - Uncategorized
  - RaspberryPi
tags:
  - express
  - interface
  - js
  - node
  - nodejs
  - npm
  - server
  - remote
  - access
  - ngrok
---
## Context

Recently, I started working on some Raspberry Pi projects, but the most frustrating part of that experience was to access the raspberry pi during development.

I had the following options:

* Use the Television at my place as a monitor over HDMI (not great pixel quality) and use wired keyboard and mouse to control. This was troublesome since I could only develop when I'm at my place and the Television is free.
* Be on the same network and ssh into the PI. This worked for a while since I could also access the ports of RPi, so I could host my applications on a certain port and access them over the RPi's IP address. 

## Problem Statement

The second option is obviously the way to go, but this needs some refining. 

1. Be on the same network to access ssh and other ports. \
   This can be solved using Ngrok. For more info: \
   https://ngrok.com/\
   https://www.npmjs.com/package/ngrok
2. Access persistent shell sessions (in case of power or network drop) \
   This is why I needed to write a script
3. Access the internet as if being browsed from the RPi (this is a use case for some future projects).
   Simplest solution: ssh -L 80:remotehost:80 user@myserver

## Limitations of Ngrok

A free account on NGrok has the following limitations:

1. HTTP/TCP tunnels on random URLs/ports
2. 1 online ngrok process
3. 4 tunnels/ngrok process
4. 40 connections / minute

## Solution

The most troublesome of the above limitations is the random port. Every time I reconnect to ngrok, I receive a different port to which I need to connect. I could buy a premium account but there's a simple solution for this.

* Create a server
  * Accept beacons from devices
  * Show currently available devices
  * Timeout devices when no beacon received
* Create a client
  * Easy and scriptable installation
  * Auto-start on boot
  * Bundle Ngrok binary
  * Upon ngrok start, access the available tunnels
  * Send beacon to server with tunnel details

This way, any time I want to access a device, I just need to pull down a repository and set it to run on boot. This in turn will keep updating my server on the availability of my device and the port I can access it on.

If I want to access a different port, maybe over http protocol instead of tcp (ssh is supported over tcp), I can just edit a global variable in the pulled down code and restart the device. The new tunnel should show up on the server once the device is up and running.

## Why not use a VPN?

In cases like my office network, I might need to be already connected to a VPN or some other network proxy. Configuring my development client device to connect to my home VPN might not always be an option.

## Security

Working on it...
