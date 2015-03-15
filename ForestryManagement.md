# The Forestry Management Problem #

---

## Adapted from a real-world problem ##

---

  1. [The problem description](http://130.216.209.237/engsci392/pulp/ForestryManagement#description)

> 2. [Extra for Experts](http://130.216.209.237/engsci392/pulp/ForestryManagement#extra)

> 3. [Student Tasks](http://130.216.209.237/engsci392/pulp/ForestryManagement#tasks)

## Problem Description ##

---

A paper company own a number of mills that produce paper with different processes, e.g., the thermo-mechanical process and the cold caustic soda process. They procure raw materials for each of their processing machines from a number of different suppliers.

`Thermo-mechanical Processing Machine`

![http://pulp-or.googlecode.com/svn/wiki/forestry_1.jpg](http://pulp-or.googlecode.com/svn/wiki/forestry_1.jpg)


Their suppliers consist of 3 forestry operations: Kaingaroa, NSW and Taupo. They also own a recycling plant where they receive waste paper.

They own mills at Kawerau (NZ), Boyer (Tasmania) and Albury (NSW). The following table summarises the processing machines at each mill:

|    |Thermo-Mechanical | Refiner-Mechanical | Stone Groundwood | Cold Caustic Soda | Recycled Fibre |
|:---|:-----------------|:-------------------|:-----------------|:------------------|:---------------|
|Mill | Process (TMP) | Process (RMP) | Process (SGW) | Process (CCS) | Process (RCF) |
|Kawerau | yes | yes | yes |no | no |
|Boyer  |yes | no  |no | yes | no |
|Albury  |yes | no | no | no | yes |


The paper company purchases three types of raw materials: woodchips, pulp logs and waste paper. The thermo-mechanical, refiner-mechanical and cold caustic soda processes use woodchips, the stone groundwood process uses pulp logs and the recycled fibre process uses waste paper. The requirements (in tonnes) for their different machines are given below:

|    | Thermo-Mechanical | Refiner-Mechanical | Stone Groundwood | Cold Caustic Soda | Recycled Fibre |
|:---|:------------------|:-------------------|:-----------------|:------------------|:---------------|
|Mill | Process (TMP) | Process (RMP) | Process (SGW) | Process (CCS) | Process (RCF) |
|Kawerau | 10 | 15 | 52 | - | - |
|Boyer | 15 | - | - | 10 | - |
|Albury | 20 | - | - | - | 22 |


The supplies of the various raw material is given in the following table:

![http://pulp-or.googlecode.com/svn/wiki/forestry_table.jpg](http://pulp-or.googlecode.com/svn/wiki/forestry_table.jpg)


The transportation cost of the raw materials is given in the following table:


Note that pulp logs can be "chipped" into woodchips at the suppliers at a cost of $250/tonne and that waste paper can be "compacted" into woodchips at the recycling plant at a cost of $600/tonne. Any excess waste paper that is not used must be disposed of at a cost of $150/tonne.

`Tree Chipper`

![http://pulp-or.googlecode.com/svn/wiki/forestry_2.jpg](http://pulp-or.googlecode.com/svn/wiki/forestry_2.jpg)


The paper company want to know how to supply their mills at minimum cost. They also want to know how much "streamlining" their processes (i.e., reduce the amount of raw materials they use) will reduce their overall transportation costs.

For more detail see [Supply Chain Optimisation in the Paper Industry, Philpott and Everett](http://www.springerlink.com/content/jawl58272mytx03h/)


## Extra for Experts ##

---

### Student Tasks ###

---

Solve The Forestry Management Problem as a single balanced transportation problem. Write a management summary of your solution, including an answer to the "streamlining" question.
**What to hand in** Your Python files. Your management summary.

### Extra for Experts' Tasks ###

---

Instead of solving The Forestry Management Problem as a single transportation problem, solve it as three separate transportation problems, one for each raw material..
**What to hand in** Your Python file(s).