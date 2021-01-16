---
description: Calculate the root-mean squared deviation using quaternions.
---

# Root Mean Squared Deviation

### Introduction

### Define the Subcommand

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
```
output:
 standard output or specified file
```
{% endtab %}
{% endtabs %}

### Application

