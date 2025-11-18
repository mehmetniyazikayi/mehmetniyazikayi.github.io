---
title: "QAOA, Let's GOAOAOA !!!"
date: 2025-11-09
layout: post
tags: [qaoa, quantum, optimization, projects]
---

Today I’m releasing the first stable version of my **QAOA research repository**, now available at:

**GitHub:**  
https://github.com/mehmetniyazikayi/QAOA

This project brings all my QAOA-related work into **one unified structure** — covering multiple quantum SDKs, clean toy problems, consistent utilities, and reproducible workflows that run on both CPU and GPU setups.

---

## Why this matters

QAOA research is often fragmented.  
Every SDK uses its own:

- circuit style  
- optimizer interface  
- simulator backends  
- ansatz conventions  
- file structures  

This repository aims to unify these into one clean workspace — a **central hub** for all my QAOA experiments, tutorials, and research notes.

---

## What’s inside right now

Two fully working toy cases are already included:

### **1. Max-Cut**

- QUBO + Ising forms  
- QAOA circuits across SDKs  
- reproducible notebooks  
- utilities for graph generation + visualization

### **2. JSSP (Job Shop Scheduling Problem)**

- full scheduling QUBO  
- QAOA circuits with resource constraints  
- parsing tools  
- schedule visualization  
- realistic, nontrivial benchmark

---

## Overview Table

| Toy Case | Description | Status | SDKs Implemented |
|---------|-------------|--------|------------------|
| **Max-Cut** | Classic graph partitioning benchmark | Complete | Qiskit, Qulacs, CUDA-Q, PennyLane, QSim, QuTip, Qudora, Qibo |
| **JSSP** | Hard industrial scheduling problem | Complete | Qiskit (full), CUDA-Q (in progress), PennyLane (in progress) |
| **More to come** | Additional QUBO/Ising problems |  Planned | All supported frameworks |

---

## Upcoming posts

I will publish **dedicated blog posts** for both **Max-Cut** and **JSSP** soon.

Each will include:

- theoretical background  
- QUBO / Ising formulation  
- QAOA circuit explanation  
- backend differences  
- performance notes  
- visualization and sample outputs  


---

## Why I built this

1. I finally wanted *one* place to dump all my QAOA chaos — experiments, notes, scheduling problems, graph problems, and whatever else I end up doing at 3AM.  
2. I keep switching between Qiskit, PennyLane, CUDA-Q, QSim and Qulacs, and .. and ...yeah!!! and honestly… I got tired of pretending they all behave the same. So here’s my **fair arena** for them to fight it out.  
3. I write too many notebooks for tutorials. This repo is basically me telling myself: “stop rewriting the same code every week.”  
4. Also, it’s nice to have a clean HPC/QPU-ready setup so I don’t have to rebuild my environment every time I get a new idea.

---

## Next steps

- Write the deep-dive posts for Max-Cut and JSSP  
- Add warm-start QAOA because sometimes we all need a head start  
- Run GPU experiments until something breaks (and then fix it)  
- Benchmark mixers like it’s a personality test  
- Plot energy landscapes that look suspiciously like modern art  
- Experiment with QAOA bricks  
- Add more real-world QUBO problems because why not

More updates soon — this thing is definitely not slowing down :) 

