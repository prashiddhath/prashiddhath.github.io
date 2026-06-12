---
title: "Minstrel TX Rate Control in User space – GSoC '22"
date: 2022-06-13
permalink: /posts/2022/06/gsoc22-intro-minstrel-userspace/
tags:
  - gsoc
  - wifi
  - rate-control
---

*Originally published on the [Freifunk Blog](https://blog.freifunk.net/2022/06/13/minstrel-tx-rate-control-in-user-space-gsoc-22/).*

Hi everyone! I'm Prashiddha. I have recently graduated from Jacobs University Bremen with a BSc. Computer Science. For the past year, I have been involved in the research and development of open-source software at [SupraCoNeX](https://supraconex.de/), primarily focusing on facilitating rate control in user space.

For GSoC '22, I'll be working on implementing and testing [Minstrel HT](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/tree/net/mac80211/rc80211_minstrel_ht.c), the default WiFi rate control for Linux-based OpenWRT OS, in user space.

## What is WiFi Rate Control?

A typical WiFi network consists of at least a sender and a receiver that communicate through the propagation of radio frequencies within the license-free ISM band. The choice of a transmission scheme between the WiFi devices determines the theoretical network throughput or data rate. A metric called the Modulation Coding Scheme (MCS) Index has been defined to help better understand the WiFi data rates and the RF environment of the network.

With newer IEEE 802.11 standards such as IEEE 802.11ax, there are hundreds of available MCS rates for transmission. The performance of WiFi networks is far from optimal, and there have been significant efforts to develop WiFi rate control algorithms that dynamically adapt transmission data rates in response to the varying wireless channel conditions.

## Motivation

In Linux-based OpenWRT WiFi devices, the mac80211 subsystem in the kernel space is responsible for rate control. Development in kernel space is restricted to integer value operations, and capabilities for prototyping and debugging are highly restricted. Given these limitations, the need for a user space rate control algorithm is apparent. My GSoC '22 project focuses on implementing a user space variant of Minstrel HT with experiments designed to compare performance with its kernel space counterpart.

## Deliverables

* Software architecture of the user space Minstrel HT implementation in Python.
* Proper documentation and guide on working with the Minstrel HT package.
* Ready-to-run demo script to showcase the potential of user space Minstrel HT.
* Detailed analysis of WiFi rate control experiments for performance comparison between kernel and user space Minstrel HT.

## What's Already Done?

Prior to GSoC '22, I had already implemented a working version of the user space Minstrel HT in Python using WiFi-Manager as part of my bachelor thesis. Multiple experiments were conducted to evaluate various parallelization methods (async task, thread pool, process pool), with async tasks proving to be the best scheme.

## What's Next?

* Changing the output to a live printout of the rate statistics table.
* Extending user space Minstrel HT with functionalities from the kernel variant such as calculating retransmission counts, random sample tables, and reducing spatial streams.
* Adding the Butterworth Filter currently used by the kernel Minstrel HT.

Thanks for reading!
