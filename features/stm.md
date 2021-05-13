---
description: 'Calculate Sterimol descriptors L, Bmin, and Bmax.'
---

# Sterimol

## Introduction

The multidimensional Sterimol parameters were developed by [Verloop](https://www.sciencedirect.com/science/article/pii/B9780080292229500512) and the original Sterimol program by [Verloop and Hoogenstraaten](http://www.ccl.net/cca/software/SOURCES/FORTRAN/STERIMOL/) to capture the dimensions and thus the steric interactions of a substituent along different directions. Using [Corey-Pauling-Koltun](https://www.pnas.org/content/37/4/205.short) molecular models \([CPK-model](https://en.wikipedia.org/wiki/Space-filling_model)\), major axes Bmin, Bmax, and L can be defined around the binding point of a given substituent. In short, Bmin represents the shortest distance perpendicular to the primary attachment axis, while Bmax represents the longest distance. These two sub-parameters can be considered the minimum and maximum width of a substituent and are influenced by the extent of branching. The last subparameter L is the total distance that follows the primary bond axis and thus refers to the length.

An example of how the Sterimol descriptors of an ethane molecule along the C2-C5 bond are constructed is shown below \(depiction is taken from [here](https://github.com/bobbypaton/DBSTEP)\). For the calculation of Sterimol descriptors `kallisto` uses van-der-Waals radii that are obtained from atomic static polarizabilities as described in the section [van-der-Waals Radii](https://app.gitbook.com/@ehjc/s/kallisto/~/drafts/-MRAfxINKqRBUyA1POhp/features/vdw). 



![](../.gitbook/assets/sterimol_new.png)

{% hint style="info" %}
The applied Sterimol algorithm has been initially implemented in the [Morfeus](https://kjelljorner.github.io/morfeus/sterimol.html) software package and was integrated by permission of its [main developer](https://scholar.google.com/citations?hl=de&user=85jiD4EAAAAJ).
{% endhint %}

## Define the Subcommand

{% tabs %}
{% tab title="stm" %}
```bash
> kallisto stm options arguments
```
{% endtab %}

{% tab title="options" %}
```markup
# Note that the atom count starts at 0
--origin <int>
(required)
description:
 number of the origin atom

# Note that the atom count starts at 0
--partner <int>
(required)
description:
 number of the partner atom
 
--out <string> 
(optional)
description: 
 write output to file
```
{% endtab %}

{% tab title="arguments" %}
```text
input file is given as (positional) argument
```
{% endtab %}
{% endtabs %}

## Application

To calculate Sterimol parameter for an ethane molecule along the C2-C5 bond, we use the subcommand `stm`

```bash
> cat ethane.xyz
8
ethane
H    0.00 0.00 0.00
C    0.00 0.00 -1.10
H    -1.00 0.27 -1.47
H    0.27 -1.00 -1.47
C    1.03 1.03 -1.61
H    1.03 1.03 -2.71
H    2.03 0.76 -1.25
H    0.76 2.03 -1.25
# Note that the counting of atoms starts at 0
> kallisto stm --origin 1 --partner 4 ethane.xyz
Calculated for atom 1 (origin) and atom 4 (partner)
L, Bmin, Bmax / au:  6.29  4.27  4.54
L, Bmin, Bmax / A:  3.33  2.26  2.40
# Save output to file 'stm'
> kallisto stm --out stm --origin 1 --partner 4 ethane.xyz
> cat stm
Calculated for atom 1 (origin) and atom 4 (partner)
L, Bmin, Bmax / au:  6.29  4.27  4.54
L, Bmin, Bmax / A:  3.33  2.26  2.40
```

