# The Data Fitting Problem #

---

## Also known as The Least Squares Problem ##

## Problem Description ##

---

When modelling data, scientists often want to fit an analytical model to their experimental data. In this case an experiment has provided some(x,y)-coordinates that have a growth curve shape, i.e., initially  increases quickly with , thens tails off to some maximum value. The scientists in this study have suggested three possible functions to model this behaviour:

  1. ![http://pulp-or.googlecode.com/svn/wiki/1892607815-14px.png](http://pulp-or.googlecode.com/svn/wiki/1892607815-14px.png)
  1. ![http://pulp-or.googlecode.com/svn/wiki/527908802-14px.png](http://pulp-or.googlecode.com/svn/wiki/527908802-14px.png)
  1. ![http://pulp-or.googlecode.com/svn/wiki/1061364386-14px.png](http://pulp-or.googlecode.com/svn/wiki/1061364386-14px.png)


Given one of the possible functions f(x) and the data points xi they want to find a, b  and c to minimize the squared distance between the data points and the estimates, i.e.,

![http://pulp-or.googlecode.com/svn/wiki/1072468793-14px.png](http://pulp-or.googlecode.com/svn/wiki/1072468793-14px.png)


---

The scientists have specified the number of data points and their coordinates in a [data file](http://130.216.209.237/engsci392/pulp/Regression%20Data).

The scientists want to know which of the suggested functions provides the best fit to the data.


## Student Tasks ##

---

Write a Python file to solve The Data Fitting Problem using PuLP. Write a management summary of your solution. Be sure to indicate which of the functions fits the data best.
**What to hand in** Your Python file. Your management summary.