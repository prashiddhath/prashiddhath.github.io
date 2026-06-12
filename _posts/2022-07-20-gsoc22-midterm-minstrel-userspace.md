---
title: "Update on Minstrel TX Rate Control in User space – GSoC '22"
date: 2022-07-20
permalink: /posts/2022/07/gsoc22-midterm-minstrel-userspace/
tags:
  - gsoc
  - wifi
  - rate-control
---

The midterm report covers three main additions to the user space Minstrel HT. First, two new estimators were implemented: the Butterworth filter (now used by the kernel) and an Exponentially Discounted Averaging filter for research. Second, the output was redesigned to match the kernel debug format, producing human-readable rate statistics tables and CSV files for offline analysis. Third, a configuration module was added to let users tune filter parameters and rate control properties. The post concludes with a first analysis comparing the three filters on real WiFi hardware.

[Read the full post on the Freifunk Blog](https://blog.freifunk.net/2022/07/20/update-on-minstrel-tx-rate-control-in-user-space-gsoc-22/)
