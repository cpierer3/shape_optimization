# NGSolve Shape Optimization

Welcome to the **NGSolve Shape Optimization** project. This Jupyter Book demonstrates PDE-constrained shape optimization using the NGSolve finite element library.

## Project Overview

This project implements shape optimization problems of the form:

$$
\min_{\Omega \subset \mathsf{D}} J(u)
:= \int_\Omega |\nabla u_\Omega - \nabla u_{ref}|^2 \, dx
$$

subject to the PDE constraint:

$$
\int_\Omega \nabla u_\Omega \cdot \nabla v + u_\Omega v \, dx
=
\int_\Omega f v \, dx
\quad \text{for all } v \in H_0^1(\Omega)
$$



## Contents

This book contains:
- Main optimization implementation in ngsolve/netgen
- Mathematical derivations
- Numerical experiments
