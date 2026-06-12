---
title: "GSoC '23: Midterm Report on Joint Power and Rate Control in Userspace"
date: 2023-07-26
permalink: /posts/2023/07/gsoc23-midterm-joint-power-rate/
tags:
  - gsoc
  - wifi
  - rate-control
  - power-control
---

*Originally published on the [Freifunk Blog](https://blog.freifunk.net/2023/07/26/gsoc-23-midterm-report-on-joint-power-and-rate-control-in-userspace/).*

## Passive Minstrel-HT Validation

Before extending py-minstrel-ht with power control, it is crucial to ensure the user space rate control mirrors the kernel Minstrel-HT behavior. A **passive py-minstrel-ht** was developed that runs alongside the kernel algorithm: the kernel performs the actual rate control, while py-minstrel-ht passively records all its rate selections using the same statistics, enabling a direct comparison.

The key metrics compared were:
* **Probability estimation**: The Butterworth filter in user space acts identically to the kernel. Minor differences (up to 0.2%) stem from floating-point precision loss in the kernel's integer scaling.
* **Throughput estimation**: Matches almost exactly, with negligible errors from floating-point precision differences.
* **Rate setting (MRR chain)**: Experiments of 20 minutes each showed error rates below 0.5% in most MRR indices across multiple chip types.

Investigating the passive experiments revealed and fixed several bugs in py-minstrel-ht:
* Probability calculation did not account for packet counts from the last update interval.
* The airtime threshold for the maximum probability rate was computed incorrectly.
* Unused rates were erroneously excluded from the maximum probability rate selection.
* Estimated throughput for unused rates was not being updated, only their success probability.

## Proposed Joint Power and Rate Controller

The power control extension draws inspiration from Minstrel-Blues (Prof. Thomas Hühn, 2011). Key design elements:

**Best Rate Selection with Utility Function**: Instead of selecting rates purely by estimated throughput, the joint controller uses a linear utility function that trades off throughput (benefit) against interference to other transmissions (cost). The cost factor is approximated from the interference area (proportional to power) and interference duration (inversely proportional to throughput).

**Power Sampling**: The algorithm tracks two power levels per rate: `safe` (highest success probability) and `optimal` (lowest power still achieving comparable throughput). Power sampling cycles through the MRR chain, with sampling priority given to best-throughput rates.

**Configurable Parameters**: delta (min success probability for safe power), sigma (tolerance for optimal power), pwr_inc/pwr_dec (power step sizes), and opt_pwr_offset (offset from sample to best power).

## Next Steps

The second half of GSoC '23 will focus on testing and extending py-minstrel-ht with power tuning on ath9k hardware (routers just arrived). The passive validation provides a solid foundation for comparing the joint controller against kernel Minstrel-HT.
