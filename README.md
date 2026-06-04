# Markov Chains & Stochastic Modeling

> M1 Informatique — Parcours Intelligence Artificielle · Université d'Avignon · 2024–2025

[![Python](https://img.shields.io/badge/Python-3.10+-blue?logo=python)](https://python.org)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange?logo=jupyter)](https://jupyter.org)
[![NumPy](https://img.shields.io/badge/NumPy-1.24+-013243?logo=numpy)](https://numpy.org)

---

## Overview

This project explores the theoretical and computational foundations of **discrete-time Markov chains** and their applications to stochastic simulation and web ranking. It covers random walks, stationary distribution computation via the Power Method, and the implementation of Google's PageRank algorithm.

---

## Table of Contents

- [Background](#background)
- [Project Structure](#project-structure)
- [Experiments & Results](#experiments--results)
  - [1. Bounded Random Walk Simulation](#1-bounded-random-walk-simulation)
  - [2. Stationary Distribution — Power Method](#2-stationary-distribution--power-method)
  - [3. PageRank Algorithm](#3-pagerank-algorithm)
- [Key Results](#key-results)
- [Installation](#installation)
- [Usage](#usage)
- [Author](#author)

---

## Background

A **Markov chain** is a stochastic process $(X_t)_{t \geq 0}$ on a finite state space $\mathcal{S}$ satisfying the Markov property:

$$P(X_{t+1} = j \mid X_0, \ldots, X_t) = P(X_{t+1} = j \mid X_t) = P_{ij}$$

This project investigates:
- **Ergodic theory**: long-run time averages converge to the stationary distribution
- **Cesàro mean convergence**: $\bar{x}(N) = \frac{1}{N}\sum_{k=0}^{N-1} x^{(k)} \to \pi$
- **Power iteration**: $x^{(k+1)} = x^{(k)} P$ converges to the left eigenvector $\pi$

---

## Project Structure

```
markov-chains-stochastic-modeling/
├── tp1.ipynb          # Main Jupyter notebook (all experiments)
├── t1.py              # Standalone Python script
├── TPsimu.pdf         # Original subject / problem statement
├── CM1.pdf – CM4.pdf  # Lecture notes (Markov chains theory)
└── README.md
```

---

## Experiments & Results

### 1. Bounded Random Walk Simulation

A particle moves on $\{-N, \ldots, M\}$ with reflecting barriers:
- Right with probability $p$, left with probability $1-p$
- Stays in place at boundaries

**Parameters explored:** $p = 0.6$, $N = M = 10$, up to 1000 steps.

The empirical time proportions converge to the theoretical stationary distribution, validating the ergodic theorem.

| Parameter | Value |
|-----------|-------|
| $p$ (right) | 0.6 |
| $N$ (left boundary) | 10 |
| $M$ (right boundary) | 10 |
| Steps | 1 000 |

### 2. Stationary Distribution — Power Method

The transition matrix $P$ is constructed explicitly for the bounded walk. The **Power Method** iteratively computes:

$$x^{(k+1)} = x^{(k)} P, \qquad \bar{x}(N) = \frac{1}{N+1}\sum_{k=0}^{N} x^{(k)}$$

Convergence is declared when $\|x^{(k+1)} - x^{(k)}\| < \varepsilon = 10^{-8}$.

**Result:** The Cesàro average $\bar{x}(N)$ converges smoothly to the analytical stationary distribution $\pi_i \propto (p/(1-p))^i$.

### 3. PageRank Algorithm

PageRank models web surfing as a Markov chain on $n$ pages. The **Google matrix** is:

$$A_\alpha = (1-\alpha) A + \alpha \, \mathbf{e} \cdot x_0^\top$$

where $\alpha = 0.15$ is the teleportation probability and $x_0$ is the initial "home" distribution.

**Test graph:** 8 nodes (7 pages + google.com as node 7)

| Rank | Node | PageRank Score |
|------|------|----------------|
| 1 | Node 7 (Google.com) | **0.2544** |
| 2 | Node 0 | 0.2163 |
| 3 | Node 5 | 0.1445 |
| 4 | Node 6 | 0.1228 |
| 5 | Node 4 | 0.0919 |
| 6 | Node 1 | 0.0919 |
| 7 | Node 2 | 0.0781 |
| 8 | Node 3 | 0.0000 |

Convergence in fewer than 100 iterations with $\varepsilon = 10^{-9}$.

---

## Key Results

| Experiment | Result |
|------------|--------|
| Random walk ergodicity | Empirical proportions → theoretical $\pi$ |
| Power Method convergence | $\varepsilon = 10^{-8}$ reached in ~50 iterations |
| PageRank top node | Node 7 with score **0.2544** |
| PageRank isolated node | Node 3 with score **0.0000** (no in-links) |

---

## Installation

```bash
git clone https://github.com/KELI-Kekeli-Christ/markov-chains-stochastic-modeling.git
cd markov-chains-stochastic-modeling
pip install numpy matplotlib jupyter
jupyter notebook tp1.ipynb
```

---

## Usage

Open `tp1.ipynb` in Jupyter and run cells sequentially. Each section is self-contained.

```python
# Example: simulate a bounded random walk
positions = simulate_random_walk(p=0.6, N=10, M=10, steps=1000)
```

---

## Author

**Christ Kekeli KELI**  
M1 Informatique — Intelligence Artificielle  
Université d'Avignon  
Encadrant : Yezekael HAYEL
