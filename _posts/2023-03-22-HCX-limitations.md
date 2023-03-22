---
layout: post
title: HCX limitations
share-title: HCX and its limitations
subtitle: Limitations and thoughts arounds that
tags: [AVS, HCX, limitations]
---
First off lets make sure you know where to check the limitations are published aligned to your specific version:<br>

<https://configmax.esp.vmware.com/guest?vmwareproduct=VMware%20HCX&release=VMware%20HCX%204.6&categories=41-0,42-0,43-0,44-0,45-0>

Not all of these numbers match up to AVS. For example the number of service meshes for an AVS SDDC is set to **10**! keep that in mind when you are doing that design.

Replication Assisted VMotion allows for a maximum of 200 VMs to be moved.  Offset that number to the amount of VMs per manager, which is 300 and you know that in order to achieve at least some level of parallelism, in the event of multiple clusters the number of migratable VMs so to speak that are moveable at the same time using RAV is **300**

Obviously this means that with 200 max VMs per mesh and a 300 max VMs per Manager you can either setup a 200 and 100 VMs capability in parallel or you will have to cut down on the number of VMs you can migrate at the same time per mesh.  A 50 max VM eg = 6 service meshes to be setup side by side migrating in parallel.

Minimum bandwidth is 100Mbps to be able to do vMotion. 