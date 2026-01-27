We want to solve the PDE-constrained shape optimization problem

$$
\min_{\Omega \subset \mathsf{D}} J(u)
:= \int_\Omega |u_\Omega - u_{ref}|^2 \, dx
$$

subject to $(\Omega,u_\Omega)$ satisfying

$$
\int_\Omega \nabla u_\Omega \cdot \nabla v + u_\Omega v \, dx
=
\int_\Omega f v \, dx
\quad \text{for all } v \in H_0^1(\Omega),
$$

where $\Omega \subset \mathbb{R}^2$ and
$u_d, f \in H^2(D)$ and $\Omega$ belongs to

$$
\mathcal{A}(D) \{\Omega \subset D: \Omega \;\text{is measurable and smooth} \}
$$

## Exercise 4

Use the direct method to compute the derivative 

$$
DJ(\Omega)(X) = \lim _{t \downarrow 0} \frac{J(\Omega_t) - J(\Omega)}{t}
$$

---

Considering the perturbed state equation

$$
\int_{\Omega_t} \nabla u_{\Omega_t} \cdot \nabla \varphi
+ u_{\Omega_t}\,\varphi
=
\int_{\Omega_t} f \varphi
\qquad \forall \varphi \in H^1_0(\Omega_t),
$$

a change of variables with $T_t(x) = y$ yields

$$
\int_\Omega A(t)\nabla u_t \cdot \nabla \varphi_t
+ \int_\Omega \xi(t)u_t \varphi_t
=
\int_\Omega \xi(t) f_t \varphi_t.
$$

Here,

$$
\begin{aligned}
A(t) &= \det(\partial T_t)\,\partial T_t^{-\top}, \\
\xi(t) &= \det(\partial T_t), \\
u_t &= u_{\Omega_t} \circ T_t, \\
\varphi_t &= \varphi \circ T_t, \\
f_t &= f \circ T_t.
\end{aligned}
$$

Using the identity

$$
\nabla v \circ T_t = \partial T_t^{-\top}\nabla (v \circ T_t),
$$

and replacing the test functions accordingly, we obtain

$$
\int_\Omega A(t)\nabla u_t \cdot \nabla \psi
+ \int_\Omega \xi(t)u_t \psi
=
\int_\Omega \xi(t) f_t \psi
\qquad \forall \psi \in H^1_0(\Omega).
$$


Differentiating with respect to $t$ and evaluating at $t=0$ yields

$$
\int_\Omega A'(0)\nabla u \cdot \nabla \psi
+ \int_\Omega \nabla \dot{u} \cdot \nabla \psi
+ \int_\Omega \operatorname{div}(X) u \psi
+ \int_\Omega \dot{u}\,\psi
=
\int_\Omega \operatorname{div}(X)f\psi
+ \int_\Omega \nabla f \cdot X\,\psi.
$$

With

$$
A'(0) = \operatorname{div}(X)\,I - \partial X - \partial X^\top,
$$

we obtain

$$
\begin{aligned}
\int_\Omega \nabla \dot{u} \cdot \nabla \psi
+ \int_\Omega \dot{u}\,\psi
&=
- \int_\Omega \operatorname{div}(X) u \psi \\
&\quad
- \int_\Omega
\bigl(\operatorname{div}(X)I - \partial X - \partial X^\top\bigr)
\nabla u \cdot \nabla \psi \\
&\quad
+ \int_\Omega (\nabla f \cdot X)\,\psi \\
&\quad + \int_\Omega \operatorname{div}(X)f\psi.
\end{aligned}
\tag{1}
$$

Here, $\dot{u}$ denotes the **material derivative** of $u$.  
Following the approach of Lemma 4.217 (adapted to our setting), we obtain convergence
$$
\dot{u} \in H^1_0(\Omega).
$$

### Shape derivative of cost functional

We differentiate $t \mapsto J(\Omega_t)$:

