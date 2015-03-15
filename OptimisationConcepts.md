# Optimisation Concepts #

## Linear Programing ##
The simplest type of mathematical programme is a linear programme. For your mathematical programme to be a linear programme you need the following conditions to be true:
  1. The decision variables must be real variables;
  1. The objective constraint must be a linear expression;
  1. The constraints must be linear expressions.

Linear expressions are any expression of the form

a\_1x\_1+a\_2x\_2+a\_3x\_3+ ... a\_nx\_n {<= , =, >=} b <br>

where a_1,a_2,a_3,.. a_n and b Image are known quantities and x_1,x_2,x_3,.. x_n are variables. The process of solving a linear programme is called linear programming. Linear programming is done via the Revised Simplex Method (also known as the Primal Simplex Method), the Dual Simplex Method or an Interior Point Method. CPLEX allows you to specify which method you use, but we won’t go into further detail here.<br>
<br>
<h2>Integer Programing</h2>

Integer programmes are almost identical to linear programmes with one very important exception. Some of the decision variables in integer programmes may need to have only integer values. The variables are known as integer variables. Since most integer programmes contain a mix of real variables and integer variables they are often known as mixed integer programmes. While the change from linear programming is a minor one, the effect on the solution process is enormous. Integer programmes can be very difficult problems to solve and there is a lot of current research finding “good” ways to solve integer programmes. Integer programming (the process of solving a (mixed) integer programme) was originally done using the branch-and-bound process. The branch part of the process eliminated non-integer values for integer variables in the following way:<br>
<br>
<ul><li>Initially, all variables are left as real variables. The problem is solved using linear programming;<br>
</li><li>If one of the integer variables in the linear programming solution has a fractional value, e.g., x_1 = 0.5 then the linear programme is split in two and the fractional region eliminated. This is done by branching on the variable value, e.g., adding the constraint x_1<=0 to form one linear programme and x_1>=1 to form the other.<br>
</li><li>By finding the optimal solution in each of these new linear programmes and comparing we can find the optimal solution for the original problem.<br>
</li><li>If either of the new linear programmes has a fractional value for an integer variable then a new branch is needed.</li></ul>

This branching process results in the formation of a branch-and-bound tree (we will discuss the bounding next). Each node in this tree represents a linear programme consisting of the original linear programme and the extra branches added. Eventually all the leaf nodes in the tree will contain solutions where all the integer variables have integer values and no further branching is needed. All these values can be compared and the best one is the solution to the original integer programme.<br>
Note For MIPs of any reasonable size this tree could be huge, in fact it grows exponentially as the number of integer variables increases. The bounding process allows sections of the branch-and-bound tree to be removed from consideration before all the leaf nodes have integer solutions. It relies on the following optimization principle:<br>
<br>
Adding constraints to a mathematical programming will result in a deterioration of the optimal objective value.<br>
<br>
This means that adding the branching constraints to the linear programmes at the branch-and-bound tree nodes will mean the resulting nodes will have an optimal objective function value that is equal to or worse than the optimal objective function value of the original linear programme. Thus the objective function values get worse the deeper into the tree you look. Since we are finding the integer solution in the branch-and-bound tree with the best objective value, we can use any integer solutions to bound the tree. The current best integer solution is called the incumbent. After solving a linear programme at a leaf node of the branch-and-bound tree one of the following conditions holds:<br>
<br>
<ul><li>The linear programme is infeasible (no more branching is possible);<br>
</li><li>The linear programme solution is an integer solution with a better objective value than the incumbent. The incumbent is replaced with this new solution;<br>
</li><li>The linear programme solution has a worse objective than the incumbent. Any nodes created from this node will also have a worse objective than the incumbent. This node is bounded by the incumbent objective;<br>
</li><li>The linear programme solution is fractional and has a better objective value than the incumbent. Further branching from this node is necessary to ensure an optimal solution is found.</li></ul>

Only the last condition requires more branching, all the other conditions result in the node becoming fathomed and no more branching is required from that node.<br>
Example<br>
<br>
<img src='http://pulp-or.googlecode.com/svn/wiki/bandb.jpg' />

