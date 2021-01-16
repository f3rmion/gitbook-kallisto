---
description: Find the molecular graph according to covalent bonds between atoms.
---

# Molecular Graph Information

## Introduction

## Define the Subcommand

{% tabs %}
{% tab title="bonds" %}
```bash
> kallisto --verbose bonds options arguments
```
{% endtab %}

{% tab title="options" %}
```markup
--inp <string> 
(optional, default: coord)
description: 
 input file in xmol format (Ångström) or in Turbomole format (Bohr)

# Note that the atom count starts at 0
--partner <int>
(optional)
description:
 print all covalent bonds (partner) of atom
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

