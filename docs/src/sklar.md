```@meta
CurrentModule = Copulas
```

# Sklar's Theorem

Recall the following theorem from [sklar1959](@cite): 

> **Theorem (Sklar):** For every random vector $\bm X$, there exists a copula $C$ such that 
>
> $\forall \bm x\in \mathbb R^d, F(\bm x) = C(F_{1}(x_{1}),...,F_{d}(x_{d})).$
> The copula $C$ is uniquely determined on $\mathrm{Ran}(F_{1}) \times ... \times \mathrm{Ran}(F_{d})$, where $\mathrm{Ran}(F_i)$ denotes the range of the function $F_i$. In particular, if all marginals are absolutely continuous, $C$ is unique.


The implementation we have of this theorem allows building multivariate distributions by specifying separately their marginals and dependence structures as follows:


```julia
using Copulas, Distributions, Random
X₁ = Gamma(2,3)
X₂ = Pareto()
X₃ = LogNormal(0,1)
C = ClaytonCopula(3,0.7) # A 3-variate Clayton Copula with θ = 0.7
D = SklarDist(C,(X₁,X₂,X₃)) # The final distribution
```

From this construction, the object `D` is a genuine multivariate random vector following `Distributions.jl`'s API, and can be sampled (`rand()`), can have its probability density function and its distribution function evaluated (respectively `pdf` and `cdf`), etc.


```@docs
SklarDist
```

```@bibliography
Pages = ["sklar.md"]
Canonical = false
```