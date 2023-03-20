---
layout: post
title: Custom certificates
share-title: HCX service mesh
subtitle: Impact on deploying HCX service mesh
tags: [AVS, HCX, service mesh]
---

During HCX service mesh creation one of the steps in there is to deploy the HCX MA or mobility agent on the IX appliance (interconnector).  This is normally part of the service mesh deployment itself and doesn't require any additional action from your part.

In a standard deployment, one without customer CA backed certificates the MA gets deployed to the IX appliance as part of the service mesh creation.
If and when your on-prem ESXi cluster is setup using **custom certificates** however, as it is considered a host in the on-premise ESXi clusterlandscape it needs to therefore authenticate using a host certificate signed by the on-premise CA or Certificate Authority.

Looking for clues the error message pointing in that direction

{: .box-note}
**Note:** Error adding Mobility agent host failed, unable to reach <IP address of IX>

If you have verified ports open between IX and connector (check the diagram) then most likely your on-prem environment works with on-prem/custom a Certificate Authority.  In order for the IX appliance to be allowed to join a custom certificate validated environment it will have to be equipped with a suitable certificate.

Lets first check and make sure we are in a custom certificate landscape

In the vCenter client select the vcenter itself, in configure/settings/advanced settings look up

### vpxd.certmgmt.mode

if this is set to custom then the ESXi cluster ONLY works with on-prem/customer Certificate Authority signed certificates.

In order to continue working with those you will need to drop the CA and the cert on the IX appliance directly

There's two solutions to work with this however:

## switching from customer to thumbprint

Before doing this, check if this is not going to generate issues as switching it to thumbprint will basically remove all validity cert checks.  It will simply check to see if there's a certificate but will not validate it

## get a new CA signed certificate

THis is the only clean solution as it will get a signed cert by the CA you want to use (same CA as the one setup in vCenter)

Here's how you do that:

ssh into HCX connector as admin.  As a reminder you deployed the HCX connector on premise and set the password for this user yourself

| prompt- ccli | |
| promp- list | his will provide you with a list of all of the appliances the connector sees |
| prompt- go 0 | The IX appliance |
| prompt- ssh | Drop into the IX appliance itself |
| prompt- cd /etc/vmware/ssl | cd into this directory where the self signed certs are |
+--+--+--+
|  |  |  |
+--+--+--+
|  |  |  |
+--+--+--+
|  |  |  |
+--+--+--+
|  |  |  |
+--+--+--+
|  |  |  |
+--+--+--+
|  |  |  |
+--+--+--+