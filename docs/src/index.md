
# HighDimPDE.jl


**HighDimPDE.jl** is a Julia package to **solve Highly Dimensional non-linear, non-local PDEs** of the form

```math
\begin{aligned}
    (\partial_t u)(t,x) &= \int_{\Omega} f\big(t,x,{\bf x}, u(t,x),u(t,{\bf x}), ( \nabla_x u )(t,x ),( \nabla_x u )(t,{\bf x} ) \big) \, d{\bf x} \\
    & \quad + \big\langle \mu(t,x), ( \nabla_x u )( t,x ) \big\rangle + \tfrac{1}{2} \text{Trace} \big(\sigma(t,x) [ \sigma(t,x) ]^* ( \text{Hess}_x u)(t, x ) \big).
\end{aligned}
```

where $u \colon [0,T] \times \Omega \to \R$, $\Omega \subseteq \R^d$ is subject to initial and boundary conditions, and where $d$ is large.


**HighDimPDE.jl** implements solver algorithms that break down the curse of dimensionality, including

* the [Deep Splitting scheme](@ref deepsplitting)

* the [Multi-Level Picard iterations scheme](@ref mlp)

* the Deep BSDE scheme (@ref deepbsde).


To make the most out of **HighDimPDE.jl**, we advise to first have a look at the 

* [documentation on the Feynman Kac formula](@ref feynmankac),

as all solver algorithms heavily rely on it.

## Algorithm overview

------------------------------------------------------------
Features  |    `DeepSplitting`   | `MLP`     | `DeepBSDE` |
----------|:----------------------:|:------------:|:--------:
Time discretization free|  ❌ | ✅ |   ❌ |
Mesh-free       | ✅ |   ✅ |   ✅ |
Single point $x \in \R^d$ approximation| ✅  |  ✅ | ✅ |
$d$-dimensional cube $[a,b]^d$ approximation| ✅   | ❌ | ✔️ |
GPU | ✅ |  ❌ | ✅ |      
Gradient non-linearities  | ✔️|  ❌ | ✅ |

✔️ : might be supported in the future