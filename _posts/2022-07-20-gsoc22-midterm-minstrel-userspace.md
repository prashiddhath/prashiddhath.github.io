---
title: "Update on Minstrel TX Rate Control in User space – GSoC '22"
date: 2022-07-20
permalink: /posts/2022/07/gsoc22-midterm-minstrel-userspace/
tags:
  - gsoc
  - wifi
  - rate-control
---

*Originally published on the [Freifunk Blog](https://blog.freifunk.net/2022/07/20/update-on-minstrel-tx-rate-control-in-user-space-gsoc-22/).*

Hi everyone! As the first evaluation of GSoC '22 approaches, this post provides a detailed update on the progress of Minstrel HT WiFi rate control in user space.

## New Estimators

### Butterworth Filter

The kernel Minstrel HT replaced EWMA with a new estimator based on the SuperSmoother (Butterworth) filter developed by John F. Ehlers. The Butterworth filter has now been added to the user space Minstrel HT with the period set to 16. The filter calculates the average success probability of a data rate where `curr_prob` denotes the success probability in the current 50ms update interval.

### Exponentially Discounted Averaging and Variance

An exponentially discounted filter has been added for research purposes, capable of discounting with respect to both the number of observations and the time of those observations using two parameters alpha and beta in [0,1]. This allows a trade-off between emphasizing number of observations versus recency of those observations.

## Changes to Output

The output has been changed to match the kernel Minstrel HT debug output format, with two new file types per access point:

* **rc_stats**: A human-readable rate statistics table showing average success probability and average throughput for each data rate across all three implemented filters (EWMA, Exponentially Discounted, Butterworth).
* **rc_stats_csv**: Stores all RateTable data throughout execution for offline analysis and comparison with kernel Minstrel HT.

## Configuration File

A new configuration script `config.py` allows tweaking filter parameters, rate control properties (sample interval, update interval), and selecting which filter to use for rate control.

## First Analysis of Estimators

An experiment was conducted for 10 minutes on a BananaPi router (MediaTek 7622 chip) with an iperf3 connection, yielding rate statistics for 24 data rates. Results comparing the estimated throughput across the three filters were visualized using seaborn.

Thanks for reading!
