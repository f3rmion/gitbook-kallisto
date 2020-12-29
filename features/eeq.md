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

### Simple Example

As usual we invoke `kallisto` via the command line. Please note that you need a valid molecular structure either in an `xmol` format \(\*.xyz in Ångström\) or in the `Turbomole` format \(coord in Bohr\). We exemplify the calculation of atomic partial charges for the alanine-glycine molecule.

```text
> cat alanine-glycine.xyz
  20

C     2.081440     0.615100    -0.508430
C     2.742230     1.824030    -1.200820
N     4.117790     1.799870    -1.190410
C     4.943570     2.827040    -1.822060
C     6.440080     2.569360    -1.637600
O     7.351600     3.252270    -2.069090
N     0.610100     0.695090    -0.538780
O     2.095560     2.724940    -1.739670
O     6.705220     1.463410    -0.897460
H     0.303080     1.426060     0.103770
H     0.338420     1.050680    -1.460480
C     2.488753    -0.593400    -1.198448
H     2.416500     0.557400     0.532050
H     4.614100     1.081980    -0.670550
H     4.699850     3.794460    -1.373720
H     4.722890     2.844690    -2.894180
H     7.687400     1.448620    -0.860340
H     2.029201    -1.457008    -0.719999
H     2.170233    -0.542411    -2.238576
H     3.572730    -0.688405    -1.154998
```

To calculate coordination numbers, we call the subcommand `eeq` within `kallisto`

```text
> kallisto --verbose eeq --inp alanine-glycine.xyz
0.059704461728256275
0.2626494653657499
-0.4965512448739412
0.047991263003576215
0.2744196871227069
-0.38881537388038867
-0.6402141334784498
-0.3928319273751289
-0.47582669447302023
0.2790624116759344
0.2891096702066603
-0.1845935570451514
0.12417598515268524
0.27028773655342087
0.14722120980685544
0.14502596136754614
0.2992214711225029
0.13031907222773667
0.1342346682463232
0.11540986754612566
```

We obtain a list of atomic EEQ charges ordered according to the input.

