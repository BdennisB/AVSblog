---
layout: post
title: HCX connector
share-title: HCX connector
subtitle: Setting it up, tips and tricks
tags: [AVS, HCX, vmotion]
---

## firewall

Lets dig a little bit deeper and beyond of whats in our public docs.  Again just sharing from personal experience.

<img title="HCX extract" alt="Port/protocol info" src="https://bdennisb.github.io/AVSblog/assets/img/screen3.jpg" width=850 height="350">
Usually when preparing for HCX the L4 green line info as stipulated above (as part of the larger HCX diagram as published by VMWare and also inside of our checklist) is ignored.  Instead deployment usually focuses on everything red, as it crossing the DC perimeter into Azure or public internet (the vmware.com urls)

Please make sure to check the ones IX-vCenter and last but not least the 8000 port.  Port 8000 is needed for vMotion.
This is where the network profile comes in.  If you overlook creating a compute profile specifically for vMotion and/or block it from being exposed on the VDS (or VSS) you will not be able to vMotion your workload.  
Do not forget this therefore if you want to avoid running into issues building your service mesh. 

Please see also another post on this blog covering the install process specifically.



