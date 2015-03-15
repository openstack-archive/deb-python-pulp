# The Data Flow Problem #

---

## Adapted from a real-world problem ##

## Problem Description ##

---

Many large companies are starting to centralise their data storage. Centralised data storage allows for increased efficiency of data storage resources, security of the data and reliability of the storage system. Storage Area Networks ("SANs?") are a popular way to provide centralised storage. SANs? connect servers and/or client machines (known as hosts) to the centralised data storage devices using a network of links (ethernet, fibre channel and/or SCSI cables), hubs and switches.

The problem facing network/storage engineers is how to build a cost-efficient, reliable SAN.

To answer this question, we must first consider the different components of this example SAN:

![http://pulp-or.googlecode.com/svn/wiki/san.jpg](http://pulp-or.googlecode.com/svn/wiki/san.jpg)



### Hosts ###

The hosts are web servers, application servers, client machines, etc. They have a number of port slots for network interface cards (NICs?). Each slot has a specified port bandwidth capacity and a port cost (the cost of the NIC to put in the port slot).

![http://pulp-or.googlecode.com/svn/wiki/san_hosts.jpg](http://pulp-or.googlecode.com/svn/wiki/san_hosts.jpg)


### Devices ###

The (storage) devices are disks, disk arrays, tape drives, etc. They have the same attributes as hosts, namely a number of port slots, port bandwidth capacity and port cost.

![http://pulp-or.googlecode.com/svn/wiki/san_devices.jpg](http://pulp-or.googlecode.com/svn/wiki/san_devices.jpg)


### Hubs ###

Hubs are one type of aggregation point in a network. They can connect several other components (hosts, devices, switches). However, hubs are essentially loops and any flow going into a hub must visit _all the links and ports connected to the hub_ before leaving to its destination.

![http://pulp-or.googlecode.com/svn/wiki/san_hub_loop.jpg](http://pulp-or.googlecode.com/svn/wiki/san_hub_loop.jpg)


This means that the overall hub bandwidth is restricted by the connections made to the hub (that is, the overall hub bandwidth is less than or equal to the minimum of the link bandwidths connected to it). Hubs have a number of port slots, a cost and an overall bandwidth capacity. Hubs come with their port slots preconfigured, i.e., no NIC cards need to be purchased, and the port bandwidth capacity is the same as the overall capacity (for the reason specified earlier).

![http://pulp-or.googlecode.com/svn/wiki/san_hubs.jpg](http://pulp-or.googlecode.com/svn/wiki/san_hubs.jpg)



### Switches ###

Switches are the other type of aggregation point in a network. Unlike hubs, switches route data intelligently, so each port operates inependently. Switches have a number of port slots without NICs?, so there is also a port cost for purchasing a NIC. Since the ports operate independently, their port slots have a port bandwidth capacity. There is also the cost of the entire switch to take into account.

![http://pulp-or.googlecode.com/svn/wiki/san_switches.jpg](http://pulp-or.googlecode.com/svn/wiki/san_switches.jpg)


### Links ###

Finally, links are simply cables that connect one port (or NIC in a port slot) to another. They are typically ethernet, fibre channel or SCSI. Links have a cost and a bandwidth capacity.

![http://pulp-or.googlecode.com/svn/wiki/san_links.jpg](http://pulp-or.googlecode.com/svn/wiki/san_links.jpg)


### Maximising Throughput ###

A storage networking consultant has been provided with the following network diagram, with the bandwidth capacities shown. This network already exists, so all costs are zero.

![http://pulp-or.googlecode.com/svn/wiki/san_problem.jpg](http://pulp-or.googlecode.com/svn/wiki/san_problem.jpg)


His client wants to send 110 MB/s of data from each host to the devices. Where should they send the data?

The cost of a link reduces as its bandwidth capacity decreases. What is the lowest bandwidth capacity for the links in the network that will still support the 110 MB/s flow from the hosts?


## Student Tasks ##

---

Write a Python file to solve the Data Network Flows problem. Write a management summary of your solution.