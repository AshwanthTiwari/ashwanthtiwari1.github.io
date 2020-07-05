---
layout: default
title: Azure Site Recovery
date: 2020-04-27 13:45
category:
author:
tags: [Azure]
summary:
---

In few of my roles I was heavily involved in designing and implementing disaster recovery using VMware SRM.

I have had some exposure to Azure site recovery. However, I wanted to setup one in lab to see the differences.

Scenario: Azure to Azure DR architecture with couple of Windows VM provisioned using terraform.

High-level Architecture or setup -

![an image alt text]({{ https://github.com/AshwanthTiwari/tiwariap.github.io }}/images/ASR-lab.png "an image title")

Steps -

1. Source location or Primary DC - couple of Windows VM using some automation such as terraform

2. Destination location - Setup a recovery vault. The setup is pretty straightforward

![an image alt text]({{ https://github.com/AshwanthTiwari/tiwariap.github.io }}/images/ASR-vaultsetup1.png "an image title")

3.There are some other requirements such as Cache storage account in source location, storage account in target location. You can either setup these beforehand or ASR will do it for you.

*****WIP