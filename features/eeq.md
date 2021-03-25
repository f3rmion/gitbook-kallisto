---
description: Calculate atomic partial charges via Lagrangian constraints.
---

# Partial Charges

## Introduction

Classical electronegativity equilibration \(EEQ\) partial charges are determined by minimising the following energy expression of the isotropic electrostatic interaction, which is dependent on atomic charges _q_

$$
E_{IES} = \sum\limits_{i=1}^N\left( \chi_iq_i + \frac{1}{2}\left(J_{ii} + \frac{2\gamma_{ii}}{\sqrt{\pi}}\right)q_i^2\right) + \frac{1}{2}\sum\limits_{i=1}^N\sum\limits_{j\ne i}^Nq_iq_j\frac{\text{erf}(\gamma_{ij}R_{ij})}{R_{ij}} \\[1em]\quad \text{with}\quad \chi_i = EN_i - \kappa_i\sqrt{CN_i}.
$$

The first part of the equation above describes the on-side interaction of atom `i` in terms of a Taylor expansion expressed in atomic partial charges. Within `chii` , we apply the Pauling electronegativity \(`EN`\) and the atomic coordination number \(`CN`\) scaled by a parameter `kappai`to introduce an environment dependency into the partial-charge approach.The second part of the equation describes the \(pairwise\) interactions between the atom `i` and all `j`particles as obtained for interacting charge densities \(for a deeper understanding check the references, [Goedecker et al.](https://doi.org/10.1103/PhysRevB.92.045131) and [Caldeweyher et al.](https://doi.org/10.26434/chemrxiv.7430216.v2); **Note**: Eq. 12 in [Caldeweyher et al.](https://doi.org/10.26434/chemrxiv.7430216.v2) is _erroneous_ while the definition above is correct as it is also given in the [JCP publication](https://doi.org/10.1063/1.5090222)\).

To obtain EEQ partial charges under the constraint that the partial charges conserve the total charge of the system, the method of constrained [Lagrangian optimisation](https://en.wikipedia.org/wiki/Lagrange_multiplier) is used

$$
\mathcal{L} = E_{IES} + \lambda\left(\sum\limits_{k=1}^Nq_k - q_{total}\right) \\ \quad \text{with}\quad \frac{\partial\mathcal{L}}{\partial q} = \mathbf{0} \quad\text{and} \quad \frac{\partial\mathcal{L}}{\partial \lambda}= \sum\limits_{k=1}^N q_k-q_{total} =0,
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
\end{pmatrix} \\[1em] \quad \text{with}\quad \mathcal{X}_i = -\chi_i
$$

Let's define the interaction matrix \(the definition of the right-hand side is given [above](eeq.md#introduction)\)

$$
\mathcal{A}_{ij} =     \begin{cases}
            J_{ii} + \frac{2\gamma_{ii}}{\sqrt{\pi}}, &         \text{if } i=j\\
            \frac{\text{erf}(\gamma_{ij}R_{ij})}{R_{ij}}, &         \text{if } i\neq j 
    \end{cases},
$$

and apply the Pauling electronegativity \(`EN`\) and the atomic coordination number \(`CN`\) to introduce an environment dependency into the partial-charge approach. Overall five parameter exist per element: `Jii`, `gammaii`, `ENi`, `Rcovi`, and `kappai`.

| Parameter | Meaning for atom i |
| :--- | :--- |
| `Jii` | [Chemical Hardness](https://doi.org/10.1021/j100023a006) |
| `gammaii` | Atomic radii dependent term |
| `ENi` | [Pauling electronegativity](https://en.wikipedia.org/wiki/Electronegativity#Pauling_electronegativity) |
| `Rcovi` | [Covalent atomic radius](https://doi.org/10.1002/chem.200800987) |
| `Kappai` | Scaling factor for `chii` |

## Define the Subcommand

{% tabs %}
{% tab title="eeq" %}
```bash
> kallisto eeq options arguments
```
{% endtab %}

{% tab title="options" %}
```markup
--inp <string> 
(optional, default: coord)
description: 
 input file in xmol format (Ångström) or in Turbomole format (Bohr)

--chrg <int>
(optional, default: 0)
description:
 absolute charge (qtotal) of the input structure (Lagrangian constraint)
```
{% endtab %}

{% tab title="arguments" %}
```text
output: 
 standard output or specified file
```
{% endtab %}
{% endtabs %}

## Application

To calculate atomic EEQ charges for a neutral charged Alanine-Glycine molecule, we call the subcommand `eeq`

```bash
> kallisto eeq --inp alanine-glycine.xyz
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
# Save output to file 'eeq'
> kallisto eeq --inp alanine-glycine.xyz eeq
> cat eeq
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

Now we obtain a list of atomic EEQ charges, which sum up to a total charge of zero. However, we can furthermore calculate atomic EEQ charges for the cationic \(or anionic\) Alanine-Glycine molecule by incorporating the `chrg` option as described in the subcommand definition.

