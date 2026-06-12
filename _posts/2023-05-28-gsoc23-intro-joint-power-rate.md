---
title: "GSoC '23: Joint Power and Rate Control in Userspace for Freifunk OpenWrt Mesh & Access Networks"
date: 2023-05-28
permalink: /posts/2023/05/gsoc23-intro-joint-power-rate/
tags:
  - gsoc
  - wifi
  - rate-control
  - power-control
---

*Originally published on the [Freifunk Blog](https://blog.freifunk.net/2023/05/28/gsoc-23-joint-power-and-rate-control-in-userspace-for-freifunk-openwrt-mesh-access-networks/).*

Hello everyone! I'm Prashiddha, a former GSoC contributor with Freifunk in 2022. For GSoC '23, I'll be working on a resource allocation algorithm that selects optimum transmission rates in conjunction with the optimum power level for OpenWRT routers.

## Overview of Joint Power and Rate Control

A rate control algorithm like Minstrel-HT determines the best transmission rates for maximum throughput, but typically assigns a high static power level that can cause interference in dense networks. It is well established that for a given rate, even though higher transmit power implies a higher SNR, it does not necessarily translate to higher throughput. The goal is to use the lowest power level still capable of providing optimum throughput, enabling better interference management and increased spatial reuse.

## WiFi Resource Allocation in Userspace

As part of the [SupraCoNeX](https://supraconex.de/) research, the WiFi Parameter Control API (WPCA) for OpenWrt access points enables WiFi resource allocation from user space. The API exposes relevant mac80211 kernel information (MCS rates, packet ACK counts) and has been extended to allow MCS rates to be set jointly with power levels, making a joint rate and power controller in user space possible.

## Extending Py-Minstrel-HT with Power Control

The plan is to extend the existing `py-minstrel-ht` package with a power tuning module. Three power modes will be realized:

* **Fixed power**: Sets all rates to a specified power level.
* **Power ceiling**: Specifies the maximum allowable power level.
* **Maximum throughput**: Dynamically finds the lowest power level that still delivers peak throughput — the most complex mode, as the wireless channel is highly dynamic.

## Deliverables

* Extension of py-minstrel-ht with a power controller, complete documentation, and execution guide.
* Ready-to-run demo scripts showcasing the joint rate and power control.
* Evaluation of the joint controller across different modes and against other rate controls.

Thanks for reading! Feel free to reach out.
