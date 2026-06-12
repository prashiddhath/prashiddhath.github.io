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

*Originally published on the [Freifunk Blog](https://blog.freifunk.net/2023/09/25/gsoc-23-final-report-on-joint-power-and-rate-control-in-userspace/).*

## Passive Minstrel-HT: Final Validation

Further refinements to the passive py-minstrel-ht achieved 0.0% error rate across all MRR chain positions in multiple experiments on TP-Link WDR4900 routers (ATH9K chips) with frame aggregation enabled. Key fixes included correcting the AMPDU length calculation and resolving a peculiarity in how the kernel Minstrel-HT handles unused rate statistics.

## Joint Power and Rate Controller

The implemented joint controller draws from Minstrel-Blues. Its core components:

**Utility Function for Rate Selection**: Rates are ranked by a linear utility combining benefit (estimated throughput relative to max throughput) and cost (interference area proportional to power, interference duration inversely proportional to throughput). A weight factor controls the throughput-interference tradeoff.

**Power Updates**: At each update interval, reference and sample power levels are adjusted based on success probability relative to configurable tolerances (inc_prob_tol, dec_prob_tol). Reference power decreases when success probability is high; increases when it drops below the threshold. The best power for each rate is set to `sample_power + opt_pwr_offset`.

**Rate and Power Sampling**: Rate sampling is unchanged from Minstrel-HT. Power sampling cycles through the MRR chain; sampled rates use the reference power. Power probing explores the `safe` and `optimal` power levels.

## Performance Results

Experiments on TP-Link WDR4900 routers (ATH9K, iperf3 UDP) and MacBook Pro station (Flent TCP) showed:

* The joint controller consistently delivered **10-25% UDP throughput improvement** over both kernel Minstrel-HT and py-minstrel-ht without power control, even in **single-link setups**.
* Results held across utility weight factors of 1, 10, and 100.
* The improvement is attributed to better aggregation decisions and dynamic power level selection.

## Conclusion and Outlook

The joint controller shows strong promise. Future work will focus on:

* Running multi-AP interference experiments to demonstrate spatial reuse gains.
* Developing an independent power controller for newer closed-source WiFi chips that still support power control but restrict full algorithm access.

Thanks to Arne Kappen and Julius Schulz-Zander for their support throughout GSoC '23!
