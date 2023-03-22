---
layout: post
title: HCX connector
share-title: HCX connector
subtitle: Setting it up, tips and tricks
tags: [AVS, HCX, service mesh]
---

Lets dig a little bit deeper and beyond of whats in our public docs.  Again just sharing from personal experience.

<img title="HCX extract" alt="Port/protocol info" src="/AVSblog/assets/img/screen3.jpg" width=850 height="500">
Usually when preparing for HCX the L4 green line info as stipulated above (as part of the larger HCX diagram as published by VMWare and also inside of our checklist) usually is ignored.  Instead deployment usually focus on everything red, as it crossing the DC perimeter into Azure.


{: .box-note}
**Note:** Purpose of this article is to share special setups beyond classic deployments
