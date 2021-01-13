---
description: Count of covalent bonds for an atom in a molecule.
---

# Atomic Coordination Numbers and Spheres

### Introduction

The concept of atomic coordination numbers \(CNs\) has been introduced by Grimme and co-workers. CNs represent hybridisation conditions for atoms inside a molecular environment that agrees quite well with chemical intuition. Within the `kallisto` program CNs are calculated in a pairwise sum that incorporates atomic covalent radii as introduced by Pyykkö. Furthermore, the differences in atomic electronegativities has been introduced for each pair as shown in its definition below with `k0 = 7.5`, `k1= 4.1`, `k2 = 19.1`, and `k3 = 254.6`

$$
CN_i = \sum\limits_i^N\sum\limits_{j \ne i} \frac{\delta_{AB}^{EN}}{2}\left( 1 + \text{erf}\left(-k_0\left(\frac{R_{AB}-R_{AB}^{cov}}{R_{AB}}\right)\right) \right)
\\
\text{where} \quad \delta_{AB}^{EN} = \left( k_1 \exp\left(|EN_A - EN_B| + k_2 \right)^2\right)/k_3
$$

Here, Pauling electronegativities \(`EN`\), the internuclear distance of pair AB \(`RAB`\), and covalent atomic radii \(`RcovAB = RcovA + RcovB`\) are used. Coordination number spheres are easily calculated by increasing the covalent atomic radii within the CN definition.

$$
CNSP_{i}^{(3,2)} = CN_{i}\left(R^{cov'}_{AB} = 3\times R^{cov}_{AB}\right) - CN_{i}\left(R^{cov'}_{AB} = 2\times R^{cov}_{AB}\right)
$$

This atomic feature is useful to determine the steric hindrance from neighbouring groups. The depiction below exemplifies this for the toluene molecule \(see Applications part\).

### Define the Subcommands

{% tabs %}
{% tab title="cns" %}
```bash
> kallisto --verbose cns options arguments
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
 standard output or specified file
```
{% endtab %}
{% endtabs %}

### Application

To calculate coordination numbers, I call the subcommand `cns` 

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
# Save output to file 'cns'
> kallisto --verbose cns --inp alanine-glycine.xyz cns
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

Now I obtain a list of atomic coordination numbers, which is in agreement with chemical intuition. 

Let's calculate coordination spheres for the toluene molecule:

```bash
> cat toluene.xyz
15
Toluene
  C      1.2264      0.0427      0.0670
  C      1.0031     -1.3293      0.0600
  C     -0.2945     -1.8256     -0.0060
  C     -1.3704     -0.9461     -0.0646
  C     -1.1511      0.4266     -0.0578
  C      0.1497      0.9292      0.0066
  C      0.3871      2.3956     -0.0022
  H      2.2495      0.4310      0.1211
  H      1.8510     -2.0202      0.1071
  H     -0.4688     -2.9062     -0.0109
  H     -2.3926     -1.3347     -0.1157
  H     -2.0006      1.1172     -0.1021
  H      0.5024      2.7582     -1.0330
  H      1.2994      2.6647      0.5466
  H     -0.4475      2.9470      0.4506
> kallisto --verbose cnsp --inp toluene.xyz
4.381228500236796
3.3677521535602004
2.8495247846705114
3.366999124462712
4.382826391660659
2.5949138877345828
2.1800188277556742
4.125179817959886
3.9722691198666404
3.801239033949839
3.972333555437317
4.128082932610809
3.7384516775418555
4.073729305140565
4.075067940009211
# Save output to file 'cnsp'
> kallisto --verbose cnsp --inp toluene.xyz cnsp
> cat cnsp
4.381228500236796
3.3677521535602004
2.8495247846705114
3.366999124462712
4.382826391660659
2.5949138877345828
2.1800188277556742
4.125179817959886
3.9722691198666404
3.801239033949839
3.972333555437317
4.128082932610809
3.7384516775418555
4.073729305140565
4.075067940009211
```

