# The Network Design Problem #

---

## Adapted from a real world problem ##

---

1. [The problem description](http://130.216.209.237/engsci392/pulp/ANetworkDesignProblem#description)

2. [Student Tasks](http://130.216.209.237/engsci392/pulp/ANetworkDesignProblem#tasks)

## Problem Description ##

---

Before undertaking this case study you must (at least) read the [Data Network Flows](http://130.216.209.237/engsci392/pulp/DataNetworkFlows) case study to learn about the components that make up Storage Area Networks (SANs).

The company that commissioned the initial research on routing their data (see [Data Network Flows](http://130.216.209.237/engsci392/pulp/DataNetworkFlows)) has decided to add another storage device (Device C) to their network. They have also performed some extensive data traffic measurement and determined the actual data flow requirements they need to support. These flows are shown in Table 1.


|Source |Destination |Requirement Mb/s |
|:------|:-----------|:----------------|
|Host 1 |Device A |65 |
|Host 1 |Device B| 50 |
|Host 1| Device C |30 |
|Host 2 |Device A| 25|
|Host 2| Device B| 70|
|Host 3 |Device A |35 |
|Host 3 |Device C| 65 |


They estimate they will need either an extra hub or an extra switch or some combination of the 3 hubs and 2 switches. They commissioned the same network consultant to design their new network for them. He finished the job, but left for his honeymoon before writing a management summary or documenting his work. The files he left are contained in:

[san\_design.zip](http://130.216.209.237/engsci392/pulp/san_design.zip)

The company want to use these files to find the optimal SAN design that will support their data flow requirements.

For more detail see [A Mixed-Integer Approach to Storage Area Network Design using Generic Network Components, O’Sullivan and Walker, Engineering Science Technical Report 626, March 2006](http://www.esc.auckland.ac.nz/research/tech/tech.html).


## Student Tasks ##

---

Comment the AMPL files `san_design_neos.mod, san_design.dat` and `san_design_neos.run` from `san_design.zip`. Run these files to find the optimal SAN design to support the flow requirements. Write a management summary for your solution.
**What to hand in** You commented AMPL files. Your management summary.

### Extra for Experts' Tasks ###

---

One problem that often arises in network design (and other mixed-integer programming) is that of symmetry. If components in the network have the same properties, then mixed-integer programming will consider all the combinations of these components even though many combinations represent the same network. The following constraints:


can be used to remove symmetry from the SAN design problem if all the hubs, switches and links have the same properties (i.e., bandwidth capacity, number of port slots, etc).

Add these constraints to `san_design_neos.run` and solve the SAN design problem again. Describe how these constraints remove symmetry. Comment on their effect on the solver's progress.
What to hand in A brief (1 page or less) summary comprised of your description of how the antisymmetry constraints work and their effect on the solver's progress.