---
layout: post
title: "Breaking the Storage Sound Barrier: Our DAOS Kernel-Bypass Performance Journey"
date: 2025-12-08 17:07:00 +01:00
tags: [hpc, storage, daos, io500, performance]
location: "Göttingen, Germany"
coordinates: "51.5413° N, 9.9158° E"
author: "Mehmet Niyazi Kayi"
---

This post summarizes the storage performance work my colleague Mojtaba and I carried out for the Scalable Storage Competition. What began as a straightforward attempt to evaluate DAOS on our hardware evolved into a deep dive into kernel bypass, NUMA topology, and every hidden switch that influences modern HPC storage performance.

The full benchmark repository is available here:  
**GitHub:** [DAOS Benchmarking Repository](https://github.com/mehmetniyazikayi/DAOS-io500-Benchmarking.git)

---

## What we actually built

We deployed and tuned a DAOS cluster across a set of CPU-only HPC nodes. The guiding principle was simple: remove every avoidable bottleneck between the application and the storage device. Achieving this required kernel-bypass NVMe access with SPDK, kernel-bypass networking using InfiniBand RDMA, careful NUMA-aware placement, and a significant amount of low-level system tuning.

The architecture is described in detail in the repository, but the operational idea is:

**The fewer layers between memory, network, and NVMe, the more the system begins to behave like a tightly integrated HPC engine rather than a traditional storage stack.**

---

## The headline result

Our strongest IO500 configuration reached a score of **80.465**, which is remarkable considering the modest hardware. We ran:

• 20 nodes  
• 64 processes per node  
• DFS API  
• InfiniBand RDMA  
• A long stonewall window  

The IO500 matrix makes it clear that this configuration significantly outperformed all alternatives.

---

## Why the performance jumped this much

DAOS is extremely sensitive to system architecture. The key contributors to the performance improvement were:

**Kernel bypass:** Eliminating the kernel from the critical path removes context-switching and TCP overhead, allowing direct communication between application memory and NVMe.

**NUMA alignment:** Each DAOS engine and NVMe device was pinned to its closest CPU and memory domain, preventing cross-socket latency penalties.

**System tuning:** IRQ pinning, CPU isolation, network parameter refinement, VFS adjustments, and other tuning steps ensured stable and predictable throughput.

**DFS API:** Using DFS instead of DFUSE bypasses the filesystem layer, exposing the raw performance potential of DAOS more directly.

---

## How big were the improvements?

From our measurements:

• IOPS improved by roughly 23 times  
• Bandwidth improved by around 139 times  
• The IO500 score improved by approximately 63 times  
• IOR Easy Write jumped by nearly 900 times  

At some point, we simply accepted that DAOS with proper tuning behaves very differently from the conventional HPC storage systems we were used to.

---

## A few moments worth remembering

TCP tried its best, but this was not its competition.  
SPDK, effective as always, was very quick to complain whenever our configuration deviated even slightly from its expectations.  
Several benchmark curves were suspicious enough that we reran tests multiple times just to confirm the results.  
Most importantly, working with Mojtaba throughout this project was essential. Every time I believed the system was fully optimized, he discovered new layers of potential improvement or new corners of the architecture worth exploring.

---

## Closing thoughts

The entire benchmarking effort was completed in an intense two-week window, from 17 November 2025 to 31 November 2025. This period involved continuous iteration, late-night debugging sessions, and a surprising number of “why is the throughput suddenly lower today?” moments. Despite the tight schedule, the structure, tuning workflow, and full IO500 evaluation came together quickly thanks to the close collaboration between Mojtaba and me. The compressed timeline ultimately forced clarity: every configuration that stayed in the final setup earned its place.

This project was more than a benchmark exercise. It was a genuinely rewarding collaboration that pushed us to understand how modern HPC storage behaves when the usual layers are stripped away. Mojtaba’s persistence, attention to detail, and willingness to challenge assumptions made this one of the most enjoyable technical explorations I’ve worked on.  

The outcome wasn’t just a strong IO500 score; it was a reminder of how much can be achieved when two people systematically dismantle every bottleneck in a system until the hardware finally shows what it is capable of.

