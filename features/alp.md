---
description: Calculate atomic dynamic polarizabilities.
---

# Dynamic Polarizabilities

## Introduction

Accurate dynamic polarizabilities can be determined by time-dependent density functional theory \(TD-DFT\) when applying a large atomic orbital basis set. Such reference TD-DFT calculations are, however, computationally demanding. To overcome this computational bottleneck, `kallisto` uses a set of pre-calculated dynamic polarizabilities for each atom and maps the environmental effect \(so-called many-body effect\) to atomic coordination numbers. Hence the problem is shifted from calculating dynamic polarizabilities to calculating atomic coordination numbers and interpolate the atomic reference systems. This procedure comes along with a tremendous increase in efficiency and overcomes furthermore numerical issues that could occur in TD-DFT calculations.

I introduced the concept of [atomic coordination numbers](https://app.gitbook.com/@ehjc/s/kallisto/~/drafts/-MQgkWTyy2kFmCRZXTvp/features/cns) \(CNs\) earlier. We calculate reference CN-values for each reference system and map all calculated TD-DFT polarizabilities to reference CN-values. Now we have a simple mapping from CN-values to TD-DFT polarizabilities, which is used within a Gaussian weighting scheme together with system-specific CN-values for a system of interest. 

$$
\alpha_j(i\omega)=\sum\limits_{j,ref=1}^{N_{j,ref}}\alpha_{j,ref}(i\omega)\,W_{j,ref}^j
$$

The above equation sums over all pre-calulcated TD-DFT polarizabilities each having a weight associated such that all weights sum up to unity. So how do we get the weighting coefficients? This is exactly where the CNs become important

$$
W_{j,ref}^j\left(CN_j, CN_{j,ref}\right) = \frac{\sum\limits_{j=1}^{N_s}\exp{\left(-\beta\times j\left(CN_j-CN_{j,ref}\right)^2\right)}}{\sum\limits_{j,ref=1}^{N_{j,ref}}\sum\limits_{j=1}^{N_s}\exp{\left(-\beta\times j\left(CN_j-CN_{j,ref}\right)^2\right)}},
$$

with the calculated CNs for the system of interest and of all reference systems. Note that the dynamic reference polarizabilities can be pre-scaled to, e.g., incorporate atomic-charge information as has been introduced recently by Caldeweyher et al. This approach uses an empirical charge-scaling function \(`zeta`\) to re-scale reference dynamic polarizabilities with respect to [electronegativity equilibration atomic partial charges](https://app.gitbook.com/@ehjc/s/kallisto/~/drafts/-MQgoO_6n1o2gY4PTCcJ/features/eeq) that enter afterwards the Gaussian weighing, respectively.

$$
\alpha_{j,ref}'(i\omega) = \alpha_{j,ref}(i\omega)\zeta
$$

 

## Define the Subcommand

{% tabs %}
{% tab title="alp" %}
```bash
> kallisto --verbose eeq options arguments 
```
{% endtab %}

{% tab title="options" %}
```text
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
```bash
output: 
 standard output or specified file
```
{% endtab %}
{% endtabs %}

## Application



