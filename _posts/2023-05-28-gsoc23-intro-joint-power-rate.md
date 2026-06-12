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

This post introduces the GSoC '23 project on joint power and rate control in user space. While rate control algorithms like Minstrel-HT optimize transmission rates, they typically use a fixed high power level that causes unnecessary interference in dense networks. The project extends the existing `py-minstrel-ht` package with a power tuning module that finds the lowest power level still delivering peak throughput. Three modes are planned: fixed power, power ceiling, and maximum throughput. The post provides background on the WPCA API that enables joint rate and power setting from user space.

[Read the full post on the Freifunk Blog](https://blog.freifunk.net/2023/05/28/gsoc-23-joint-power-and-rate-control-in-userspace-for-freifunk-openwrt-mesh-access-networks/)
