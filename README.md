# Greedy Modularity Maximization for Community Detection

## Overview
This project implements a **simplified version** of the **Greedy Modularity Maximization algorithm** for community detection in graphs.  
The algorithm identifies **communities (clusters)** in a network by **maximizing modularity**, which measures the strength of a community structure.

It produces results **similar to NetworkX’s built-in**
`greedy_modularity_communities()` function, but with a **simpler and more educational** approach.

---

## What is Community Detection?
Community detection aims to divide a graph into groups of nodes (communities) such that:
- There are **many edges within communities**, and  
- **Few edges between communities**.

The **modularity (Q)** of a partition measures how well the network is divided:

\[
Q = \frac{1}{2m} \sum_{i,j} [A_{ij} - \frac{k_i k_j}{2m}] \delta(c_i, c_j)
\]

where:  
- \(A_{ij}\): 1 if edge exists between i and j, else 0  
- \(k_i, k_j\): degrees of nodes i and j  
- \(m\): total number of edges  
- \(\delta(c_i, c_j)\): 1 if nodes i and j are in the same community  

---

## Algorithm Workflow

1. **Initialization:** Each node starts as its own community.  
2. **Iteration:** Compute modularity gain for all possible community merges and merge the pair with the highest increase.  
3. **Termination:** Stop when no merge increases modularity further.  
4. **Output:** Final community partition with maximum modularity.



---
