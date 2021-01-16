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

To sort an ethane molecule according to a breadth-first algorithms us the subcommand `sort`

```bash
> cat ethane.xyz
8
ethane
C	0.00 0.00 -1.10
H	2.03 0.76 -1.25
H	-1.00	0.27 -1.47
H	0.27 -1.00 -1.47
H	1.03 1.03 -2.71
C	1.03 1.03 -1.61
H	0.76 2.03 -1.25
H	0.00 0.00 0.00
# Save BFS sorted structure to 'ethane_s.xyz'
> kallisto sort --inp ethane.xyz --start 0 > ethane_s.xyz
> cat ethane_s.xyz
    8
Created with kallisto
C      0.0000    0.0000   -1.1000
H     -1.0000    0.2700   -1.4700
H      0.2700   -1.0000   -1.4700
C      1.0300    1.0300   -1.6100
H      0.0000    0.0000    0.0000
H      2.0300    0.7600   -1.2500
H      1.0300    1.0300   -2.7100
H      0.7600    2.0300   -1.2500
```

The depiction below shows the sorting for the ethane molecule. On the left side the initial coordinates are shown, while the right side presents the sorted structure with `start = 0`.

![](../.gitbook/assets/bfs.png)

