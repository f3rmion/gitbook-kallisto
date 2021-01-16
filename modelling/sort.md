---
description: Sort your structure according to the breadth-first search algorithm.
---

# Breadth First Sorting

### Introduction

### Define the Subcommand

{% tabs %}
{% tab title="sort" %}
```bash
> kallisto --verbose sort options arguments
```
{% endtab %}

{% tab title="options" %}
```markup
--inp <string> 
(optional, default: coord)
description: 
 input file in xmol format (Ångström) or in Turbomole format (Bohr)
 
# Note that the atom count starts at 0
--start <int>
(optional)
description:
 start BFS from given atom
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

![](../.gitbook/assets/bfs.png)

