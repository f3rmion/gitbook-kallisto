---
description: 'Calculate Sterimol descriptors L, Bmin, and Bmax.'
---

# Sterimol Descriptors

### Introduction

An example how the Sterimol descriptors of an ethane molecule along the C2-C5 bond are constructed is shown below \(depiction taken from [here](https://github.com/bobbypaton/DBSTEP)\).

### 

![](../.gitbook/assets/sterimol_new.png)

### Define the Subcommand

{% tabs %}
{% tab title="stm" %}
```bash
> kallisto --verbose stm options arguments 
```
{% endtab %}

{% tab title="options" %}
```markup
--inp <string> 
(optional, default: coord)
description: 
 input file in xmol format (Ångström) or in Turbomole format (Bohr)
```
{% endtab %}

{% tab title="arguments" %}
```
output: 
 standard output or specified file
```
{% endtab %}
{% endtabs %}

