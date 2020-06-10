---
layout: post
title: Load Balancing
date: 2020-06-09 14:14 -0500
category: personal
tags: fun
---

# Basic traits of well-performing application
![Load balancing](/images/loadbalance0.png)

An application is well-performing is relevant to network calling and I/O processing including persistent database or files. Specifically, we would like to minimize network calls, and requests to server are small and as fast as possible. Resource processing is run asynchronously in the background, not occupy web workers. More concurrent users access application, the application has capacity to serve them well.

Besides concurrent access, we also would like to optimize CPU vs. RAM, we think about scaling.

![Type of load balancing](/images/loadbalance1.png)

We have to scaling direction. First, vertical scaling simply increase resources on a single server. This means adding hardware like more RAM, or faster CPU. Secondly, horizontal scaling, a device standing in front of group of hosts, and coordinating traffic among them.
The horizontal scaling has more advantage than the vertical. It can be cheaper on the aspects of capacity, but more expensive to build and provision machines. The second, it can provide fault tolerance, it means if a single web host has hardware problem, we always have alternative for replacement. Therefore, there’s no downtime because horizontal scaling, we could opt in or opt out by increasing or decreasing capacity easily and on demand

Once we are architecture application, always figure out how to separate application into many tiers, now is micro service. We try to avoid install persistent database together with application or build a new host with its own database, the point is that  distribute workload with multiple copies of application server and load balancing (like ELB in AWS), all application servers are replicated and point to the same database, so you might end up with a diamond shape architecture. Of course, for multi-tier model, it allows to scale each layer independently.

![](/images/loadbalance2.png)
Issue concerns about how to store the information of personal user session like shopping cart, profile picture on local file. The load balance r is smart enough to route specific user to node server.
Some solutions are database or cookies stores, cloud-based storage like S3, Elastic File System (EFS) (automatically scale and mount by multiple instances to let application server can share volume.
