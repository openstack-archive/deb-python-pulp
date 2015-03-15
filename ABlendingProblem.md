# The Whiskas Problem #

## Problem Description ##

![http://pulp-or.googlecode.com/svn/wiki/whiskas_label.jpg](http://pulp-or.googlecode.com/svn/wiki/whiskas_label.jpg)

Whiskas cat food, shown above, is manufactured by Uncle Ben’s. Uncle Ben’s want to produce their cat food products as cheaply as possible while ensuring they meet the stated nutritional analysis requirements shown on the cans. Thus they want to vary the quantities of each ingredient used (the main ingredients being chicken, beef, mutton, rice, wheat and gel) while still meeting their nutritional standards.

![http://pulp-or.googlecode.com/svn/wiki/whiskas_blend.jpg](http://pulp-or.googlecode.com/svn/wiki/whiskas_blend.jpg)

The costs of the chicken, beef, and mutton are $0.013, $0.008 and $0.010 respectively, while the costs of the rice, wheat and gel are $0.002, $0.005 and $0.001 respectively. (All costs are per gram.) For this exercise we will ignore the vitamin and mineral ingredients. (Any costs for these are likely to be very small anyway.)

Each ingredient contributes to the total weight of protein, fat, fibre and salt in the final product. The contributions (in grams) per gram of ingredient are given in the table below.

|    | Protein | Fat | Fibre | Salt |
|:---|:--------|:----|:------|:-----|
|Chicken |0.100 |0.080 |0.001 |0.002|
|Beef |0.200 |0.100 |0.005 |0.005|
|Mutton |0.150 |0.110 |0.003 |0.007|
|Rice |0.000 |0.010 |0.100 |0.002|
|Wheat bran |0.040 |0.010 |0.150 |0.008|
|Gel |- |- |- |- |

## Simplified Formulation ##

First we will consider a simplified problem to build a simple Python model.
  1. Identify the Decision Variables
> > Assume Whiskas want to make their cat food out of just two ingredients: Chicken and Beef. We will first define our decision variables:
      * x<sub>1</sub> =  percentage of chicken meat in a can of cat food
      * x<sub>2</sub> = percentage of beef used in a can of cat food
> > > The limitations on these variables (greater than zero) must be noted but for the Python implementation, they are not entered or listed separately or with the other constraints.
  1. Formulate the Objective Function

> > The objective function becomes:
> > min $0.013 x<sub>1</sub> + $0.008 x<sub>2</sub>
  1. Formulate the Constraints
> > The constraints on the variables are that they must sum to 100 and that the nutritional requirements are met:
    * 1.000 x<sub>1</sub>  + 1.000 x<sub>2</sub> == 100.0
    * 0.100 x<sub>1</sub>  + 0.200 x<sub>2</sub> >= 8.0
    * 0.080 x<sub>1</sub>  + 0.100 x<sub>2</sub> >= 6.0
    * 0.001 x<sub>1</sub>  + 0.005 x<sub>2</sub> <= 2.0
    * 0.002 x<sub>1</sub>  + 0.005 x<sub>2</sub> <= 0.4

### Solution to Simplified Problem ###

To obtain the solution to this Linear Program, we can write a short program in Python to call PuLP's modelling functions, which will then call a solver. This will explain step-by-step how to write this Python program. It is suggested that you repeat the exercise yourself. The code for this example is found in http://pulp-or.googlecode.com/svn/trunk/pulp-or/examples/WhiskasModel1.py

The start of the your file should then be headed with a short commenting section outlining the purpose of the program. For example:


```
"""
The Simplified Whiskas Model Python Formulation for the PuLP Modeller

Authors: Antony Phillips, Dr Stuart Mitchell    2007
"""
```

Then you will import PuLP's functions for use in your code:<br>

<pre><code># Import PuLP modeler functions<br>
from pulp import *<br>
</code></pre>

A variable called <code>prob</code> (although its name is not important) is created using the <code>LpProblem</code> function. It has two parameters, the first being the arbitrary name of this problem (as a string), and the second parameter being either <code>LpMinimize</code> or <code>LpMaximize</code> depending on the type of LP you are trying to solve:<br>
<br>
<pre><code># Create the 'prob' variable to contain the problem data<br>
prob = LpProblem("The Whiskas Problem",LpMinimize)<br>
</code></pre>

The problem variables <code>x1</code> and <code>x2</code> are created using the <code>LpVariable</code> function. It has four parameters, the first is the arbitrary name of what this variable represents, the second is the lower bound on this variable, the third is the upper bound, and the fourth is essentially the type of data (discrete or continuous). The options for the fourth parameter are <code>LpContinuous</code> or <code>LpInteger</code>, with the default as <code>LpContinuous</code>. If we were modelling the number of cans to produce, we would need to input <code>LpInteger</code> since it is discrete data. The bounds can be entered directly as a number, or <code>None</code> to represent no bound (i.e. positive or negative infinity), with <code>None</code> as the default. If the first few parameters are entered and the rest are ignored (as shown), they take their default values. However, if you wish to specify the third parameter, but you want the second to be the default value, you will need to specifically set the second parameter as it's default value. i.e you cannot leave a parameter entry blank. (e.g <code>LpVariable("example",None,100)</code>)<br>
<br>
<pre><code># The 2 variables Beef and Chicken are created with a lower limit of zero<br>
x1 = LpVariable("ChickenPercent",0)<br>
x2 = LpVariable("BeefPercent",0)<br>
</code></pre>

The variable <code>prob</code> now begins collecting problem data with the <code>+=</code> operator. The objective function is logically entered first, with an important comma <code>,</code> at the end of the statement and a short string explaining what this objective function is:<br>
<br>
<pre><code># The objective function is added to 'prob' first<br>
prob += 0.013 * x1 + 0.008 * x2, "Total Cost of Ingredients per can"<br>
</code></pre>

The constraints are now entered (Note: any "non-negative" constraints were already included when defining the variables). This is done with the '+=' operator again, since we are adding more data to the <code>prob</code> variable. The constraint is logically entered after this, with a comma at the end of the constraint equation and a brief description of the cause of that constraint:<br>
<br>
<pre><code># The five constraints are entered<br>
prob += x1 + x2 == 100, "PercentagesSum"<br>
prob += 0.100 * x1 + 0.200 * x2 &gt;= 8.0, "ProteinRequirement"<br>
prob += 0.080 * x1 + 0.100 * x2 &gt;= 6.0, "FatRequirement"<br>
prob += 0.001 * x1 + 0.005 * x2 &lt;= 2.0, "FibreRequirement"<br>
prob += 0.002 * x1 + 0.005 * x2 &lt;= 0.4, "SaltRequirement"<br>
</code></pre>

Now that all the problem data is entered, the <code>writeLP</code> function can be used to copy this information into a .lp file into the directory that your code is running from. Once your code runs successfully, you can open this .lp file with Notepad to see what the above steps were doing. You will notice that there is no assignment operator (such as an equals sign) on this line. This is because the function/method called <code>writeLP</code> is being performed to the variable/object <code>prob</code> (and the string <code>"WhiskasModel.lp"</code> is an additional parameter). The dot <code>.</code> between the variable/object and the function/method is important and is seen frequently in Object Oriented software (such as this):<br>
<br>
<pre><code># The problem data is written to a .lp file<br>
prob.writeLP("WhiskasModel.lp")<br>
</code></pre>

The LP is solved using the solver that PuLP chooses. The input brackets after <code>solve</code> are left empty in this case, however they can be used to specify which solver to use (e.g  <code>prob.solve(CPLEX())</code> ):<br>
<br>
<pre><code># The problem is solved using PuLP's choice of solver<br>
prob.solve()<br>
</code></pre>

Now the results of the solver call can be displayed as output to us. Firstly, we request the status of the solution, which can be one of "Not Solved", "Infeasible", "Unbounded", "Undefined" or "Optimal". The value of prob.status is returned as an integer, which must be converted to it's significant text meaning using the <code>LpStatus</code> dictionary. Since <code>LpStatus</code> is a dictionary, it's input must be in square brackets:<br>
<br>
<pre><code># The status of the solution is printed to the screen<br>
print "Status:", LpStatus[prob.status]<br>
</code></pre>

The variables and their resolved optimum values can now be printed to the screen. The <code>for</code> loop makes <code>variable</code> cycle through all the problem variable names (in this case just <code>ChickenPercent</code> and <code>BeefPercent</code>). Then it prints each variable name, followed by an equals sign, followed by its optimum value. <code>.name</code> and <code>.varValue</code> are properties of the object <code>variable</code>.<br>
<br>
<pre><code>for variable in prob.variables():<br>
    print variable.name, "=", variable.varValue<br>
</code></pre>

The optimised objective function value is printed to the screen, using the value function. This ensures that the number is in the right format to be displayed. <code>.objective</code> is an attribute of the object <code>prob</code>:<br>
<br>
<pre><code># The optimised objective function value is printed to the screen<br>
print "Total Cost of Ingredients per can = ", value(prob.objective)<br>
</code></pre>

Running this file should then produce the output to show that Chicken will make up 33.33%, Beef will make up 66.67% and the Total cost of ingredients per can is 96 cents.<br>
<br>
<br>
The segmented .py file shown above can be obtained in full <a href='http://130.216.209.237/engsci392/pulp/WhiskasModel1.py'> here </a>. Opening the file normally will run it, which will execute the commands and exit in less than 1 second. You will need to open this file with IDLE or PyDev to run it and view the output properly.<br>
<br>
<h2>Full Formulation</h2>
Now we will formulate the problem fully with all the variables. Whilst it could be implemented into Python with little addition to our method above, we will look at a better way which does not mix the problem data, and the formulation as much. This will make it easier to change any problem data for other tests. We will start the same way by algebraically defining the problem:<br>
<br>
<ol><li>Identify the Decision Variables<br>
<blockquote>For the Whiskas Cat Food Problem the decision variables are the percentages of the different ingredients we include in the can. Since the can is 100g, these percentages also represent the amount in g of each ingredient included. In STATS 255, the decisions were the amount in g in each cat food, but it is more convenient to use percentages.<br>
We must formally define our decision variables, being sure to state the units we are using.<br>
<ul><li>x<sub>1</sub> = percentage of chicken meat in a can of cat food<br>
</li><li>x<sub>2</sub> = percentage of beef used in a can of cat food<br>
</li><li>x<sub>3</sub> = percentage of mutton used in a can of cat food<br>
</li><li>x<sub>4</sub> = percentage of rice used in a can of cat food<br>
</li><li>x<sub>5</sub> = percentage of wheat bran used in a can of cat food<br>
</li><li>x<sub>6</sub> = percentage of gel used in a can of cat foo}<br>
</li></ul>Note that these percentages must be between 0 and 100.<br>
</blockquote></li><li>Formulate the Objective Function<br>
<blockquote>For the Whiskas Cat Food Problem the objective is to minimise the total cost of ingredients per can of cat food.<br>
We know the cost per g of each ingredient. We decide the percentage of each ingredient in the can, so we must divide by 100 and multiply by the weight of the can in g. This will give us the weight in g of each ingredient.</blockquote></li></ol>

<blockquote>min $0.013 x<sub>1</sub> + $0.008 x<sub>2</sub> + $0.010 x<sub>3</sub> + $0.002 x<sub>4</sub> + $0.005 x<sub>5</sub> + $0.001 x<sub>6</sub></blockquote>

<ol><li>Formulate the Constraints<br>
<blockquote>The constraints for the Whiskas Cat Food Problem are that:<br>
</blockquote><ul><li>The sum of the percentages must make up the whole can (= 100%).<br>
</li><li>The stated nutritional analysis requirements are met.</li></ul></li></ol>

<blockquote>The constraint for the "whole can" is:</blockquote>

<blockquote>x<sub>1</sub> + x<sub>2</sub> + x<sub>3</sub> + x<sub>4</sub> + x<sub>5</sub> +x <sub>6</sub> = 100</blockquote>

<blockquote>To meet the nutritional analysis requirements, we need to have at least 8g of Protein per 100g, 6g of fat, but no more than 2g of fibre and 0.4g of salt. To formulate these constraints we make use of the previous table of contributions from each ingredient. This allows us to formulate the following constraints on the total contributions of protein, fat, fibre and salt from the ingredients:<br>
</blockquote><ul><li>0.100 x<sub>1</sub> +0.200 x<sub>2</sub> +0.150 x<sub>3</sub> +0.000 x<sub>4</sub> +0.040 x<sub>5</sub> +0.0 x<sub>6</sub> >= 8.0<br>
</li><li>0.080 x<sub>1</sub> +0.100 x<sub>2</sub> +0.110 x<sub>3</sub> +0.010 x<sub>4</sub> +0.010 x<sub>5</sub> +0.0 x<sub>6</sub> >= 6.0<br>
</li><li>0.001 x<sub>1</sub> +0.005 x<sub>2</sub> +0.003 x<sub>3</sub> +0.100 x<sub>4</sub> +0.150 x<sub>5</sub> +0.0 x<sub>6</sub> <= 2.0<br>
</li><li>0.002 x<sub>1</sub> +0.005 x<sub>2</sub> +0.007 x<sub>3</sub> +0.002 x<sub>4</sub> +0.008 x<sub>5</sub> +0.0 x<sub>6</sub> <= 0.4</li></ul>

<ol><li>Identify the Data<br>
<blockquote>We know the total weight of the can. We also know the cost of the ingredients, the nutritional analysis requirements and the contribution (per gram) of each ingredient in terms of the nutritional analysis. This is enough to formulate the necessary mathematical programme, but we will reconsider our data after solving the mathematical programme and performing some post-optimal analyis.</blockquote></li></ol>

<h3>Solution to Full Problem</h3>

To obtain the solution to this Linear Program, we again write a short program in Python to call PuLP's modelling functions, which will then call a solver. This will explain step-by-step how to write this Python program with it's improvement to the above model. It is suggested that you repeat the exercise yourself. The code for this example is found in <a href='http://pulp-or.googlecode.com/svn/trunk/pulp-or/examples/WhiskasModel2.py'>http://pulp-or.googlecode.com/svn/trunk/pulp-or/examples/WhiskasModel2.py</a>

As with last time, it is advisable to head your file with commenting on it's purpose, and the author name and date. Importing of the PuLP functions is also done in the same way:<br>
<br>
<pre><code>"""<br>
The Full Whiskas Model Python Formulation for the PuLP Modeller<br>
<br>
Authors: Antony Phillips, Dr Stuart Mitchell   2007<br>
"""<br>
<br>
# Import PuLP modeler functions<br>
from pulp import *<br>
</code></pre>

Next, before the <code>prob</code> variable or type of problem are defined, the key problem data is entered into dictionaries. This includes the list of Ingredients, followed by the cost of each Ingredient, and it's percentage of each of the four nutrients. These values are clearly laid out and could easily be changed by someone with little knowledge of programming. The ingredients are the reference keys, with the numbers as the data.<br>
<br>
<pre><code># Creates a list of the Ingredients<br>
Ingredients = ["CHICKEN", "BEEF", "MUTTON", "RICE", "WHEAT", "GEL"]<br>
<br>
# A Dictionary of the costs of each of the Ingredients is created<br>
costs = {"CHICKEN": 0.013,<br>
         "BEEF"   : 0.008,<br>
         "MUTTON" : 0.010,<br>
         "RICE"   : 0.002,<br>
         "WHEAT"  : 0.005,<br>
         "GEL"    : 0.001}<br>
<br>
# A dictionary of the protein percent in each of the Ingredients is created<br>
proteinPercent = {"CHICKEN": 0.100,<br>
                  "BEEF"   : 0.200,<br>
                  "MUTTON" : 0.150,<br>
                  "RICE"   : 0.000,<br>
                  "WHEAT"  : 0.040,<br>
                  "GEL"    : 0.000}<br>
<br>
# A dictionary of the fat percent in each of the Ingredients is created<br>
fatPercent = {"CHICKEN": 0.080,<br>
              "BEEF"   : 0.100,<br>
              "MUTTON" : 0.110,<br>
              "RICE"   : 0.010,<br>
              "WHEAT"  : 0.010,<br>
              "GEL"    : 0.000}<br>
<br>
# A dictionary of the fibre percent in each of the Ingredients is created<br>
fibrePercent = {"CHICKEN": 0.001,<br>
                "BEEF"   : 0.005,<br>
                "MUTTON" : 0.003,<br>
                "RICE"   : 0.100,<br>
                "WHEAT"  : 0.150,<br>
                "GEL"    : 0.000}<br>
<br>
# A dictionary of the fibre percent in each of the Ingredients is created<br>
saltPercent = {"CHICKEN": 0.002,<br>
               "BEEF"   : 0.005,<br>
               "MUTTON" : 0.007,<br>
               "RICE"   : 0.002,<br>
               "WHEAT"  : 0.008,<br>
               "GEL"    : 0.000<br>
</code></pre>

The <code>prob</code> variable is created to contain the formulation, and the usual parameters are passed into 'LpProblem'.<br>
<br>
<pre><code># Create the 'prob' variable to contain the problem data<br>
prob = LpProblem("The Whiskas Problem", LpMinimize)<br>
</code></pre>

A <i>dictionary</i> called <code>ingredient_vars</code> is created which contains the LP variables, with their defined lower bound of zero. The reference keys to the dictionary are the Ingredient names, and the data is <code>Ingr_IngredientName</code>. (e.g. MUTTON: Ingr_MUTTON)<br>
<br>
<pre><code># A dictionary called 'ingredient_vars' is created to contain the referenced variables<br>
ingredient_vars = LpVariable.dicts("Ingr",Ingredients,0)<br>
</code></pre>

Since <code>costs</code> and <code>ingredient_vars</code> are now dictionaries with the reference keys as the Ingredient names, the data can be simply extracted with a list comprehension as shown. The <code>lpSum</code> function will add the elements of the resulting list. Thus the objective function is simply entered and assigned a name:<br>
<br>
<pre><code># The objective function is added to 'prob' first<br>
prob += lpSum([costs[i] * ingredient_vars[i] for i in Ingredients]), "Total Cost of Ingredients per can"<br>
</code></pre>

Further list comprehensions are used to define the other 5 constraints, which are also each given names describing them.<br>
<br>
<pre><code># The five constraints are added to 'prob'<br>
prob += lpSum([ingredient_vars[i] for i in Ingredients]) == 100, "PercentagesSum"<br>
prob += lpSum([proteinPercent[i] * ingredient_vars[i] for i in Ingredients]) &gt;= 8.0 "ProteinRequirement"<br>
prob += lpSum([fatPercent[i] * ingredient_vars[i] for i in Ingredients]) &gt;= 6.0 "FatRequirement"<br>
prob += lpSum([fibrePercent[i] * ingredient_vars[i] for i in Ingredients]) &lt;= 2.0, "FibreRequirement"<br>
prob += lpSum([saltPercent[i] * ingredient_vars[i] for i in Ingredients &lt;= 0.4, "Salt Requirement"<br>
</code></pre>

Following this, the prob.writeLP line etc follow exactly the same as in the simplified example. To see the entire file, it is available<a href='http://130.216.209.237/engsci392/pulp/WhiskasModel2.py'> here </a>.<br>
<br>
The optimal solution is 60% Beef and 40% Gel leading to a Objective Function value of 52 cents per can.<br>
<br>
<h2>Post-Optimal Analysis</h2>

For The Whiskas Cat Food Problem we will not perform any post-optimal analysis. However, as you will remember from STATS255, a Sensitivity Analysis and a Parametric Analysis can be performed.<br>
<br>
<ol><li>Validation<br>
<blockquote>To validate our solution for The Whiskas Cat Food Problem, we can do a quick check that our solution makes sense. First, the percentages should add up to 100%. If not, there is something wrong. Next, we can do a quick check of the constraints to ensure none of them are violated.</blockquote></li></ol>

<ul><li>Note For large models you won't always be able to check the solution by hand.</li></ul>

<blockquote>The final validation is to write up a management summary for your manager and/or client and see if they think our solution is a valid one. If they identify some (or all) of the solution that is not valid, then you should discuss with them the reasons why it is invalid and start a "feedback" loop in your optimisation process.</blockquote>

<h2>Presentation of Solution and Analysis</h2>

The solution for The Whiskas Cat Food Problem is a simple one to summarise. Here is an example management summary (with the numbers removed):<br>
<br>
<pre><code>The Whiskas Cat Food Problem<br>
Stuart Mitchell, 2007<br>
<br>
Uncle Ben’s want to produce their cat food products as cheaply as possible while ensuring<br>
they meet the stated nutritional analysis requirements shown on the cans. Thus they want<br>
to vary the quantities of each ingredient used (the main ingredients being chicken,<br>
beef, mutton, rice, wheat and gel) while still meeting their nutritional standards.<br>
<br>
The stated nutritional analysis requirements are: _______<br>
The cost for each ingredient is: _______<br>
<br>
To minimise the cost per 100g can of Whiskas cat food, Whiskas should use<br>
_______ g of Chicken,<br>
_______ g of Beef,<br>
<br>
The cost per can is _______<br>
</code></pre>

IMPORTANT When presenting your solution you must be careful about the number of decimal places you use. You should not use a greater accuracy than your data allows.<br>
<br>
<h2>Implementation and Ongoing Monitoring</h2>
The first step towards Implementation is a good management summary. You may also want to discuss any issues that may arise from the solution you have found with Uncle Ben's (for example, if you solution can be implemented on their production line).<br>
<br>
Ongoing Monitoring may take the form of:<br>
<ul><li>Updating your data files and resolving as the data changes (changing costs, nutritional requirements, etc);<br>
</li><li>Resolving our model for new products (e.g., 200g cans);<br>
</li><li>Looking for possible savings (e.g., analysing the cost of the ingredients to see if any price changes will affect the ingredient mix).