---
description: Calculate atomic partial charges via Lagrangian constraints.
---

# Electronegativity Equilibration



### Introduction

Classical electronegativity equilibration \(EEQ\) partial charges are determined by minimising the following energy expression, which is dependent on atomic charges _q_

$$
E_{IES} = \sum\limits_{i=1}^N\left( \chi_iq_i + \frac{1}{2}\left(J_{ii} + \frac{2\gamma_{ii}}{\sqrt{\pi}}\right)q_i^2\right) + \frac{1}{2}\sum\limits_{i=1}^N\sum\limits_{j\ne i}^Nq_iq_j\frac{\text{erf}(\gamma_{ij}R_{ij})}{R_{ij}}.
$$

To obtain EEQ partial charges, under the constraint that the partial charges conserve the total charge of the system, the method of constrained Lagrangian optimisation is used

$$
\mathcal{L} = E_{IES} + \lambda\left(\sum\limits_{k=1}^Nq_k - q_{total}\right) \quad \text{with}\quad \frac{\partial\mathcal{L}}{\partial q} = \mathbf{0} \quad\text{and} \quad \frac{\partial\mathcal{L}}{\partial \lambda}= \sum\limits_{k=1}^N q_k-q_{total} =0,
$$

which leads to a set of \(N + 1\) linear equations that can be rewritten in matrix form as

$$
\begin{pmatrix}
\mathcal{A} & \mathbf{1}\\
\mathbf{1} & \mathbf{0}
\end{pmatrix}
\begin{pmatrix}
\mathbf{q} \\
\mathbf{\lambda} 
\end{pmatrix} =
\begin{pmatrix}
\mathcal{X} \\
q_{total} 
\end{pmatrix}.
$$

We define the interaction matrix and the right-hand side as

$$
\mathcal{A}_{ij} =     \begin{cases}
            J_{ii} + \frac{\sqrt{2}\gamma_{ii}}{\sqrt{\pi}}, &         \text{if } i=j,\\
            \frac{\text{erf}(\gamma_{ij}R_{ij})}{R_{ij}}, &         \text{if } i\neq j 
    \end{cases}
\quad \text{and}\quad \mathcal{X} = EN_i - \kappa_i\sqrt{CN_i},
$$

and apply the Pauling electronegativity \(`EN`\) and the atomic coordination number \(`CN`\) to introduce an environment dependency into the approach.

