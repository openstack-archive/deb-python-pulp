# The Coke Production Problem #

---

## Adapted from a real-world problem ##

---

  1. [The problem description](http://130.216.209.237/engsci392/pulp/CokeProduction#description)

> 2. [Tasks](http://130.216.209.237/engsci392/pulp/CokeProduction#tasksStudent)


## Problem Description ##

---

Over 29% of world’s coke is made in China. Recently market liberalization has lead to town and village enterprises, with uncertainty in future markets resulting in short-sighted resource use. There are currently many small cokemaking plants with relatively primitive technology. This has resulted in an industry with low transportation costs (as coke is supplied by many small local producers) but high pollution and energy use.


![http://pulp-or.googlecode.com/svn/wiki/800px-Koks_Brennstoff.jpg](http://pulp-or.googlecode.com/svn/wiki/800px-Koks_Brennstoff.jpg)


The government wants to move cokemaking to Shanxi, where they can establish bigger facilities. This plan will be more efficient, with less pollution, but will also result in higher transport costs (calculated from a GIS database). The plants in Shanxi will be built with one or more oven batteries, each making 75,000 tonnes of coke a year. The process these plants will use to convert coal to coke is "thermal decomposition". **This process results in 1 tonne of coke produced for every 1.3 tonnes of coal processed**.

The (simplified) problem we will model has the following details:


  1. There are six coal mines, each able to supply up to a certain amount of coal each year to the plants for processing

> 2.There are six customers, each with a certain demand for coke each year

> 3.There are six possible plant locations, each able to process a certain amount of coke each year

![http://pulp-or.googlecode.com/svn/wiki/coke_map.jpg](http://pulp-or.googlecode.com/svn/wiki/coke_map.jpg)


Each plant has 6 possible sizes, with coke processing levels and associated construction costs shown below:

| **Size (kT/yr)** | **Cost (MRMB)** |
|:-----------------|:----------------|
|75 | 4.4 |
|150 | 7.4 |
|225 | 10.5 |
|300 | 13.5 |
|375 | 16.5 |
|450 | 19.6 |


Each Mine has the following coal supply per year:

| **Mine** | 1 | 2 | 3 | 4 | 5 | 6 |
|:---------|:--|:--|:--|:--|:--|:--|
| **Coal Supply (kT/yr)** | 25.8 | 728 | 1456 | 40 | 36.9 | 1100 |


Each Customer has the following coke demand per year:

| **Customer** | 1 | 2 | 3 | 4 | 5 | 6 |
|:-------------|:--|:--|:--|:--|:--|:--|
| **Coke Demand (kT/yr)** | 83 | 5.5 | 6.975 | 5.5 | 720.75 | 5.5 |


The transportation costs (RMB/kT) between the mines and the plants are as follows:

| RMB/kT|  Plant 1|  Plant 2|  Plant 3|  Plant 4|  Plant 5|  Plant 6|
|:------|:--------|:--------|:--------|:--------|:--------|:--------|
|Mine 1 | 231737 | 46813 | 79337|  195845 | 103445 | 45186 |
|Mine 2 | 179622 | 267996 | 117602 | 200298|  128184 | 49046 |
|Mine 3|  45170 | 93159  |156241 | 218655|  103802|  119616 |
|Mine 4 | 149925 | 254305 | 76423 | 123534|  151784 | 104081 |
|Mine 5 | 152301 | 205126 | 24321 | 66187 | 195559 | 88979 |
|Mine 6 | 223934 | 132391 | 51004 | 122329 | 222927 | 54357 |


The transportation costs (RMB/kT) between the plants and the customers are as follows:

|RMB/kT|  Plant 1 | Plant 2 | Plant 3|  Plant 4 | Plant 5 | Plant 6|
|:-----|:---------|:--------|:-------|:---------|:--------|:-------|
|Customer 1 | 6736  |42658 | 70414 | 45170  |184679 | 111569  |
|Customer 2 | 217266 | 227190|  249640|  203029 | 153531 | 117487 |
|Customer 3 | 35936 | 28768 | 126316 | 2498|  130317 | 74034 |
|Customer 4 | 73446 | 52077 | 108368 | 75011|  49827|  62850|
|Customer 5  |174664 | 177461 | 151589 | 153300 | 59916|  135162 |
|Customer 6 | 186302|  189099|  147026 | 164938  |149836 | 286307 |


## Student Tasks ##

---

Write a Python file to solve the Coke production Problem. What to hand in Your 3 AMPL files. Your management summary.