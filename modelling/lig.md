---
description: Get all substructures attached to a specified atom.
---

# Substructure Finder

### Introduction

### Define the Subcommand

{% tabs %}
{% tab title="lig" %}
```bash
> kallisto --verbose lig options arguments
```
{% endtab %}

{% tab title="options" %}
```markup
--inp <string> 
(optional, default: coord)
description: 
 input file in xmol format (Ångström) or in Turbomole format (Bohr)
 
--center <int>
(required)
description:
 central atom from which covalently bound substructures are obtained
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

