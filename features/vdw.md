---
description: Calculate atomic van der Waals radii.
---

# van-der-Waals Radii

## Introduction

Atomic van-der-Waals radii ...

## Define the Subcommand

{% tabs %}
{% tab title="vdw" %}
```bash
> kallisto --verbose vdw options arguments 
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
 
 --vdwtype <string>
 (optional, default: rahm)
 description:
  reference atomic van der Waals radii
   rahm: 10.1002/chem.201700610
   truhlar: 10.1021/jp8111556
   
--angstrom (flag)
(optional, default: radii in Bohr)
description:
 calculate van-der-Waals radii in Ångström
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



