---
layout: post
title: "Build and Secure Networks in Google Cloud"
published: true
---

I recently completed the '[Build and Secure Networks in Google Cloud: Challenge Lab](https://www.qwiklabs.com/focuses/12068?parent=catalog)' by Qwiklabs and found it quite interesting.

This lab demonstrates firewall rules in action by getting you to implement rules that allow access to VMs via `SSH` & `HTTP` within specific IP ranges.

The process is entirely hands-on, but I felt it lacked some detail about why you must incorporate certain security practices. Perhaps, they expected users to be familiar with these concepts before undertaking the lab.

Either way, in this short blog, I will explain why the implementation provided in this lab aids in securing a service in GCP.

## Present State

At the beginning of the lab, you are provided with the following environment in GCP—a straightforward architecture consisting of a VPC network with two subnets and two VMs.

<p style="margin-top: 3%; text-align:center;">
<img style="box-shadow: 0px 0px 10px 0px rgb(0 0 0 / 50%); max-width: 85%" src="../images/secure-networks-gcp/initial-layout.png" />
<p style="margin-bottom: 3%; font-style: italic; text-align:center;" >Figure 1: Initial GCP Setup. Source: Qwiklabs</p>
</p >

This architecture serves the website to users, but parts of it don't make much sense or are too permissive.

Fundamentally, here are the issues I see with this setup:
1. The `bastion` VM is redundant. Since the `bastion` VM cannot SSH into the `juice-shop` VM, there would be no reason to have it.
2. Users can `SSH` directly into the `juice-shop` VM from their local machine. This means that the `juice-shop` VM is exposed to the outside world via Port `22`.
3. Permissive firewall rules. Although it's not apparent from the diagram, we know that both the `bastion` and `juice-shop` VM must be open to port `22` via the internet.

## Future State

This lab aims to transform the above configuration into the one below. The main layout remains the same, but it is made more secure through the setup of Identity-Aware Proxy (IAP) and Firewall rules.

<p style="margin-top: 3%; text-align:center;">
<img style="box-shadow: 0px 0px 10px 0px rgb(0 0 0 / 50%); max-width: 85%" src="../images/secure-networks-gcp/future-layout.png" />
<p style="margin-bottom: 3%; font-style: italic; text-align:center;" >Figure 2: Secure GCP Setup, implemented as part of the lab. Source: Qwiklabs</p>
</p >

Essentially, this implementation resolves the security flaws above by:
1. Enabling `SSH` to the `bastion` VM via IAP. This means that only authorized users can `SSH` into the VM, and port `22` is not open to the internet.
2. Access to `juice-shop` is only possible via the `bastion` instance. Therefore, users can no longer access the VM directly from a local machine but instead go via the management network, adding a layer of security.
3. Restricted firewall rules. The `bastion` instance is only open to `SSH` from IAP, and `juice-shop` is only to `bastion`. `HTTP` is the only port available to the outside world and is limited to `juice-shop`.

## Summary

Since completing this lab by Qwiklabs, I've better understood the parallels between securing infrastructure on-prem and in the cloud. The concepts explained here could be easily translated to an on-prem environment with a similar setup.

Basically, by the end of the lab, you have an environment that serves a website to the internet and is only manageable via the management network. Perhaps, this adds some complexity to a straightforward layout, but it ensures the safety of your data and infrastructure.