$$
\begin{aligned}
dJ(\Omega)(X)
&= \left.\frac{d}{dt} J(\Omega_t)\right|_{t=0} \\
&= \left.\frac{d}{dt} \int_\Omega
\det(\partial T_t)\,(u_t - u_{\mathrm{ref}})^2 \right|_{t=0} \\
&= \int_\Omega \operatorname{div}(X) (u - u_{\mathrm{ref}})^2
+ 2 \int_\Omega \dot{u}(u - u_{\mathrm{ref}}) \\
&\quad
- 2 \int_\Omega (u - u_{\mathrm{ref}})
\nabla u_{\mathrm{ref}} \cdot X.
\end{aligned}
\tag{2}
$$

### The adjoint equation

To eliminate the explicit occurrence of the material derivative $\dot{u}$,
we introduce the Lagrangian

$$
\mathcal{L} :
\mathbb{R} \times H^1_0(\Omega) \times H^1_0(\Omega)
\rightarrow \mathbb{R},
$$

defined by

$$
\mathcal{L}(t,u,p)
=
\int_\Omega A(t)\nabla u \cdot \nabla p
+ \int_\Omega \xi(t) u p
- \int_\Omega \xi(t)f_t p
+ \int_\Omega \xi(t)(u - u_{\mathrm{ref},t})^2.
$$

The formal Lagrangian approach (see Tröltzsch) suggests that the adjoint
$p$ satisfies

$$
\partial_u \mathcal{L}(0,u,p)(\psi) = 0
\qquad \forall \psi \in H^1_0(\Omega).
$$

Computing the derivative yields

$$
\partial_u \mathcal{L}(0,u,p)(\psi)
=
\int_\Omega \nabla \psi \cdot \nabla p
+ \int_\Omega \psi p
+ 2 \int_\Omega (u - u_{\mathrm{ref}})\psi.
$$


### Adjoint problem

We define the adjoint solution $p \in H^1_0(\Omega)$ by

$$
\int_\Omega \nabla \psi \cdot \nabla p
+ \int_\Omega \psi p
=
-2 \int_\Omega (u - u_{\mathrm{ref}})\psi
\qquad \forall \psi \in H^1_0(\Omega).
\tag{3}
$$

Choosing $\psi = \dot{u}$ in (3) gives

$$
\int_\Omega \nabla \dot{u} \cdot \nabla p
+ \int_\Omega \dot{u} p
=
-2 \int_\Omega (u - u_{\mathrm{ref}})\dot{u}.
$$

On the other hand, choosing $\psi = p$ in (1) yields

$$
\begin{aligned}
\int_\Omega \nabla \dot{u} \cdot \nabla p
+ \int_\Omega \dot{u} p
&=
- \int_\Omega \operatorname{div}(X) u p \\
&\quad
- \int_\Omega
\bigl(\operatorname{div}(X)I - \partial X - \partial X^\top\bigr)
\nabla u \cdot \nabla p \\
&\quad
+ \int_\Omega (\nabla f \cdot X)\,p.
\end{aligned}
$$

Combining both identities yields

$$
\begin{aligned}
2 \int_\Omega (u - u_{\mathrm{ref}})\dot{u}
&=
\int_\Omega \operatorname{div}(X) u p \\
&\quad
+ \int_\Omega
\bigl(\operatorname{div}(X)I - \partial X - \partial X^\top\bigr)
\nabla u \cdot \nabla p \\
&\quad
- \int_\Omega (\nabla f \cdot X)\,p \\
& \quad
- \int_\Omega \operatorname{div}(X)f p
\end{aligned}
\tag{4}
$$

### Final expression for the shape derivative

Inserting (4) into (2) yields

