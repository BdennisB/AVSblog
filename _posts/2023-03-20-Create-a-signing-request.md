---
layout: post
title: Create a certificate signing request
share-title: HCX service mesh
subtitle: Working with customer certs on ESXi
tags: [AVS, HCX, service mesh]
---

This file will be used as input for the actual signing request.  Copy/paste this into a file called new.conf

*Important* make sure you have openssl installed onto the VM where you will be doing this

<img title="a title" alt="Alt text" src="/AVSblog/assets/img/screen1.jpg">


Issue the certificate signing request or CSR

*openssl req -newkey rsa:2048 -keyout new.key -out new.csr -config new.conf -nodes*

This will create a new file private key called new.key and new.csr

once done - lets now verify this to make sure there's no errors

*openssl req -in new.csr -noout -text*

send the csr file (new.csr) to have it signed by your internal PKI (CA).  Make sure you tell them about the SAN names and/or one or multiple IPs.

Once signed and you have the option make sure to download the files in base64 format.  You will be sent, root CA including (if any) intermediate certs

To create a PEM file containing all relevant info, if needed:

*cat signed_cert.crt new.key cacerts.crt > multi_part_new.pem*







T