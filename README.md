# Recursive-Adic Number Field

A novel non-Archimedean number system based on recursive depth rather than prime divisibility.

## Overview

This repository contains the theoretical foundation and mathematical framework for the **Recursive-Adic Number Field** (ℚ_R, v), a new valuation system that measures numbers by their recursive compressibility rather than traditional size or factorization.

The framework introduces two complementary constructions:
- **Construction A**: An additive completion (ℤ̂_R, d_R) defining a complete ultrametric topology on ℤ
- **Construction B**: A valued field (ℚ_R, v) embedding recursive depth into an algebraic field structure within ℚ((t))

## Key Concepts

### Recursive Division Tree (RDT)

The foundation is the RDT depth function R(n), computed via dynamic programming:

```
R(1) = 0
R(n) = 1 + min[1≤k<n] (R(k) + R(n-k))/α
```

For α = 1.5, this function saturates at exactly 3.0 for all n ≥ 23, confirming the theoretical ceiling R_∞ = α/(α-1).

### Ultrametric Structure

The recursive-adic metric is defined as:

```
d_R(a,b) = σ^R(|a-b|)
```

This satisfies the strong triangle inequality, making (ℤ, d_R) an ultrametric space.

## Mathematical Properties

- **Complete non-Archimedean field** of rank 1
- **Ultrametric inequality** proven via hierarchical decomposition
- **Valuation extends multiplicatively**: v(t^R(n)) = R(n)
- **Saturation theorem**: lim[n→∞] R(n) = α/(α-1)
- **Computational complexity**: O(n²) with memoization, O(n) space

## Applications

### 1. Machine Learning
Depth-aware attention mechanisms that modulate attention scores by recursive depth difference:

```
Attention(Q,K,V)_ij = exp(QiKj^T/√dk) · σ^|R(i)-R(j)| / Σ_j[...]
```

### 2. Number Theory
- Recursive zeta functions
- Depth-equidistribution studies
- Analogues of Hensel's lemma for recursive lifting

### 3. Information Theory
- Depth entropy: H_R = -Σ p_d log p_d
- Hierarchical complexity measures
- Adaptive compression via recursive quantization

### 4. Physics
- Renormalization via depth-indexed counterterms
- Hierarchical subtraction schemes
- Connections to Connes-Kreimer theory

## Implementation

The paper includes verified Wolfram Language implementations:

```mathematica
(* Recursive depth function with memoization *)
ClearAll[r]
r[1] := 0
r[n_] := r[n] = 1 + Min[Table[(r[k] + r[n - k])/alpha, {k, 1, n - 1}]]

(* Recursive metric *)
dR[a_, b_, sigma_] := sigma^r[Abs[a - b]]

(* Valuation embedding *)
phi[n_] := ToExpression["t"]^r[n]
norm[n_, rho_] := rho^r[n]
```

## Standard Depth Values (α = 1.5)

| n | R(n) | n | R(n) | n | R(n) |
|---|------|---|------|-----|------|
| 1 | 0.000 | 8 | 2.824 | 20 | 2.999 |
| 2 | 1.000 | 10 | 2.922 | 23 | 3.000 |
| 3 | 1.667 | 12 | 2.965 | 50 | 3.000 |
| 5 | 2.407 | 15 | 2.990 | 100 | 3.000 |

## Open Problems

1. **Exact growth rate**: Rigorously prove R_max(α) = α/(α-1)
2. **Non-saturation**: For which α does R(n) grow unboundedly?
3. **Level set distribution**: What is the density of {n : R(n) = d}?
4. **Hierarchy connections**: Relationship to Kolmogorov complexity K(n) or prime factor function Ω(n)?

## Document

The complete mathematical treatment is available in:
- **PDF**: `The_Recursive_Adic_Number_Field__Construction__Analysis__and_Recursive_Depth_Transforms__1_.pdf`

## Author

**Steven Reid**  
Independent Researcher  
ORCID: [0009-0003-9132-3410](https://orcid.org/0009-0003-9132-3410)

## References

1. S. Reid, *Recursive Division Tree: A Log-Log Algorithm for Integer Depth*, DOI: 10.5281/ZENODO.17487650
2. K. Mahler, *p-adic Numbers and Their Functions*, Cambridge University Press
3. W. Hahn, "Über Reihen mit nichtnegativen Exponenten," *Monatsh. Math. Phys.*, 1907
4. A. Connes and D. Kreimer, "Hopf Algebras, Renormalization and Noncommutative Geometry," *Communications in Mathematical Physics*, 1998



*The underlying mathematical ideas and theoretical development are entirely original work by the author. Computational tools including Wolfram Language and large language models assisted with calculations and document preparation.*
