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

# LAB 2A: Raft - (Leader Election)

## Introduction

It is easier to watch a [visalization](http://thesecretlivesofdata.com/raft/#election) than typing words. 

## Thinking Process

### Read the academic paper
 
![Figure 2: A condensed summary of the Raft consensus algorithm (excluding membership changes and log compaction). The server
behavior in the upper-left box is described as a set of rules that trigger independently and repeatedly](/assets/img/self-study/6.5840/raft-figure2.PNG)
This is basically what we need to implement in the coming lab

### Handle voting with asynchronous 

As first I try to follow my map reduce implementation to implement something like
```go
for i := 0; i < len(rf.peers); i++ {
		if rf.me == i {
			continue
		}
		requestvote(i);
	}
```

However, this does not works well as it might take some time to return, and this usually will leader to an election time out in other custer and start another election. Therefore we should start another go routine here to make sure that each request vote will start smoothly even the previous one does not return in time.

```go
for i := 0; i < len(rf.peers); i++ {
		if rf.me == i {
			continue
		}
		go func(counter int) { 
			requestvote(counter);
		}(i)
	}
```

### Good use of time package

with go [time package](https://pkg.go.dev/time), we could trigger a timer for electionTimeOut and heartbeatTImeOut with Timer.Reset()

```go
// Function wrappers to return standard and random time.Duration for heartbeat and election time out respectively
func StandardHeartBeat() time.Duration {
	return 150 * time.Millisecond
}

func RamdomizedElection() time.Duration {
	return time.Duration(100 + (rand.Int63()%500)) * time.Millisecond
}

// Ticker Function to store action trigger by Time out 
func (rf *Raft) ticker() {
	for rf.killed() == false {
		select {
		case <-rf.heartbeatTimeOut.C:
			rf.mu.Lock()
			if rf.role == Leader {
				rf.SendHeartbeat() 
				//Reset timeout to be trigger next time
				rf.heartbeatTimeOut.Reset(StandardHeartBeat())
			}
			rf.mu.Unlock()
		case <-rf.electionTimeOut.C: 
			rf.mu.Lock() 
			rf.role = Candidate
			rf.StartElection()
			//Reset timeout to be trigger next time
			rf.electionTimeOut.Reset(RamdomizedElection())
			rf.mu.Unlock()
		}
	}
}

```