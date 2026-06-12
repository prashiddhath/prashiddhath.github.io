---
title: "GSoC '23: Final Report on Joint Power and Rate Control in Userspace"
date: 2023-09-25
permalink: /posts/2023/09/gsoc23-final-joint-power-rate/
tags:
  - gsoc
  - wifi
  - rate-control
  - power-control
---

The final GSoC '23 report presents the completed joint power and rate controller, inspired by Minstrel-Blues. The controller selects rates using a utility function balancing throughput and interference cost, while dynamically adjusting reference and sample power levels based on success probability thresholds. Experiments on TP-Link WDR4900 routers (ATH9K, UDP via iperf3) and a MacBook Pro station (TCP via Flent) showed consistent 10-25% throughput improvements over kernel Minstrel-HT — even in single-link setups — attributed to better aggregation decisions and dynamic power selection. Future work targets multi-AP spatial reuse experiments and an independent power controller for newer closed-source WiFi chips.

[Read the full post on the Freifunk Blog](https://blog.freifunk.net/2023/09/25/gsoc-23-final-report-on-joint-power-and-rate-control-in-userspace/)
