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

The midterm report covers two workstreams. First, a passive variant of py-minstrel-ht was developed to validate that user space rate selection matches the kernel Minstrel-HT — running alongside the kernel algorithm and comparing MRR chain decisions. Multiple bugs were identified and fixed, bringing error rates below 0.5% across all MRR positions. Second, the proposed joint power and rate controller is introduced: it uses a utility function that trades off throughput against interference cost to select rates, and tracks `safe` and `optimal` power levels per rate through cyclic power sampling.

[Read the full post on the Freifunk Blog](https://blog.freifunk.net/2023/07/26/gsoc-23-midterm-report-on-joint-power-and-rate-control-in-userspace/)
