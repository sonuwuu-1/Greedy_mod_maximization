# Greedy Modularity Maximization for Community Detection

## Overview

This project implements a **simplified version** of the **Greedy Modularity Maximization algorithm** for community detection in graphs.
The algorithm identifies **communities (clusters)** in a network by **maximizing modularity**, which measures the strength of a community structure.

It produces results **similar to NetworkX’s built-in** `greedy_modularity_communities()` function, but with a **simpler and more educational** approach.

---

## What is Community Detection?

Community detection aims to divide a graph into groups of nodes (communities) such that:

* There are **many edges within communities**, and
* **Few edges between communities**.

The **modularity (Q)** of a partition measures how well the network is divided:

**Q = (1 / 2m) × Σᵢⱼ [Aᵢⱼ − (kᵢ × kⱼ) / (2m)] × δ(cᵢ, cⱼ)**

where:

* **Aᵢⱼ** = 1 if edge exists between i and j, else 0
* **kᵢ, kⱼ** = degrees of nodes i and j
* **m** = total number of edges
* **δ(cᵢ, cⱼ)** = 1 if nodes i and j are in the same community

---

## Algorithm Workflow

1. **Initialization:** Each node starts as its own community.
2. **Iteration:** Compute modularity gain for all possible community merges and merge the pair with the highest increase.
3. **Termination:** Stop when no merge increases modularity further.
4. **Output:** Final community partition with maximum modularity.

---

## Time Complexity Analysis

Let:

* **n** = number of nodes
* **m** = number of edges
* **c** = number of communities (initially **n**)

---

### 🔹 1. Modularity Computation

Each call to `modularity()` iterates over all pairs of nodes **within the same community**.

**Time Complexity:** O(n²)

---

### 🔹 2. Merge Evaluation

At each iteration, all pairs of communities are tested for modularity gain → roughly **O(c²)** merges.
Each merge recomputes modularity (**O(n²)**), leading to:

**O(c² × n²)**

Initially **c ≈ n**, giving a **worst-case time complexity of O(n⁴)**.
However, since communities merge quickly and most real-world graphs are sparse,
the **practical runtime** is approximately:

**O(n³)**

---

### 🔹 3. Space Complexity

| Component                    | Space     |
| ---------------------------- | --------- |
| Adjacency list & degree maps | O(n + m)  |
| Community lists              | O(n)      |
| **Total Space**              | **O(n²)** |
