---
title: 'Fix Power Flow Divergence and TDS Initialization Error in ANDES'
date: 2022-11-23
permalink: /posts/2022/11/andes_init_debug/
tags:
  - Power System Modeling
  - ANDES
  - LTB
  - Open Source
---
As dsicussed in [ANDES Discussions #386](https://github.com/cuihantao/andes/discussions/386), the user may run into ***power flow divergence*** or ***TDS initialization error*** when revising cases file from given cases. In this blog, we will discuss how to fix these errors. The case files and source code can be found at [andes_init_debug](https://github.com/jinningwang/jinningwang/tree/main/blogs/andes_init_debug).

# Power flow divergence

AC power flow resutls are used as the initialization points of TDS. In ANDES, devices ``Bus``, ``PQ``, ``PV``, ``Slack``, ``Shunt``, ``Line`` are used to solve AC power flow. Usually, the user may revise the system topology, such as adding new devices (`Bus`) or changing load (``PQ``). Belows are some possible reasons for failed power flow:

1. Power load unbalance is too large;
2. Bus initial voltage and angle are inapproriate.

# TDS initialization error

After solving the AC power flow, the dynamic device can be initialized from the power flow results. Belows list some possible reasons for failed TDS initialization:

1. Inapproriate limiter values, usually occurs in ``TurbineGov``, ``Exciter`` if power flow is changed significantly;
2. Inapproriate dynamic devcie parameters;
3. Inapproriate equations in dynamic model, usually happens when developing new models.
