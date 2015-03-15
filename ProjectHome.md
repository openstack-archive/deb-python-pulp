PuLP is an LP modeler written in python. PuLP can generate MPS or LP files and call GLPK (http://www.gnu.org/software/glpk/glpk.html),  COIN (http://www.coin-or.org/),  CPLEX (http://www.cplex.com/), and  GUROBI (http://www.gurobi.com/) to solve linear problems.

See the examples directory for examples.

PuLP requires Python >= 2.5.

The examples require at least a solver in your PATH or a shared library file.

Documentation is found on http://packages.python.org/PuLP/


Use `LpVariable()` to create new variables. To create a variable 0 <= x <= 3
```
>>> x = LpVariable("x", 0, 3)
```

To create a variable 0 <= y <= 1
```
>>> y = LpVariable("y", 0, 1)
```

Use `LpProblem()` to create new problems. Create "myProblem"
```
>>> prob = LpProblem("myProblem", LpMinimize)
```

Combine variables to create expressions and constraints and add them to the
problem.
```
>>> prob += x + y <= 2
```

If you add an expression (not a constraint), it will
become the objective.
```
>>> prob += -4*x + y
```

Choose a solver and solve the problem. ex:
```
>>> status = prob.solve(GLPK(msg = 0))
```

Display the status of the solution
```
>>> LpStatus[status]
'Optimal'
```

You can get the value of the variables using value(). ex:
```
>>> value(x)
2.0
```

Exported Classes:
  * `LpProblem` -- Container class for a Linear programming problem
  * `LpVariable` -- Variables that are added to constraints in the LP
  * `LpConstraint` -- A constraint of the general form
> > a1x1+a2x2 ...anxn (<=, =, >=) b
  * `LpConstraintVar` -- Used to construct a column of the model in column-wise
> > modelling

Exported Functions:
  * `value()` -- Finds the value of a variable or expression
  * `lpSum()` -- given a list of the form `[a1 * x1, a2 * x2, ..., an  * xn]` will
> > construct a linear expression to be used as a constraint or variable
  * `lpDot()` --given two lists of the form `[a1, a2, ..., an]` and
> > `[ x1, x2, ..., xn]` will construct a linear expression to be used
> > as a constraint or variable

Comments, bug reports, patches and suggestions are welcome.

pulp-or-discuss@googlegroups.com


