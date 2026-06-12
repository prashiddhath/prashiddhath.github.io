---
title: "Final Report on Minstrel TX Rate Control in User space – GSoC '22"
date: 2022-09-12
permalink: /posts/2022/09/gsoc22-final-minstrel-userspace/
tags:
  - gsoc
  - wifi
  - rate-control
---

*Originally published on the [Freifunk Blog](https://blog.freifunk.net/2022/09/12/final-report-on-minstrel-tx-rate-control-in-user-space-gsoc-22/).*

Hi everyone! With GSoC 2022 concluding, this final post covers all accomplishments, conclusions, and future outlook for Minstrel TX Rate Control in user space.

## Goals (All Completed)

* Adding proper output to aid in rate control analysis.
* Extending user space Minstrel HT with missing functions from the kernel.
* Addition of new estimators/filters for research purposes.
* Proper documentation, demo, and guide.

## Key Contributions

### New Output System

The old printout-based output was replaced with a dedicated file and folder per access point. Each AP produces `rc_stats` (human-readable) and `rc_stats_csv` (for offline analysis) files, updated at every 50ms interval.

### New Functions from Kernel Minstrel HT

* **get_avg_ampdu_len**: Calculates average AMPDU length for a connected station.
* **calc_retransmit**: Dynamically computes retry count for each rate in the MRR chain (previously static at 10).
* **check_sudden_death**: Detects sudden packet loss; downgrades affected rates when packet count exceeds 30 with 75% loss.
* **prob_rate_reduce_streams**: Finds a more robust rate using fewer streams than the current max probability rate.
* **downgrade_rate**: Reduces the best or second-best throughput rate to the max group throughput rate from a lower stream group.

### New Estimators

Two new filters added alongside the existing EWMA:
* **Butterworth Filter**: Now the primary filter, matching the kernel Minstrel HT.
* **Exponentially Discounted Averaging and Variance**: For research, discounts by both number of observations and recency.

### Codebase Restructure

The minstrel module was split into `minstrel` and `sample` modules, enabling each station to have an independent Sample object. Redundant loops were merged, significantly reducing computation time.

### Rate-Setting Experiment Framework

A separate repository with scripts to configure and run rate-setting experiments was created — for each supported rate, the experiment sets the rate, waits for stabilization, then collects packet statistics for a configurable duration.

### Sample Rate Algorithm

Implemented John C. Bicket's [Sample Rate](https://www.cse.iitb.ac.in/~mythili/teaching/cs653_spring2014/references/samplerate.pdf) algorithm (2005) in user space as a Python package using WiFi-Manager. Unlike Minstrel HT, Sample Rate is packet-based rather than time-interval based.

## Future Work

* Test on embedded hardware (current tests only on laptops).
* Add built-in compression for `rc_stats_csv` which grows quickly.
* Implement random sampling table from kernel Minstrel HT.
* Extend AMPDU length usage in throughput estimation once API support is available.

Thanks to my mentor, Prof. Thomas Hühn, for his guidance throughout the project!
