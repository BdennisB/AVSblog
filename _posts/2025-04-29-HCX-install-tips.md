---
layout: post
title: HCX
share-title: HCX install tips
subtitle: HCX recommendations setting it up
tags: [AVS, HCX, profiles]
last_modified_at:   2025-04-29 21:27:00 +0000
---
The HCX connector appliance is I think worth a little bit of attention.  
Often overlooked and quickly dismissed it is a vital touch point in the entire setup.  Troubleshooting it therefore, to at least get a feel of how it is behaving could be a usefuly thing to learn about.

# Activation
As part of the HCX activation/setup phase you need to work through the following steps
* Activating it, this means generating a perpetual license key using the AVS portal (again see our documention - pick resources (top right corner for the link))
* Connect it to local vCenter (full admin credentials required here)
* Setup up SSO

Lets zoom in on the SSO part.  If you are not using the vsphere.local domain here.  Please make sure you specify the user preceeded by its FQDN.  Don't use the netbios name but fully qualify it.

{: .box-warning}
**Warning:** If you have a proxy requirement here, please check one of the other posts on this blog for more info as it requires proxy exclusions to be set!

With all of that in place prior to either restarting the connector or resarting the services individually, which can be done from the admin part of the HCX connector itself btw please ensure you have the following handy

* ensure proxy allows connectivity toward *connect.hcx.vmware.com* and *hybridity.depot.vmware.com*.  It will save you a lot of hassle.  Double checking that can be done by hitting the check button when setting the proxy itself or, as described in a different post use curl on the connector prompt.
* ensure you have access to the on-prem vcenter.  This is required to ensure all plugins are correctly put in place when the connector restarts.

# service mesh config

Once you have established the HCX plugin is correctly installed on the vCenter on-prem (home - drop down list should have made HCX visible as an option) it is now time to start setting up the service mesh.  Here's a few tips and tricks to turn this into a first time right time experience.

## network profile

I always create 2 at the very minimum and use management for uplink.  Ensure you have at least 4 IPs (as per our checklist), 2 in vMotion and 2 in Management.  
If you have a dedicated replication network, ensure you have an IP in there as well to create a separate profile for it.
The IX appliance (1 per each service mesh btw) uses the network that it will belong to to commmunicate with vcenter, nsx manager, NTP and DNS.  In case you therefore want to use a seperate network please make sure it can route to the networks where these services are in.  

{: .box-note}
**Note:**  IF you want to replicate your VMs across using Replicated Assisted vMotion ensure your vMotion network is exposed on the VDS!  If you are not planning on using this facility you can also opt to expose it on the VSS (if still in use)

## compute profile

All our new (March 2023) SDDCs come with enterprise HCX activated by default.  There is no need to therefore raise an SR again as it was the case before.  Because of this you will see Replication Assisted vMotion selectable when you go through the motions of setting up the compute profile

## limits

Every service mesh created between a connector and an AVS manager.  In essence therefore between an on-prem vCenter and an AVS SDDC needs to take into account the following:
- **ONE** IX/WO appliance
- Up to **TEN** NE appliance pairs.  This means a maximum of 80 VLANs can be supported by **ONE** service mesh.
- ONE AVS SDDC supports up to **TEN** service meshes meaning we can 'link up' so to speak 10 source vCenters with one AVS SDDC

 {: .box-note}
**Note:**  Keep in mind NE HA.  If you want to increase resilience on the NE appliance pairs you can by activating HA.  THis effectively means creating 2 NE appliance pairs.  One tunnel being the active one, the other one the standard.  THis will **reduce** the amount of VLANs you are allowed to stretch/service mesh.  Keep in mind the **TEN** appliance max count.

Check <https://configmax.esp.vmware.com/> for the latest on the limits.
