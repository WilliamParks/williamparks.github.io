---
layout: post
title:  "Benchmarking CPU Affinity For Fuzzing"
date:   2021-12-05
---

## Introduction
Fuzzers work by generating input, providing that input to the target program, and detecting if that input causes the target program to execute in an interesting way, such as a segmentation fault. Significant research has been done on each of these steps, using things such as [grammars](https://github.com/googleprojectzero/domato) to intelligently generate input, [sanitizers](https://clang.llvm.org/docs/AddressSanitizer.html) to detect subtle execution flaws, and [edge coverage](https://clang.llvm.org/docs/SanitizerCoverage.html) to determine when a program should be looked at further.

Unless you are particularly lucky, each generated sample only has a small probability of finding incorrect execution. Thus, in order to find a bug, it helps to repeat this process a large number of times!

However, per [Fuzzing: On the Exponential Cost of Vulnerability Discovery](https://mboehme.github.io/paper/FSE20.EmpiricalLaw.pdf), "finding linearly more bugs in the same time requires exponentially more machines. For instance, for every new bug we want to find in 24 hours, we might need twice more machines". Thus, the economics of fuzzer speed improvements dictate that we need a significant performance increase for the time spent on such efforts. 

However, which optimizations are worth doing? This post takes a look at [Processor Affinity](https://en.wikipedia.org/wiki/Processor_affinity) to measure the effect that it has on fuzzer performance.

## CPU Core Affinity
All operating systems 

## LibAFL

## Inprocess
`libfuzzer` libfuzzer 

## Forkserver

## Appendix - Hardware

|               |                     |
| --------------| ------------------- |
| OS            | Ubuntu 20.04.3      |
| Kernel        | 5.11.0-41-generic   |
| CPU           | AMD Ryzen 3900x (12 cores/24 hardware threads)    |
| RAM           | 64 GB               | 