$$
\begin{aligned}
DJ(\Omega)(X)
&=
\int_\Omega \operatorname{div}(X) (u - u_{\mathrm{ref}})^2
- 2 \int_\Omega (u - u_{\mathrm{ref}})
\nabla u_{\mathrm{ref}} \cdot X \\
&\quad
+ \int_\Omega \operatorname{div}(X) u p \\
&\quad
+ \int_\Omega
\bigl(\operatorname{div}(X)I - \partial X - \partial X^\top\bigr)
\nabla u \cdot \nabla p \\
&\quad
- \int_\Omega (\nabla f \cdot X)\,p\\
& \quad
- \int_\Omega \operatorname{div}(X)fp .
\end{aligned}
$$

## Exercise 5.

Use the average adjoint method to compute the derivate

$$
DJ(\Omega)(X) = \lim _{t \downarrow 0} \frac{J(\Omega_t) - J(\Omega)}{t}
$$


Considering the parametrised Lagrangian

$$
\mathcal{L}(t, u, p) = \int _\Omega A(t) \nabla u \cdot \nabla v + \int _\Omega \xi(t) u v - \int _\Omega \xi(t) f_t v + \int _ \Omega \xi(t) (u- u_{\mathrm{ref}, t})^2 
$$

we define the $\emph{average adjoint} p^t \in H^1_0(\Omega)$ as the solution to

$$
\int_0^1 \partial _u \mathcal{L}(t, s u_t, (1-s)u_0, p^t)(v) ds = 0 \quad \forall v \in H^1_0(\Omega)
$$
Thanks to Lemma 3.63 we now that

$$
\mathcal{L}(t, u_t, 0) = \mathcal{L}(t, u_0, p^t) \quad \text{for t sufficiently small}
$$

Therefore we have 

$$
DJ(\Omega)(X) = \lim _ {t \downarrow 0} \frac{J(T_t^X(\Omega)) - J(\Omega)}{t} = \lim _{t \downarrow 0} \frac{\mathcal{L}(t, u_0, p^t) - \mathcal{L}(0, u_0, p^t)}{t} 
$$

Since 

$$
\begin{aligned}
\frac{\mathcal{L}(t, u_0, p^t) - \mathcal{L}(0, u_0, p^t)}{t} &= \int _\Omega \frac{A(t) - \operatorname{I}}{t} \nabla u_0 \cdot \nabla p^t \\
                                                    &+ \int _\Omega \frac{\xi(t)- 1}{t} u_0 p^t \\
                                                    &- \int _\Omega \frac{\xi(t)f_t-f_0}{t} p^t \\
                                                    &- \int _\Omega \xi(t) \frac{(u_0- u_{\mathcal{ref}, t})^2}{t} - \frac{(u_0 - u_{\mathcal{ref}})}{t}
                                        
\end{aligned}
$$

It holds that

$$
\begin{aligned}
DJ(\Omega)(X) &= \int _\Omega A'(0) \nabla u_0 \cdot \nabla p ^0 \\
                & + \int _\Omega \xi'(t) u_0 p^0 - \\
                & - \int _\Omega \nabla f \cdot X p ^0\\
                & - \int _\Omega \operatorname{div}(X) f p^0 \\
                & + \int _\Omega \frac{d}{dt}(\xi(t)*(u_0-u_{\mathrm{ref,t}})) \bigg |_{t=0}


\end{aligned}
$$

which is equivalent to 

$$
\begin{aligned}
DJ(\Omega)(X)
&=
\int_\Omega \operatorname{div}(X) (u - u_{\mathrm{ref}})^2
- 2 \int_\Omega (u - u_{\mathrm{ref}})
\nabla u_{\mathrm{ref}} \cdot X \\
&\quad
+ \int_\Omega \operatorname{div}(X) u p \\
&\quad
+ \int_\Omega
\bigl(\operatorname{div}(X)I - \partial X - \partial X^\top\bigr)
\nabla u \cdot \nabla p \\
&\quad
- \int_\Omega (\nabla f \cdot X)\,p\\
& \quad
- \int_\Omega \operatorname{div}(X)fp .
\end{aligned}
$$

with $p^0 = p, u_0 = u$.


