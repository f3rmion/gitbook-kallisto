---
description: Calculate atomic dynamic polarizabilities.
---

# Polarizabilities

## Introduction

Accurate dynamic polarizabilities can be determined by time-dependent density functional theory \(TD-DFT\) when applying a large atomic orbital basis set. Such reference TD-DFT calculations are, however, computationally demanding. To overcome this computational bottleneck `kallisto` uses a set of pre-calculated dynamic polarizabilities \([TD-PBE0/d-aug-def2-QZVP level of theory](https://aip.scitation.org/doi/10.1063/1.5090222)\) for each atom and maps the environmental effect \(so-called many-body effect\) to atomic coordination numbers. Hence the problem is shifted from calculating dynamic polarizabilities to calculating atomic coordination numbers and interpolate the atomic reference systems. This procedure comes along with a tremendous increase in efficiency and overcomes furthermore numerical issues that could occur in TD-DFT calculations. The accuracy of such polarizabilities is high such that a mean absolute deviation below 5% can be obtained with respect to experimentally derived molecular polarizabilities for small sized organic molecules \(see [statistics](alp.md#molecular-polarizabilities) below\).

We introduced the concept of [atomic coordination numbers](https://app.gitbook.com/@ehjc/s/kallisto/~/drafts/-MQgkWTyy2kFmCRZXTvp/features/cns) \(CNs\) earlier. We calculate reference CN-values for each reference system and map all calculated TD-DFT polarizabilities to reference CN-values. Now we have a simple mapping from CN-values to TD-DFT polarizabilities, which is used within a Gaussian weighting scheme together with system-specific CN-values for a system of interest.

$$
\alpha_j(i\omega)=\sum\limits_{j,ref=1}^{N_{j,ref}}\alpha_{j,ref}(i\omega)\,W_{j,ref}^j
$$

The above equation sums over all pre-calculated TD-DFT polarizabilities \(count of `Nj,ref`\) each having a weight associated such that all weights sum up to unity. So how do we get the weighting coefficients? This is exactly where the CNs become important

$$
W_{j,ref}^j\left(CN_j, CN_{j,ref}\right) = \frac{\sum\limits_{j=1}^{N_s}\exp{\left(-\beta\times j\left(CN_j-CN_{j,ref}\right)^2\right)}}{\sum\limits_{j,ref=1}^{N_{j,ref}}\sum\limits_{j=1}^{N_s}\exp{\left(-\beta\times j\left(CN_j-CN_{j,ref}\right)^2\right)}},
$$

with the calculated CNs for the system of interest and of all reference systems. The equation above uses the limit `Ns` for one of the summations, which is determined separately for each reference system \(for those details [check out the paper](https://chemrxiv.org/articles/preprint/A_Generally_Applicable_Atomic-Charge_Dependent_London_Dispersion_Correction_Scheme/7430216)\).Note that the dynamic reference polarizabilities can be pre-scaled to, e.g., incorporate atomic-charge information as has been introduced recently by [Caldeweyher et al](https://doi.org/10.26434/chemrxiv.7430216.v2). This approach uses an empirical charge-scaling function \(`zeta`\) to re-scale reference dynamic polarizabilities with respect to [electronegativity equilibration atomic partial charges](https://app.gitbook.com/@ehjc/s/kallisto/~/drafts/-MQgoO_6n1o2gY4PTCcJ/features/eeq) that enter afterwards the Gaussian weighing as discussed above, respectively.

$$
\alpha_{j,ref}'(i\omega) = \alpha_{j,ref}(i\omega)\zeta
$$

### Molecular Polarizabilities

We obtain molecular polarizabilities as the sum of all atomic ones \(see below\). This approximation offers the possibility to calculate accurate molecular polarizabilities efficiently.

$$
\alpha_{mol} = \sum\limits_{i=1}^N \alpha_i
$$

The direct comparison to experimental polarizabilities shows the great success of the implemented method. As can be seen in the table below `kallisto` calculates molecular polarizabilities \(for 47 organic molecules - see [complete benchmark](https://github.com/f3rmion/molpol135) with overall 135 structures\) that are comparable to accurate quantum chemistry calculations \(MP2/def2-QZVPD\), but several orders of magnitude faster! We furthermore compare to the recently published AlphaML model \(CCSD mode\) and to the [python](https://github.com/dftd4/dftd4/tree/main/python) `dftd4`API, which uses a pre-compiled Fortran library.

| **Measure in %** | \*\*\*\*[**MP2**](https://aip.scitation.org/doi/abs/10.1063/1.4932594)\*\*\*\* | \*\*\*\*[**kallisto**](https://github.com/AstraZeneca/kallisto)\*\*\*\* | \*\*\*\*[**AlphaML**](https://tools.materialscloud.org/alphaml/input_structure/)\*\*\*\* |
| :--- | :--- | :--- | :--- |
| **MAD** | 3.1 | 4.7 | 10.9 |
| **MD** | -2.6 | -2.2 | -0.8 |
| **RMSD** | 3.1 | 6.8 | 20.6 |
| **AMAX** | 16.9 | 22.3 | 74.4 |
|  |  |  |  |
| Timings | [_dftd4_](https://github.com/dftd4/dftd4/tree/main/python)\_\_ | \_\_[_kallisto_](https://github.com/AstraZeneca/kallisto)\_\_ | \_\_[_AlphaML_](https://tools.materialscloud.org/alphaml/input_structure/)\_\_ |
| _**tCPU / s\***_ | 0.3 | 9.9 | 152.0 |

**MAD** = Mean Absolute Deviation; **MD** = Mean Deviation; **RMSD** = Root-Mean Squared Deviation; **AMAX** = Absolut MAXimum deviation.

**\***Total amount of computation time to obtain molecular polarizabilities for 45 organic molecules including: [1-3-butadiene](https://github.com/f3rmion/molpol135/blob/main/structures/1-3-butadiene/inp.xyz), [1-butene](https://github.com/f3rmion/molpol135/blob/main/structures/1-butene/inp.xyz), [2-methyl-1-propene](https://github.com/f3rmion/molpol135/blob/main/structures/2-methyl-1-propene/inp.xyz), [acetaldehyde](https://github.com/f3rmion/molpol135/blob/main/structures/acetaldehyde/inp.xyz), [acetone](https://github.com/f3rmion/molpol135/blob/main/structures/acetone/inp.xyz), [adamantane](https://github.com/f3rmion/molpol135/blob/main/structures/adamantane/inp.xyz), [benzene](https://github.com/f3rmion/molpol135/blob/main/structures/benzene/inp.xyz), [C2H2](https://github.com/f3rmion/molpol135/blob/main/structures/C2H2/inp.xyz), [C2H4](https://github.com/f3rmion/molpol135/blob/main/structures/C2H4/inp.xyz), [C2H6](https://github.com/f3rmion/molpol135/blob/main/structures/C2H6/inp.xyz), [CH3Cl](https://github.com/f3rmion/molpol135/blob/main/structures/CH3Cl/inp.xyz), [CH3CN](https://github.com/f3rmion/molpol135/blob/main/structures/CH3CN/inp.xyz), [CH3OH](https://github.com/f3rmion/molpol135/blob/main/structures/CH3OH/inp.xyz), [CH3SH](https://github.com/f3rmion/molpol135/blob/main/structures/CH3SH/inp.xyz), [CH4](https://github.com/f3rmion/molpol135/blob/main/structures/CH4/inp.xyz), [CO2](https://github.com/f3rmion/molpol135/blob/main/structures/CO2/inp.xyz), [cyclopropane](https://github.com/f3rmion/molpol135/blob/main/structures/cyclopropane/inp.xyz), [dimethylamine](https://github.com/f3rmion/molpol135/blob/main/structures/dimethylamine/inp.xyz), [dimethylether](https://github.com/f3rmion/molpol135/blob/main/structures/dimethylether/inp.xyz), [E-2-butene](https://github.com/f3rmion/molpol135/blob/main/structures/E-2-butene/inp.xyz), [ethanol](https://github.com/f3rmion/molpol135/blob/main/structures/ethanol/inp.xyz), [ethoxyethane](https://github.com/f3rmion/molpol135/blob/main/structures/ethoxyethane/inp.xyz), [H2CO](https://github.com/f3rmion/molpol135/blob/main/structures/H2CO/inp.xyz), [H2O](https://github.com/f3rmion/molpol135/blob/main/structures/H2O/inp.xyz), [H2S](https://github.com/f3rmion/molpol135/blob/main/structures/H2S/inp.xyz), [HCN](https://github.com/f3rmion/molpol135/blob/main/structures/HCN/inp.xyz), [methyl-propyl-ether](https://github.com/f3rmion/molpol135/blob/main/structures/methyl-propyl-ether/inp.xyz), [N2O](https://github.com/f3rmion/molpol135/blob/main/structures/N2O/inp.xyz), [n-butane](https://github.com/f3rmion/molpol135/blob/main/structures/n-butane/inp.xyz), [NCCN](https://github.com/f3rmion/molpol135/blob/main/structures/NCCN/inp.xyz), [neopentane](https://github.com/f3rmion/molpol135/blob/main/structures/neopentane/inp.xyz), [NH3](https://github.com/f3rmion/molpol135/blob/main/structures/NH3/inp.xyz), [n-heptane](https://github.com/f3rmion/molpol135/blob/main/structures/n-heptane/inp.xyz), [n-hexane](https://github.com/f3rmion/molpol135/blob/main/structures/n-hexane/inp.xyz), [n-octane](https://github.com/f3rmion/molpol135/blob/main/structures/n-octane/inp.xyz), [n-pentane](https://github.com/f3rmion/molpol135/blob/main/structures/n-pentane/inp.xyz), [OCS](https://github.com/f3rmion/molpol135/blob/main/structures/OCS/inp.xyz), [oxirane](https://github.com/f3rmion/molpol135/blob/main/structures/oxirane/inp.xyz), [propadiene](https://github.com/f3rmion/molpol135/blob/main/structures/propadiene/inp.xyz), [propane](https://github.com/f3rmion/molpol135/blob/main/structures/propane/inp.xyz), [propyne](https://github.com/f3rmion/molpol135/blob/main/structures/propyne/inp.xyz), [SO2](https://github.com/f3rmion/molpol135/blob/main/structures/SO2/inp.xyz), [SO3](https://github.com/f3rmion/molpol135/blob/main/structures/SO3/inp.xyz), and [trimethylamine](https://github.com/f3rmion/molpol135/blob/main/structures/trimethylamine/inp.xyz)\). Timings for `dftd4` and `kallisto` have been obtained by [@awvwgk](https://github.com/AstraZeneca/kallisto/issues/27) and are averaged over five runs on a Skylake, Intel\(R\) Core\(TM\) i7-6500U CPU @ 2.50GHz. `AlphaML` values were taken from the printout of their [webinterface](https://tools.materialscloud.org/alphaml/input_structure/). Total timing is calculated as the sum of all contributions.

## Define the Subcommand

{% tabs %}
{% tab title="alp" %}
```bash
> kallisto alp options arguments
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

--molecular (flag)
(optional, default: false)
description:
 get the molecular polarizability as sum of all atomic ones
```
{% endtab %}

{% tab title="arguments" %}
```bash
output: 
 standard output or specified file
```
{% endtab %}
{% endtabs %}

## Application

To calculate atomic dynamic polarizabilities for a neutral charged Alanine-Glycine molecule, we call the subcommand `alp`

```bash
> kallisto alp --inp alanine-glycine.xyz
6.797559893536487
7.954558030234794
8.343416502883054
6.874125501683613
7.912180255606206
6.205524049384421
8.929930573457574
6.216975421946396
6.374242458036639
1.3827173212295591
1.3536217412847078
7.549015744100922
1.9657806025363944
1.4088758603316331
1.8573692724029527
1.8673376164561566
1.336319279749363
1.9359520557775551
1.9173190746286342
2.0092941860457025
# Save output to file 'alp'
> kallisto alp --inp alanine-glycine.xyz alp
> cat alp
6.797559893536487
7.954558030234794
8.343416502883054
6.874125501683613
7.912180255606206
6.205524049384421
8.929930573457574
6.216975421946396
6.374242458036639
1.3827173212295591
1.3536217412847078
7.549015744100922
1.9657806025363944
1.4088758603316331
1.8573692724029527
1.8673376164561566
1.336319279749363
1.9359520557775551
1.9173190746286342
2.0092941860457025
# Get the molecular polarizability for the Alanine-Glycine molecule
> kallisto alp --inp alanine-glycine.xyz --molecular
90.19211544088955
```

Now we obtain a list of atomic dynamic polarizabilities. Molecular polarizabilities can be calculated by using the `molecular` flag. We can furthermore calculate dynamic polarizabilities for the cationic \(or anionic\) Alanine-Glycine molecule by incorporating the `chrg` option as described in the subcommand definition.

