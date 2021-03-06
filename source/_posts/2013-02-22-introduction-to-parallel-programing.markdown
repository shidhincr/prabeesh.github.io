---
layout: post
title: "Introduction to Parallel Programing"
date: 2013-02-22 23:16:54 +0530
comments: true
categories: 
---
This post focuses on parallel computing on the GPU. Parallel computing is a way of solving large problems by breaking them into smaller pieces and run these smaller pieces at the same time.
###Main reasons of technical trends on the parallel computing on the GPU
Modern processors are made from transistors. And each year, those transistors get smaller and smaller. The feature size is the minimum size of a transistor on a chip. As the feature size decreases, transistors get smaller, run faster, use less power, and put more of them on a chip. And the consequence is that ,more and more resources for computation every single year. One of the primary feature of a processors is clock speed . Over many years, the clock speeds continue to go up. However, over the last decade, that have essentially remained constant. Even though transistors are continuing to get smaller and faster and consume less energy per transistor, Running a billion transistors generates high amount of heat . since we can't keep all these processors cool, Power has emerged as a primary driving factor.

Traditional CPUs has very complicated control hardware. This allows flexibility in performance, but as control hardware gets more complicated, it becomes more expensive in terms of power and design complexity. So might choose to build simpler control structures. And the way is that going to build that data path in the GPU is by building a large number of parallel compute units. Individually, those compute units are small, simple and power efficient. So put a very large number of them on a single chip. More generally program them in such a way that they can all work together to solve complex problems. A high end GPU contains over 3,000 arithmetic units, ALUs, that can simultaneously run 3,000 arithmetic operations. Gpus can have tens of thousands of parallel pieces which are active at the same time. each of those pieces of work a thread, and a modern GPU may be running up to 65,000 concurrent threads. Together, all this computing power has the potential to solve the problems faster.

To build a power efficient processor, choice is minimizing latency. Latency is the amount of time to complete a task. The other choice is throughput. Throughput is tasks completed per unit time. Regulating throughput is the right approach,because Latency Lags Bandwidth
###CUDA(Computer Unified Device Architecture)
CUDA is a parallel programming platform. The programming model implemented by the GPU is created by NVIDIA. CUDA gives developers to access the virtual instruction set memory of the parallel computational elements in CUDA GPUs. Unlike CPUs, GPU have a parallel throughput architecture that emphasizes executing many concurrent threads slowly, rather than executing a single thread very quickly. This approach for solving general purpose problems on GPU is known as GPGPU. 

The CUDA programming model allows us to program both CPU and GPU with one program so that the power of the GPU in programs. At First, the CPU allocates storage space on the GPU. Then, the CPU copies some input data from the CPU to the GPU.and the Next step is, CPU calls some kernels watching these kernels on the GPU that process this data. And finally, the CPU copies the results back to the CPU from the GPU.

This blog is my short notes as part of the course now I am doing in the Udacity [Intro to Parallel Programming](https://www.udacity.com/course/cs344).
