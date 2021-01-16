---
description: Simply exchange a found substructure with another.
---

# Substructure Exchanger

## Introduction

## Define the Subcommand

{% tabs %}
{% tab title="exs" %}
```bash
> kallisto --verbose exs options arguments
```
{% endtab %}

{% tab title="options" %}
```markup
--inp <string> <string>
(required)
description: 
 two input files in xmol format (Ångström) 
 or in Turbomole format (Bohr). Both formats need
 to match. First <string> is the reference and 
 second <string> the new structure 

# Note that the atom count starts at 0
--center <int>
(required)
description:
 central atom for which covalently bound substructures are obtained

# Note that the substructure count starts at 0
--subnr <int>
(required)
description:
 substructure to be replaced by new structure
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

