---
title: "Portfolio item number 2"
excerpt: "Short description of portfolio item number 2<br/><img src='/images/local_maximum_principle.png'>"
collection: portfolio
---
Quadrature points contributing to numerical fluxes can be limited based on face defined maximum principles, and the resulting cell mean at the next timestep can satisfy a cell mean maximum principle. 

The main distinction from the literature is that the flux contributing quadrature points at a face must satisfy two local boundedness principles when the requirements of theorem 2.1 are viewed from the perspective of cells K,L respectively. This has
important consequences on the design of multidimensional limiter functions. It implies that both $p_L(x_q)$, $p_K(x_q)$ could be limited based on the same but extended face defined maximum principle. 