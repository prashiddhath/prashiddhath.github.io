---
title: "Minstrel TX Rate Control in User space – GSoC '22"
date: 2022-06-13
permalink: /posts/2022/06/gsoc22-intro-minstrel-userspace/
tags:
  - gsoc
  - wifi
  - rate-control
---

This introductory post for GSoC '22 covers the motivation and plan for implementing [Minstrel HT](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/tree/net/mac80211/rc80211_minstrel_ht.c) — Linux's default WiFi rate control algorithm — in user space for OpenWRT access points. Development in kernel space is restricted (no floating-point, high crash risk, limited debugging), making a Python-based user space variant valuable for research and experimentation. The post introduces the WiFi-Manager package and outlines the planned deliverables: a fully functional user space Minstrel HT with documentation, demo scripts, and performance comparisons against the kernel variant.

[Read the full post on the Freifunk Blog](https://blog.freifunk.net/2022/06/13/minstrel-tx-rate-control-in-user-space-gsoc-22/)
