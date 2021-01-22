---
description: Calculate the root-mean squared deviation using quaternions.
---

# Root Mean Square Deviation

## Introduction

A widely used way to compare the structures is to translate and rotate one structure with respect to the other to minimize the root mean square deviation \(RMSD\). We implemented a simple scheme, based on quaternions, for the optimal transformation \(rotation-translation\) that minimizes the RMSD between two sets of structures.

Quaternions are generally represented in the form

$$
q = a+b\,\mathbf{i} +c\,\mathbf {j} +d\,\mathbf {k}
$$

with `a`, `b`, `c`, and `d` are real numbers; and **i**, **j**, and **k** are the fundamental quaternion units.

## Define the Subcommand

{% tabs %}
{% tab title="rms" %}
```bash
> kallisto --verbose rms options arguments
```
{% endtab %}

{% tab title="options" %}
```markup
--compare <string> <string>
(required)
description: 
 compare two input files in xmol format (Ångström) 
 or in Turbomole format (Bohr) and calculate a RMSD 
 error and a rotation matrix
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

