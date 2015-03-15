# The Herd Feeding Problem #

---

## Adapted from a real-world problem ##

---


  1. [The problem description](http://130.216.209.237/engsci392/pulp/FeedingTheHerd#description)

> 2. [Student Tasks](http://130.216.209.237/engsci392/pulp/FeedingTheHerd#tasks)


## Problem Description ##

---


When determining how to feed a herd of dairy cows, farmers need to take into account many different parameters, e.g.,
  * How much milk they want the cows to produce;
  * The price of the various feed types;
  * If the cows are pregnant and how far through their pregnancy are they;
  * How much pasture their farm currently has for grazing.

Farmers will often turn to farm consultants to help them make the best decision. In this case study we are going to analyse the decision suggested by a farm consultant.

The following table gives some typical amounts of MJME (megajoules of metabolisable energy) required for a cow each day in order for it to produce various amounts of milk that day.

![http://pulp-or.googlecode.com/svn/wiki/milk_table.jpg](http://pulp-or.googlecode.com/svn/wiki/milk_table.jpg)

Cows get MJME from their feed, or more specifically the amount of DM (dry matter) in their feed. The next table give a list of possible feed types, their cost, %DM, MJME per kgDM as well as their percentage of protein and NDF (neutral detergent fibre).

![http://pulp-or.googlecode.com/svn/wiki/feed_table.jpg](http://pulp-or.googlecode.com/svn/wiki/feed_table.jpg)

This month, a consultant has estimated that a herd of 350 cows each requires 180 MJME per day to produce 23 L of milk. For nutrition they need their feed to contain 17% protein and 32% NDF.

He also estimates the farm has 1920 kg of usable pasture.

His feed solution for each cow is given below.

![http://pulp-or.googlecode.com/svn/wiki/feed_solution.jpg](http://pulp-or.googlecode.com/svn/wiki/feed_solution.jpg)

The farm wants to know if this is the best possible solution.

For more information on MJME, DM, etc see [Farmingshow.com - Straggle Muster 113](http://www.farmingshow.com/stragglemuster/muster113.htm).


## Student Tasks ##

---


Write a Python file to solve The Herd Feeding Problem using PuLP. Write a management summary of your solution. Be sure to compare it to the consultant's solution.
What to hand in Your Python file. Your management summary.