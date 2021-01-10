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

To calculate atomic van-der-Waals radii for a neutral charged Alanine-Glycine molecule, I call the subcommand `vdw`

```bash
> kallisto --verbose vdw --inp alanine-glycine.xyz
3.3065606171598922
3.38164759676716
3.4391750162303536
3.311855692814488
3.3790680338248973
3.2967634203187104
3.4727151121721547
3.2976318319108247
3.3094215076503897
2.420916892530216
2.4135730093586507
3.356462625678808
2.5457085831894677
2.4274072320381417
2.5251614207290154
2.527093029228339
2.409141369050233
2.540154025796337
2.536646925483585
2.5536833297719026
# Save output to file 'vdw'
> kallisto --verbose vdw --inp alanine-glycine.xyz vdw
3.3065606171598922
3.38164759676716
3.4391750162303536
3.311855692814488
3.3790680338248973
3.2967634203187104
3.4727151121721547
3.2976318319108247
3.3094215076503897
2.420916892530216
2.4135730093586507
3.356462625678808
2.5457085831894677
2.4274072320381417
2.5251614207290154
2.527093029228339
2.409141369050233
2.540154025796337
2.536646925483585
2.5536833297719026
```



