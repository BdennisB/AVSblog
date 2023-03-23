---
layout: post
title: HCX Troubleshooting
share-title: Connector issues
subtitle: HCX connector troubleshooting
tags: [AVS, HCX, Troubleshooting]
---
The connector, each time it needs to reboot completely needs a LONG time for it to come up and be fully ready. Don't think this is going to be ready in a couple of minutes after you boot it.  Think more like 10 - 15m of patience before you can be sure to try again whatever it is you were busy doing or were thing of doing.

In case however, and mind you this is certainly not something you should be prepared for at all times but still if you are a geek like me and want to explore what's really going on then the following section you are really going to like.

Say after a while, you have been waiting long enough and you want to check a few basic things.

Lets logon to the connector using SSH
> ssh admin@<connector ip>

Once you are there check first of all of 9443 port is listening correctly

> netstat -a | grep 9443

If you see a prompt without anything coming back to you then there's two things happening, either you are too quick or the web-engine hasnt fired up yet.  Most likely its the last one however issue the following commands to make sure

> sysctl status web-engine
> sysctl status application-management

You want to look for active statements in the bunch of text being thrown at you.  To get more info consider putting sudo in front of the above commands.

Nothing will ever happen until those two show an active stat