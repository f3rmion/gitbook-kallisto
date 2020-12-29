---
description: Count of covalent bonds for an atom in a molecule.
---

# Atomic Coordination Numbers

### Introduction

The concept of atomic coordination numbers \(CNs\) has been introduced by Grimme and co-workers. CNs represent hybridisation conditions for atoms inside a molecular environment that agrees quite well with chemical intuition. Within the `kallisto` program CNs are calculated in a pairwise sum that incorporates atomic covalent radii as introduced by Pyykkö. Furthermore, the differences in atomic electronegativities has been introduced for each pair as shown in its definition below with `k0 = 7.5`, `k1= 4.1`, `k2 = 19.1`, and `k3 = 254.6`

$$
CN_i = \sum\limits_i^N\sum\limits_{j \ne i} \frac{\delta_{AB}^{EN}}{2}\left( 1 + \text{erf}\left(-k_0\left(\frac{R_{AB}-R_{AB}^{cov}}{R_{AB}}\right)\right) \right)
\\
\text{where} \quad \delta_{AB}^{EN} = \left( k_1 \exp\left(|EN_A - EN_B| + k_2 \right)^2\right)/k_3
$$

Here, Pauling electronegativities \(`EN`\), the internuclear distance of pair AB \(`RAB`\), and covalent atomic radii \(`RcovAB = RcovA + RcovB`\). 

### Application

To calculate coordination numbers, we call the subcommand `cns` within `kallisto`

```bash
> kallisto --verbose cns --inp alanine-glycine.xyz
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

We obtain a list of atomic coordination numbers, which is in agreement with chemical intuition.

### Subcommand: cns

{% tabs %}
{% tab title="cns" %}
```bash
> kallisto --verbose cns options arguments
```
{% endtab %}

{% tab title="options" %}
```
--inp <string> 
(optional, default: coord)
description: 
 input file in xmol format (Ångström) or in Turbomole format (Bohr)
 
 --cntype <string>
(optional, default: cov)
available:
 cov (default), exp, erf
description:
 choose between different damping function definitions
```
{% endtab %}

{% tab title="arguments" %}
```
output : 
 standard output (or to specified file)
```
{% endtab %}
{% endtabs %}

