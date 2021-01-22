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

with `a`, `b`, `c`, and `d` as real numbers; and **i**, **j**, and **k** as the fundamental quaternion units. The set of quaternions is made a four-dimensional vector space over the real numbers {1, **i**, **j**, **k**} as a basis, where Hamilton defined the quaternion as consisting of a scalar part and a vector part. The vector part of the quaternion can be interpreted as a coordinate in three dimensional space. Operations such as the vector dot product and cross products can be defined in terms of quaternions, and this makes it possible to apply quaternion techniques wherever spatial vectors arise. Such as complex numbers can be represented as matrices, so can quaternions.



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

