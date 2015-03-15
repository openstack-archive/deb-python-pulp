# The Air Crew Rostering Problem #

---

## Adapted from a real-world problem ##

---


1. [The problem description](http://130.216.209.237/engsci392/pulp/AirCrewRostering#description)

2. [Student Tasks](http://130.216.209.237/engsci392/pulp/AirCrewRostering#tasks)


## Problem Description ##

---

An airline is trying to roster captains for 6 flights. The flight schedules are:

![http://pulp-or.googlecode.com/svn/wiki/flights.jpg](http://pulp-or.googlecode.com/svn/wiki/flights.jpg)


Only one captain is required for each sector, but a captain may be a passenger on a flight (this is called paxing). In addition to the six flights above the following flights are available for paxing and operate every 2 hours:

![http://pulp-or.googlecode.com/svn/wiki/recurring_flights.jpg](http://pulp-or.googlecode.com/svn/wiki/recurring_flights.jpg)


The following rules for shifts must be observed:

  * Shifts start and finish at a captain’s home base;
  * The earliest start time is on Day 1 (0001 hours) and the latest finish time is on Day 6 (2359 hours);
  * Shifts are composed of blocks of work. Each block must be no more than 13 hours;
  * Captains must have at least 12 hours break between blocks. The exception is when a block consists only of paxing flights, then a 9 hour break is all that is needed;
  * There must be a 30 min break between sector changes.

There are 6 captains available for work, 2 based in Auckland (AKL), 1 based in Christchurch (CHCH) and 3 based in Singapore (SNG). Each captain is paid $1000 for each block of work (even if it is only a 45 min pax). Each captain’s contract guarantees he/she will be paid for 3 blocks of work even if they perform less.

The airline is also curious if they can reduce the cost of their roster by using less pilots. As a second deliverable, they have asked you to investigate this option.


## Student Tasks ##

---

1. Add a columnwise formulation for finding a pilot roster.
**What to hand in** Your completed Python file.

2. Design a system/process for generating all possible Tours of Duty (TODs).
**What to hand in** A brief (less than 1 page) description of your system/process. Your Python file.

3. Solve The Air Crew Rostering Problem. Be sure to investigate the possibility of less pilots.
**What to hand in** A management summary of your solution.