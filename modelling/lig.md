---
description: Get all substructures attached to a specified atom.
---

# Substructure Finder

## Introduction

Often we are interested in the finding substructures, e.g., ligands that are covalently bound to a metal center within an organometallic catalyst structure. Here, we need information about the molecular graph. This information is, however, not adequate enough to write out ligands or other substructures. Within the `kallisto` program we implemented a recursive way to deal with substructures that are covalently bound to a specified atom \(termed as the `center`\).

## Define the Subcommand

{% tabs %}
{% tab title="lig" %}
```bash
> kallisto lig options arguments
```
{% endtab %}

{% tab title="options" %}
```markup
# Note that the atom count starts at 0
--center <int>
(required)
description:
 central atom for which covalently bound substructures are obtained
 
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

Let's dive directly into an example to extract substructures for the Iridium atom within an organometallic transition state structure describing the oxidative addition of pyridine \(B3LYP-D3\(BJ\)/LACVP\*\*/PBF\(THF\) level\) with an Iridium catalyst as pioneered by [Hartwig](https://pubs.acs.org/doi/10.1021/ja412563e).

![](../.gitbook/assets/iridiumcat.png)

```bash
> cat iridium.xyz
96

N    -1.3672999   -1.4398999    0.1359000
C    -2.4911998   -0.6808999    0.1396000
C    -3.6534996   -1.1211999   -0.5090000
C    -3.6468996   -2.3434998   -1.1725999
C    -2.4848998   -3.1187997   -1.1555999
C    -1.3670999   -2.6316997   -0.4883000
H    -0.4373000   -3.1872997   -0.4306000
H    -2.4432998   -4.0866996   -1.6463998
H    -4.5575996   -0.5223999   -0.4887000
C    -2.4206998    0.5908999    0.8954999
N    -1.2879999    0.7903999    1.6181998
C    -1.1378999    1.9348998    2.3084998
C    -2.1077998    2.9319997    2.3219998
C    -3.2770997    2.7402997    1.5819998
C    -3.4330997    1.5600998    0.8608999
H    -4.3267996    1.4057999    0.2659000
H    -1.9411998    3.8419996    2.8913997
H    -0.1872000    2.0459998    2.8181997
Ir    0.4009000   -0.6061999    1.1172999
C    -1.2690999   -3.8143996    3.7856996
C    -0.1664000   -4.5494996    4.2269996
C     1.1218999   -4.0950996    3.9273996
C     1.2993999   -2.9384997    3.1675997
C     0.2001000   -2.2075998    2.6786997
C    -1.0849999   -2.6466997    3.0382997
H    -1.9573998   -2.0870998    2.7090997
H     0.8509999   -0.7173999    2.6636997
H     2.3007998   -2.5989997    2.9226997
H    -0.3087000   -5.4547995    4.8119995
B     0.6392999    0.6220999   -0.5923999
O    -0.0586000    0.3754000   -1.7751998
C     0.0637000    1.5387999   -2.6275997
C     0.0955000    1.0794999   -4.0821996
H     0.8716999    0.3276000   -4.2397996
H     0.2802000    1.9248998   -4.7547995
H    -0.8681999    0.6330999   -4.3491996
C    -1.1760999    2.4077998   -2.3666998
H    -1.2042999    3.2867997   -3.0193997
H    -2.0717998    1.8058998   -2.5499998
H    -1.2019999    2.7410997   -1.3247999
C     1.3891999    2.1923998   -2.1029998
O     1.3915999    1.7859998   -0.7128999
C     2.6481997    1.5975998   -2.7492997
H     2.6573997    0.5124000   -2.6283997
H     2.7186997    1.8556998   -3.8108996
H     3.5309997    1.9918998   -2.2375998
C     1.4299999    3.7172996   -2.1670998
H     0.6241999    4.1645996   -1.5814998
H     2.3812998    4.0763996   -1.7610998
H     1.3476999    4.0651996   -3.2032997
B     2.0756998    0.4378000    1.7666998
O     3.3654997   -0.0810000    1.8671998
C     4.2709996    1.0315999    2.0579998
C     5.4819995    0.5533999    2.8527997
H     5.1838995    0.0640000    3.7825996
H     6.0490994   -0.1689000    2.2567998
H     6.1442994    1.3928999    3.0939997
C     4.6909995    1.5017999    0.6583999
H     5.4398995    2.2997998    0.7063999
H     5.1090995    0.6483999    0.1171000
H     3.8181996    1.8505998    0.1015000
C     3.3502997    2.0656998    2.7942997
O     2.0458998    1.7442998    2.2507998
C     3.6590996    3.5300997    2.4959998
H     3.5358997    3.7464996    1.4332999
H     2.9753997    4.1760996    3.0565997
H     4.6847995    3.7776996    2.7930997
C     3.2796997    1.8273998    4.3083996
H     3.0708997    0.7747999    4.5225996
H     4.2123996    2.1093998    4.8080995
H     2.4671998    2.4302998    4.7258995
B     1.7917998   -1.7489998    0.1412000
O     1.8500998   -3.1467997    0.2110000
C     3.0569997   -3.5802997   -0.4612000
C     4.1632996   -3.6178996    0.6029999
H     4.3272996   -2.6173997    1.0149999
H     3.8420996   -4.2739996    1.4174999
H     5.1055995   -3.9992996    0.1957000
C     2.8261997   -4.9693995   -1.0466999
H     2.6792997   -5.6906994   -0.2364000
H     3.6907996   -5.2904995   -1.6389998
H     1.9392998   -4.9911995   -1.6839998
C     3.2640997   -2.4330998   -1.5048999
O     2.7238997   -1.2952999   -0.7998999
C     4.7166995   -2.1413998   -1.8718998
H     5.1881995   -3.0188997   -2.3293998
H     4.7565995   -1.3170999   -2.5912997
H     5.2941995   -1.8488998   -0.9925999
C     2.4197998   -2.6279997   -2.7728997
H     1.3752999   -2.8206997   -2.5121998
H     2.4501998   -1.7101998   -3.3667997
H     2.7924997   -3.4536997   -3.3878997
H    -2.2764998   -4.1481996    4.0262996
H     1.9905998   -4.6454995    4.2840996
H    -4.5414996   -2.6926997   -1.6821998
H    -4.0522996    3.5020997    1.5576998
# Search for substructures of the Iridium atom
> kallisto lig --center 18 iridium.xyz
Write out substructures for 18
Substructure 0: [0, 1, 2, 3, 4, 5, 6, 7, 94, 8, 9, 10, 11, 12, 13, 14, 15, 95, 16, 17]
Substructure 1: [10, 9, 1, 0, 5, 4, 3, 2, 8, 94, 7, 6, 14, 13, 12, 11, 17, 16, 95, 15]
Substructure 2: [23, 22, 21, 20, 19, 24, 25, 92, 28, 93, 27]
Substructure 3: [26]
Substructure 4: [29, 30, 31, 32, 33, 34, 35, 36, 37, 38, 39, 40, 41, 42, 43, 44, 45, 46, 47, 48, 49]
Substructure 5: [50, 51, 52, 53, 54, 55, 56, 57, 58, 59, 60, 61, 62, 63, 64, 65, 66, 67, 68, 69, 70]
Substructure 6: [71, 72, 73, 74, 75, 76, 77, 78, 79, 80, 81, 82, 83, 84, 85, 86, 87, 88, 89, 90, 91]
```

We find the following substructures:

| \# | Substructure in complex |
| :--- | :--- |
| 0 | N-ligand |
| 1 | N-ligand |
| 2 | Pyridine |
| 3 | Hydrogen Atom |
| 4 | Bpin-ligand |
| 5 | Bpin-ligand |
| 6 | Bpin-ligand |