<h3>The LP Relaxation</h3>
The Linear Programming (LP) relaxation is the same as the integer programme, except we "relax" the integer variables to allow them to take fractional values. The integer programme's feasible region lies within the feasible region of the LP relaxation (at points where the integer variables have integer values). Therefore the integer restrictions cause the optimal objective function value to be worse in the integer programme as compared to the LP relaxation. However, if a solution x of the LP relaxation has integer values for the integer variables, then x also solves the integer programme. In some cases, if the solution values for the integer variables are large, then rounding the LP relaxation solution may give a good solution to the integer programme. However, you need to make sure that the rounded solution is not infeasible! For some classes of problem the LP relaxation gives naturally integer solutions:<br>
<br>
<ul><li>An mxm matrix M is unimodular if and only if its determinant |M| is equal to 1 or –1;<br>
</li><li>An mxn matrix A is totally unimodular if and only if every mxm non-singular submatrix of A is unimodular;<br>
</li><li>If the constraint matrix A and the right-hand side vector b of a mixed-integer programme are totally unimodular and integer respectively, then the mixed-integer programme is naturally integer and the LP relaxation solution is the optimal solution<br>
<ul><li>The transportation problem is an example of one such problem;<br>
</li><li>Most network flow problems are also naturally integer;<br>
</li><li>Some scheduling problems are naturally integer.</li></ul></li></ul>

When using PuLP, naturally integer variables are defined when the variables are created with the LpVariable function. A parameter for this function is either LpContinuous or LpInteger.<br>
<br>
<h3>Master-Slave Constraints</h3>

Using zero/one variables, we can control the range of values that other variables take. Suppose that x<i>{AB} (the amount shipped from A to B) is either 0 (we don't ship from A to B) or between 20 and 100 (we ship from A to B with limits specified by the transportation company). We introduce a new 0/1-variable Z</i>{AB} that is 1 if there is a shipment from A to B and 0 otherwise. Then we can use a master-slave constraints to let Z<i>{AB} control X</i>{AB}<br>
<br>
X<i>{AB} >= 20Z</i>{AB}<br>
X<i>{AB} <= 100Z</i>{AB}<br>
<br>
<h2>Sensitivity Analysis</h2>
In STATS/ENGSCI 255 you will have seen the following sensitivity analysis output from Excel and/or Storm.<br>
<br>
<img src='http://pulp-or.googlecode.com/svn/wiki/sensitivity_excel.jpg' />
<img src='http://pulp-or.googlecode.com/svn/wiki/sensitivity_storm.jpg' />

What do these numbers mean? First, let's look at the Excel sensitivity analysis. For the variables, the Allowable Increase and Allowable Decrease show how much the objective coefficient of that variable can change without changing the optimal solution (although the objective function will change!). For the constraints the Allowable Increase and Allowable Decrease show how much the right-hand side of the constraint (i.e., the part of the constraint that does not involve variables) can increase or decrease without changing which variables are non-zero (although the variable values will change!). The shadow price gives the amount the objective function changes for each unit change in the right-hand side. If the constraint gets tighter then the objective function will deteriorate. The following table gives the various combinations for constraints and objective functions:<br>
<table><thead><th>Constraint  Relation</th><th>Change in Constraint RHS</th><th>Objective Type</th><th>Change in Objective Function</th></thead><tbody>
<tr><td> >= 	</td><td>	 +(harder) 	</td><td>	Maximise 	</td><td>	- (worse) 	</td></tr>
<tr><td> >= 	</td><td>	 -(easier) 	</td><td>	Maximise 	</td><td>	+ (better) 	</td></tr>
<tr><td> <= 	</td><td>	 -(harder) 	</td><td>	Maximise 	</td><td>	- (worse) 	</td></tr>
<tr><td> <= 	</td><td>	 +(easier) 	</td><td>	Maximise 	</td><td>	+ (better) 	</td></tr>
<tr><td> >= 	</td><td>	 +(harder) 	</td><td>	Minimise 	</td><td>	+ (worse) 	</td></tr>
<tr><td> >= 	</td><td>	 -(easier) 	</td><td>	Minimise 	</td><td>	- (better) 	</td></tr>
<tr><td> <= 	</td><td>	 -(harder) 	</td><td>	Minimise 	</td><td>	+ (worse) 	</td></tr>
<tr><td> <= 	</td><td>	 +(easier) 	</td><td>	Minimise 	</td><td>	- (better) 	</td></tr></tbody></table>

The Storm sensitivity analysis provides the same information, but gives the Allowable Minimum and the Allowable Maximum instead. Note that the Allowable Minimum = Current Value - Allowable Decrease and the Allowable Maximum = Current Value + Allowable Increase.<br>
<br>
<h2>Parametric Analysis</h2>
In STATS/ENGSCI 255 you will have seen the following parametric analysis:<br>
<br>
<img src='http://pulp-or.googlecode.com/svn/wiki/parametric_storm.jpg' />


This analysis shows how the objective and shadow price change as a right-hand side value increases (from 230 to 500, then 500 upwards. It also shows how the objective and shadow price change as the right-hand side value decreases (from 230 to 140, 140 to 120, 120 to 0, then 0 downwards). Similar tables are also available in STORM for changes in the cost coefficients. These tables assume that only one quantity (right-hand side, cost) is changing.