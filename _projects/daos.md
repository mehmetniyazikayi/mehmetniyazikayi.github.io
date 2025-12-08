---
title: "DAOS Performance Benchmarking for IO500"
summary: "Kernel-bypass NVMe + RDMA tuning for high-performance DAOS deployments in academic HPC environments."
hero: /assets/images/daos.png
repo: https://github.com/mehmetniyazikayi/DAOS-io500-Benchmarking.git
tags: [hpc, storage, daos, performance, io500]
tech: [SPDK, RDMA, NVMe, DAOS, HPC, Linux]
date: 2025-01-15
weight: 5
---

## Abstract

This project investigates the performance characteristics of DAOS when deployed with **kernel-bypass storage** (SPDK) and **kernel-bypass networking** (InfiniBand RDMA) across a multi-node academic HPC cluster.  
Through systematic tuning of NUMA topology, device affinity, network parameters, and DAOS engine configuration, we demonstrate that DAOS can deliver performance levels typically associated with significantly larger or vendor-backed systems.

Our benchmark environment achieves an **IO500 score of 80.465**, placing it well above typical installations of similar scale.

This work was conducted jointly with my colleague **Mojtaba**, whose expertise in low-level tuning and willingness to explore unconventional configurations was essential for pushing the system to its limits.

---

## System Overview

The deployed system consists of CPU-only nodes interconnected through an HDR InfiniBand fabric, with multiple NVMe devices per node.  
The DAOS storage layer is configured to operate without kernel involvement for both:

- **Storage Path:** Using SPDK to bypass the kernel’s NVMe stack  
- **Network Path:** Using RDMA to avoid the TCP/IP stack  

This architecture allows DAOS to approach hardware-level throughput with far lower latency variability than seen in classical POSIX-based HPC filesystems.

---

## Methodology

The evaluation followed a controlled, multi-stage tuning workflow:

### 1. Baseline Deployment
DAOS engines deployed using standard configuration on all nodes.

### 2. Kernel Bypass Activation
SPDK mapped directly to NVMe devices; RDMA activated at the transport level.

### 3. NUMA & Device Placement Optimization
NVMe devices, DAOS engines, and RDMA interfaces pinned to local CPU and memory domains to eliminate cross-socket penalties.

### 4. System-Level Tuning
- CPU isolation  
- IRQ distribution  
- Memory hugepage configuration  
- Network offload adjustments  
- VFS and RPC parameter tuning  

### 5. IO500 Evaluation
Multiple IO500 runs conducted with varying node counts, process counts, and API layers (DFUSE vs DFS).

---

## Evaluation

Across all test categories, kernel-bypass configurations consistently outperformed POSIX-mode setups.  
Notably, DFS (DAOS File System library) showed performance characteristics far closer to raw hardware behavior compared to DFUSE, which incurs traditional filesystem overhead.

Testing included:

- IOR Easy Write/Read  
- IOR Hard Write/Read  
- mdtest easy/hard  
- IO500 aggregate scoring  
- Long stonewall windows for stability assessment  

The performance was validated by repeated runs to eliminate transient anomalies.

---

## Results

The strongest configuration used:

- 20 nodes  
- 64 processes per node  
- DFS API  
- InfiniBand RDMA  
- 36,000-second stonewall  

This configuration achieved:

- **IOPS improvement:** ~23×  
- **Bandwidth improvement:** ~139×  
- **IO500 score improvement:** ~63×  
- **IOR Easy Write improvement:** ~900×  

These improvements highlight the magnitude of the kernel-bypass advantage in HPC environments.

---

## Conclusions

The project demonstrates that DAOS, when configured with proper attention to hardware topology and system-level tuning, can operate at performance levels dramatically higher than expected from academic-class infrastructure.

The collaboration behind these results was a key factor. Working with **Mojtaba** made it possible to investigate and validate optimizations at a level of detail that a single person rarely maintains throughout such a project. The resulting benchmark suite serves as both a scientific evaluation and a practical guide for improving storage performance in HPC environments.

This project not only produced competitive IO500 results but also provided deep insights into the behavior of modern storage systems when traditional bottlenecks are removed.

The entire benchmarking effort was completed in an intense two-week window, from 17 November to 31 November. This period involved continuous iteration, late-night debugging sessions, and a surprising number of “why is the throughput suddenly lower today?” moments. Despite the tight schedule, the structure, tuning workflow, and full IO500 evaluation came together quickly thanks to the close collaboration between Mojtaba and me. The compressed timeline ultimately forced clarity: every configuration that stayed in the final setup earned its place.
