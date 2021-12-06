---
layout: post
title:  "Benchmarking CPU Affinity For Fuzzing"
date:   2021-12-05
---

## Introduction
Fuzzers work by generating input, providing that input to the target program, and detecting if that input causes the target program to execute in an interesting way, such as a segmentation fault. Significant research has been done on each of these steps, using things such as [grammars](https://github.com/googleprojectzero/domato) to intelligently generate input, [sanitizers](https://clang.llvm.org/docs/AddressSanitizer.html) to detect subtle execution flaws, and [edge coverage](https://clang.llvm.org/docs/SanitizerCoverage.html) to determine when a program should be mutated further.

Unless you are particularly lucky, each generated sample only has a small probability of finding incorrect execution. Thus, in order to find a bug, it helps to repeat this process a large number of times! 

## LibAFL

## Inprocess
`libfuzzer` libfuzzer 

## Forkserver

## Appendix - Hardware Used

|               |                     |
| --------------| ------------------- |
| OS            | Ubuntu 20.04.3      |
| Kernel        | 5.11.0-41-generic   |
| CPU           | AMD Ryzen 3900x     |
| RAM           | 64 GB               | 