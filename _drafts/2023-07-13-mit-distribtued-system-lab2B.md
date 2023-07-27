---
layout: post
title: "Self-Study: MIT, Distributed System - 6.824/6.5840 Lab 2A (Raft - Leader Election) "
tags: [ "self-study","Distributed System","MIT","6.824/6.5840", "English" ]
categories: ["self-study","Distributed System","MIT", "6.824/6.5840"]
toc: true
---
# Overview

MIT 6.5840, formerly known as 6.824, is a graduate-level course at the Massachusetts Institute of Technology (MIT) that covers distributed systems. The course presents abstractions and implementation techniques for engineering distributed systems, with major topics including fault tolerance, replication, and consistency. The course also includes several programming labs that give students hands-on experience with building distributed systems.

The labs for the course are using [GO lang](https://go.dev/) and as follows:

Lab 1 - [My Lab Report](https://potatochick2020.github.io/posts/mit-distributed-system-lab1): MapReduce - In this lab, students implement a MapReduce system, which is a programming model for processing large data sets in parallel.

Lab 2 - [2A: My Lab Report](https://potatochick2020.github.io/posts/mit-distributed-system-lab2A): Raft - In this lab, students implement the Raft consensus algorithm, which is used to ensure that multiple servers in a distributed system agree on the same values.

Lab 3: Key-Value storage based on Raft - In this lab, students build a fault-tolerant key-value storage system using the Raft algorithm implemented in Lab 2.

Lab 4: Sharded Key-Value storage - In this lab, students extend their key-value storage system from Lab 3 to support sharding, which allows the system to scale horizontally by partitioning data across multiple servers.

These labs provide students with practical experience in implementing distributed systems and help them understand the challenges and trade-offs involved in building such systems.

# LAB 2: Raft
Raft is a protocol that accept N/2 Failure in each cluster. For example, in a Raft cluster that formed by 7 machine, it could accpet 3 machine dies due to network failure/ some one unplug the power/ windows choose to update suddently/ earthquale or whatever. 

This lab are quite strict forward just read the [raft paper](https://pdos.csail.mit.edu/6.824/papers/raft-extended.pdf) carefully, and implement it step by step then most likely it will works well. 

MIT has seperate the implementation of raft into 4 part,
- LAB 2A: Leader Election
- LAB 2B: Log
- LAB 2C: Persistence
- LAB 2D: Log compaction

Some material that I found useful in understanding
[Student guide to raft](https://thesquareplanet.com/blog/students-guide-to-raft/)    
[Instrutors guide to raft](https://thesquareplanet.com/blog/instructors-guide-to-raft/)    
[Raft Visualization](http://thesecretlivesofdata.com/raft/#election)    
[Extended Raft Paper (Mostly refer to Figure 2)](https://pdos.csail.mit.edu/6.824/papers/raft-extended.pdf)

# LAB 2B: Raft - (Leader Election)

## Introduction

It is easier to watch a [visalization](https://thesecretlivesofdata.com/raft/#replication) than typing words. 

## Thinking Process

### Read the academic paper
 
![Figure 2: A condensed summary of the Raft consensus algorithm (excluding membership changes and log compaction). The server
behavior in the upper-left box is described as a set of rules that trigger independently and repeatedly](/assets/img/self-study/6.5840/raft-figure2.PNG)
This is basically what we need to implement in the coming lab

### Read the Raft 6.5840/6.824 architecture

This lab includes some part of the architecture which does not include in the paper as thats belong to 6.5840 Lab implementation such as the ApplyCh and ApplyMSG. It will be easier for you to understand by reading the [Raft Diagram](https://pdos.csail.mit.edu/6.824/notes/raft_diagram.pdf)

### Cut tasks into small pieces

This part of the lab was more difficult than the previous ones, and I felt overwhelmed and unsure how to begin. I eventually decided to start by trying to pass the first test case.

The first message is to reach log agreement, it simply call start() until there is a leader and the leader return success for start().
This narrow the code segment to edit to 

1. Start()
2. AppendEntriesRPC handler

```bash
--- FAIL: TestBasicAgree2B (7.17s)
    config.go:594: one(100) failed to reach agreement
```