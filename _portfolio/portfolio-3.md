---
title: "Portfolio item number 3"
excerpt: "Short description of portfolio item number 3<br/><img src='/images/Monotone.png'>"
collection: portfolio
---

<br/><img src='/images/Monotone.png'>"

This work describes the implementation of strong stability preserving time integration techniques in the stochastic context. 

We shall describe the main principle below in a very simplified setting:

_______
Suppose you are wishing to solve the following SPDE numerically
$$
d u + u_x dW = 0,\quad u(0,x) = u_0(x), 
$$
The solution is
$$
u(x,t) = u_0(x-W(t)),
$$ 
and remains bounded in both $$|u|_{BV}$$, $$|u|_{L^{\infty}}$$. We describe the proceedure to make the forward Euler scheme monotone.  

___
### Approach 1
___

In order to make the scheme capable of handling negative increments we shall define a new scheme, itself dependent on the particular realisation of the increment, consider the new adaptive scheme:
$$
u^{n+1}_i = u^n_i - \frac{(\Delta W^n)^+}{\Delta x} (u_{i}-u_{i-1}) - \frac{(\Delta W^n)^-}{\Delta x} (u_{i}-u_{i+1})  = 0
$$

where $$(c)^{+}$$, $$(c)^{-}$$ denote the positive or negative component of the input. Therefore, $u^{n+1}_i$ is either a convex combination of $$u^{n}_{i-1},u^{n}_{i}$$ or $$u^{n}_{i},u^{n}_{i+1}$$ giving the following principle:
$$u^{n+1}_{i} 
\in [\min \lbrace u^{n}_{i-1},u^{n}_{i},u^{n}_{i+1}\rbrace,\max\lbrace u^{n}_{i-1},u^{n}_{i},u^{n}_{i+1}\rbrace],$$
for all possible increments when
$$\left(1-\frac{\sqrt{\Delta t}A_{\Delta t}}{\Delta x}\right)\geq 0
$$. 
This is true when the following CFL condition is satisfied.
$$
\sqrt{\Delta t} A_{\Delta t} \leq \Delta x
$$
If one uses a 2-point random variable taking values $1$ or $-1$ with equal probability $0.5$, the timestep restriction is 
$$
\Delta t \leq \frac{\Delta x^2}.
$$
_______

