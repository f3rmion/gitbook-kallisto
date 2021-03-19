---
description: Count of covalent bonds for an atom in a molecule.
---

# Coordination Numbers

### Introduction

The concept of atomic coordination numbers \(CNs\) has been introduced by [Grimme and co-workers](https://doi.org/10.1063/1.3382344). CNs represent hybridisation conditions for atoms inside a molecular environment that agrees quite well with chemical intuition. Within the `kallisto` program CNs are calculated in a pairwise sum that incorporates atomic covalent radii as [introduced by Pyykkö](https://doi.org/10.1002/chem.200800987). Furthermore, the differences in atomic electronegativities have been introduced for each pair as shown in its definition below.

$$
CN_i = \sum\limits_i^N\sum\limits_{j \ne i} \frac{\delta_{AB}^{EN}}{2}\left( 1 + \text{erf}\left(-k_0\left(\frac{R_{AB}-R_{AB}^{cov}}{R_{AB}}\right)\right) \right)
\\
\text{where} \quad \delta_{AB}^{EN} = \left( k_1 \exp\left(|EN_A - EN_B| + k_2 \right)^2\right)/k_3
$$



The parameters used within the above definition are as follows:

| Parameter | Value |
| :--- | :--- |
| `k1` | 4.1 |
| `k2` | 19.1 |
| `k3` | 254.6 |
| `k4` | 254.6 |

Those parameters have been obtained by a least-squared fit to Wiberg bond orders of different di-atomic molecules. Here, Pauling electronegativities \(`EN`\), the internuclear distance of pair AB \(`RAB`\), and covalent atomic radii \(`RcovAB = RcovA + RcovB`\) are used. 

### Define the Subcommands

{% tabs %}
{% tab title="cns" %}
```bash
> kallisto cns options arguments
```
{% endtab %}

{% tab title="options" %}
```markup
--inp <string> 
(optional, default: coord)
description: 
 input file in xmol format (Ångström) or in Turbomole format (Bohr)
 
 --cntype <string>
(optional, default: cov)
available:
 cov, exp, erf
description:
 different CN definitions
```
{% endtab %}

{% tab title="arguments" %}
```
output: 
 standard output or specified fil
```
{% endtab %}
{% endtabs %}

### Applications

To calculate coordination numbers, I call the subcommand `cns` 

```bash
> kallisto cns --inp alanine-glycine.xyz
3.98207181
3.00785834 
2.99800682 
3.98095768 
2.993322   
1.00025168
2.99979217 
1.00140949 
1.98927904 
0.99678598 
0.9964672  
4.0016192
0.9932187  
0.99711911 
0.99333844 
0.99320143 
0.99209619 
0.99397073
0.99397068 
0.99397075
# Save output to file 'cns'
> kallisto cns --inp alanine-glycine.xyz cns
> cat cns
3.98207181
3.00785834 
2.99800682 
3.98095768 
2.993322   
1.00025168
2.99979217 
1.00140949 
1.98927904 
0.99678598 
0.9964672  
4.0016192
0.9932187  
0.99711911 
0.99333844 
0.99320143 
0.99209619 
0.99397073
0.99397068 
0.99397075
```

Now we obtain a list of atomic coordination numbers, which is in agreement with chemical intuition. 

