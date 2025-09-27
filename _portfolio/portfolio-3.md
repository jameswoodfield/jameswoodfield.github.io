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
d u + a u_x dW = 0,\quad u(0,x) = u_0(x), \quad a>0
$$
The solution is
$$
u(x,t) = u_0(x-aW(t)),
$$ 
and remains bounded in both $$|u|_{BV}$$, $$|u|_{L^{\infty}}$$. We describe the proceedure to make the forward Euler scheme monotone.  

___
### Approach 1
___

After a discretisation in space, using the first order upwind method one attains the following system
$$
d u_i +  \frac{a}{\Delta x} (u_{i}-u_{i-1}) dW = 0.
$$
<!-- this can be described as follows 
$$
d_t 
\begin{bmatrix}
u_0\\
u_1\\
\vdots\\
u_n 
\end{bmatrix}
+ 
\underbrace{\begin{bmatrix}
&1&0,&0&0&...&-1\\
&-1&1&0&0&...&0\\
&\vdots&\vdots&\vdots&\vdots &\ddots&0\\
&0&0&0&0&...-1&1\\
\end{bmatrix}}_{g}
\begin{bmatrix}
u_0\\
u_1\\
\vdots\\
u_n 
\end{bmatrix}
dW = 0 
$$
and considered a SDE after the method of lines. -->

If one were to discretise by the Euler-Maruyama scheme one would get
$$
u^{n+1}_i = u^n_i - \frac{a\Delta W^n}{\Delta x} (u_{i}-u_{i-1}) = 0
$$
This is discrete maximum principle satisfying iff 
$$(1-\frac{a\Delta W^n}{\Delta x})
\leq 1$$
$$\frac{a\Delta W^n}{\Delta x}
\geq 0$$
requiring the boundedness and positivity of $\Delta W^n$, a condition not satisfied if $\Delta W^n\sim N(0,1)$. 


In order to make the scheme capable of handling negative increments we shall define a new scheme, itself dependent on the particular realisation of the increment, consider the new adaptive scheme:
$$
u^{n+1}_i = u^n_i - \frac{a(\Delta W^n)^+}{\Delta x} (u_{i}-u_{i-1}) - \frac{a(\Delta W^n)^-}{\Delta x} (u_{i}-u_{i+1})  = 0
$$

where $$(c)^{+} = c + |c|$$, $$(c)^{-} = c-|c|$$ denote the positive or negative component of the input. 

Here, if $$\Delta W^n \in\sqrt{\Delta t}[0,A_{\Delta t}]$$,  we recover the scheme
$$
u^{n+1}_i = u^n_i - \frac{a(\Delta W^n)^+}{\Delta x} (u_{i}-u_{i-1})  
$$
$$
u^{n+1}_i = \left(1- \frac{a(\Delta W^n)^+}{\Delta x}\right) u^n_i  + \frac{a(\Delta W^n)^+}{\Delta x}u_{i-1}
$$
if 
$$\Delta W^n \in
\sqrt{\Delta t}[-A_{\Delta t},0]$$,  we recover the scheme
$$
u^{n+1}_i = u^n_i - \frac{a(\Delta W^n)^-}{\Delta x} (u_{i}-u_{i+1})
$$
$$
u^{n+1}_i = \left( 1-\frac{a(\Delta W^n)^-}{\Delta x}\right) u^n_i +\frac{a(\Delta W^n)^-}{\Delta x} u_{i+1}
$$
Therefore, $u^{n+1}_i$ is either a convex combination of $$u^{n}_{i-1},u^{n}_{i}$$ or $$u^{n}_{i},u^{n}_{i+1}$$ giving the following principle:
$$u^{n+1}_{i} 
\in [\min \lbrace u^{n}_{i-1},u^{n}_{i},u^{n}_{i+1}\rbrace,\max\lbrace u^{n}_{i-1},u^{n}_{i},u^{n}_{i+1}\rbrace],$$
for all possible increments when
$$\left(1-\frac{a\sqrt{\Delta t}A_{\Delta t}}{\Delta x}\right)\geq 0
$$. 
This is true when the following CFL condition is satisfied.
$$
\sqrt{\Delta t} A_{\Delta t} \leq \frac{\Delta x}{a}$$
i.e. one scales the timestep in accordance with the mesh spacing. 


If one uses a 2-point random variable $\Delta W\in \sqrt{\Delta t}[-1/2,1/2]$, with equal probability $A_{\Delta t} \leq 1/2$, the timestep restriction is 
$$
\Delta t \leq 4\frac{\Delta x^2}{a^2}
$$

If one uses bounded in Milstein and Tretkyov one has the following bound
$A_{\Delta t}:=\sqrt{2 k|\ln {\Delta t}|}, k \geq 1$, and the timestep restriction
$\Delta t|\ln {\Delta t}|\leq \Delta x^2/a^2$, holds in two regimes for all $\Delta x$.   


_______

