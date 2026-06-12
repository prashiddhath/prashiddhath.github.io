---
title: "Final Report on Minstrel TX Rate Control in User space – GSoC '22"
date: 2022-09-12
permalink: /posts/2022/09/gsoc22-final-minstrel-userspace/
tags:
  - gsoc
  - wifi
  - rate-control
---

The final GSoC '22 report details all contributions to the user space Minstrel HT. New kernel functions were ported including dynamic retransmission calculation, sudden-death detection, and spatial stream reduction. The codebase was restructured into separate minstrel and sample modules, significantly reducing computation time. A rate-setting experiment framework was built to validate rate control behavior on real hardware. Additionally, a user space implementation of the Sample Rate algorithm (Bicket, 2005) was developed as a standalone Python package. All initial goals were met and exceeded.

[Read the full post on the Freifunk Blog](https://blog.freifunk.net/2022/09/12/final-report-on-minstrel-tx-rate-control-in-user-space-gsoc-22/)
