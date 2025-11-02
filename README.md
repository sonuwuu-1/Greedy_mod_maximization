# Greedy Modularity Maximization for Community Detection 

## Overview

This project demonstrates a **simple educational implementation** of the **Greedy Modularity Maximization algorithm** for community detection in networks.
It follows the same principle as the **NetworkX built-in function** `greedy_modularity_communities()` but uses only **NetworkX** (no itertools or external libraries).

The algorithm detects **communities (clusters)** by maximizing the **modularity (Q)** of the graph — a measure of how well nodes are grouped based on edge density.

---

## What is Modularity?

Modularity quantifies how well a network is divided into communities.

**Formula:**

```
Q = (1 / (2m)) * Σ_ij [A_ij - (k_i * k_j) / (2m)] δ(c_i, c_j)
```

Where:

* `A_ij`: 1 if an edge exists between i and j, else 0
* `k_i, k_j`: degrees of nodes i and j
* `m`: total number of edges
* `δ(c_i, c_j)`: 1 if nodes i and j are in the same community

---

## ⚙️ ΔM Formula (Used for Merging)

To decide which communities to merge, we compute the **change in modularity (ΔM_AB)**:

```
ΔM_AB = (l_AB / L) - ((k_A * k_B) / (2 * L²))
```

Where:

* `l_AB`: number of edges between communities A and B
* `k_A`, `k_B`: sum of degrees of nodes in A and B
* `L`: total number of edges in the graph

---

## Algorithm Steps

1. **Initialization:** Each node starts as its own community.
2. **Merge Step:** For every pair of communities, compute ΔM_AB and merge the pair with the highest positive gain.
3. **Iteration:** Repeat until no merge improves modularity.
4. **Output:** Final set of communities with maximum modularity.

---

## Time Complexity Analysis

Let:

* **n** = number of nodes
* **m** = number of edges
* **c** = number of communities (initially n)

### Modularity Computation

Each ΔM computation iterates over node pairs in two communities → `O(n²)`.

### Merge Evaluation

Every iteration checks all community pairs → `O(c²)` merges.
Each merge recomputes ΔM → `O(n²)`.
Hence, total complexity ≈ **O(c² × n²)**.
Initially `c ≈ n`, so worst-case **O(n⁴)**, but practically **O(n³)** for sparse graphs.

### Space Complexity

| Component               | Space     |
| ----------------------- | --------- |
| Adjacency & degree maps | O(n + m)  |
| Community storage       | O(n)      |
| **Total**               | **O(n²)** |

---

