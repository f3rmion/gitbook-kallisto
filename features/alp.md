---
description: Calculate atomic dynamic polarizabilities.
---

# Dynamic Polarizabilities

## Introduction

Accurate dynamic polarizabilities can be determined by time-dependent density functional theory \(TD-DFT\) when applying a large atomic orbital basis set. Such reference TD-DFT calculations are, however, computationally demanding. To overcome this computational bottleneck, `kallisto` uses a set of pre-calculated dynamic polarizabilities for each atom and maps the environmental effect \(so-called many-body effect\) to atomic coordination numbers. Hence the problem is shifted from calculating dynamic polarizabilities to calculating atomic coordination numbers and interpolate the atomic reference systems. This procedure comes along with a tremendous increase in efficiency and overcomes furthermore numerical issues that could occur in TD-DFT calculations.

I introduced the concept of [atomic coordination numbers](https://app.gitbook.com/@ehjc/s/kallisto/~/drafts/-MQgkWTyy2kFmCRZXTvp/features/cns) \(CNs\) earlier. We calculate reference CN-values for each atomic reference polarizability and map those values to the reference CN. 

## Application



