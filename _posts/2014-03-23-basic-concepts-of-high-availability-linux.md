---
layout: post
title: "Basic Concepts of High Availability Linux"
date: 2014-03-23 17:07:35 +0100
comments: true
categories: 
---
When considering to build a high availability cluster based on Linux, it's easy to find all kinds of how-to's explaining the basic tooling and configuration. Most of them forget to explain some of the basic concepts of high availability. In this post I'll try to explain them.
<!-- more -->
To build a high availability cluster that consists of a node that services its clients and a (number of) node(s) that can be used to fall back when the original node becomes unavailable you would need:

- A way for the cluster to communicate about its state and configuration, this is called a *cluster messaging layer*.
- A way to automatically manage the resources of the cluster, the *cluster resource manager* (CRM).
- Some kind of middle ware between the resource manager and the actual resources, sometimes called *resource agents*.

### Cluster Messaging Layer
The cluster messaging layer is an application that is used to communicate between the nodes. This communication channel is also used to determine whether the other nodes are still alive. For Linux there are two wide used tools offering a Cluster Messaging Layer: [Heartbeat](http://www.linux-ha.org/wiki/Heartbeat) and [Corosync](http://corosync.github.io/corosync/). To my understanging they were both developed by the same group of developers, but Hearbeat is older and Corosync seems the new way to go.

The cluster messaging layer uses multicast or unicast UDP to communicate between the nodes. Built on top of the cluster messaging layer is the Cluster Resource Manager.

### Cluster Resource Manager
The cluster resource manager (CRM) decides which resource to run where. One of the most used open source Linux CRM's is [Pacemaker](http://clusterlabs.org/wiki/Main_Page). It can be configured to prefer certain locations for certain services, for example: the database should run on the server with the SSD and the application server on the server with the faster CPU. When a node fails, the cluster resource manager can move the services of the failing node to another one. This is a very risky and important decision, it should know for certain that the other node is the one failing, not its own network connection. To help make this decision two concepts are used: Quorum and STONITH.

#### Quorum
"Having quorum" basically means: the majority of the nodes are still reachable and can decide whether a certain action should be taken. In a three node cluster, with node 1 becoming disconnected, the other two nodes can decide to take over services of node 1. If the CRM is configured correctly, node 1 should notice it doesn't have quorum anymore and stop it's primary roles to avoid having, for example, two copies of the database with different changes applied by different clients. As you can understand having Quorum in a two node cluster can only be achieved when both nodes are fully functional. You can define the wanted behaviour when the two node cluster loses quorum: for example, the node could be instructed to try and kill the other node: STONITH.

#### STONITH
Shoot The Other Node In The Head. This is done in order to protect the shared resources by either disabling the node or disallowing it access to the shared storage. It is a way to to make sure the other node can not wreak havoc and corrupt or fork the data. When a node crashes, STONITH can be used to power down the system, for example via a remote power switch or via an API when it's a virtual machine. Shooting the other node in the head is a way to *fence the failing node*.

### Resource Agents
The resource agents are plugins or small shell scripts that are used by the cluster resource manager to determine whether a service is running and can also be used to start or stop a service. For Pacemaker there are a lot of readily available resource agents, so you probably don't need to code one yourself. Because the cluster resource manager should start and stop services, it is always adviced to disable the default Linux bootscripts for your services. This avoids a service being (wrongfully) started on two different nodes. As soon as the node has booted correctly the CRM should launch the service via a resource agent if needed.

### Final advice
I hope this post helps you to better understand the how-to's that can be used to configure a Linux high availability cluster. No matter what techniques you choose, make sure you have a good way to fence failing nodes in your production environment to avoid data corruption and make sure you test all scenarios!
