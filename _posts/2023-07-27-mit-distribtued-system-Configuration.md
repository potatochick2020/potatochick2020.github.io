---
layout: post
title: "Self-Study: MIT, Distributed System - 6.824/6.5840 Configuration/Help "
tags: [ "self-study","Distributed System","MIT","6.824/6.5840", "English" ]
categories: ["self-study","Distributed System","MIT", "6.824/6.5840"]
toc: true
---
# Run multiple test
```bash
#!/bin/bash

# check if the arguments are valid
if [ $# -ne 2 ]; then
  echo "Usage: $0 [Times] [2A/2B/2C/2D - Case Insensitive]"
  exit 1
fi

# assign the arguments to variables 
times=$1
test=${2^^}

# loop for the given number of times
for ((i=1; i<=times; i++))
do
  # execute the command and append the output to result.txt
  go test -run $test -race >> result.txt
done
```

By saving this script in a file e.g. test_multiple.sh , you could run ./test_multiple.sh 25 2A to test Lab 2A for 25 times

# Debug Print Log 
In util.go, it provide a simple helper function for DPrintf(), so we could enable it by controlling const Debug. It also print the timestamp which reduce the debugging effort.

![ShowTimeLog](/assets/img/self-study/6.5840/DebugLog.PNG)

I had change util.go so I could select the log that I actually need for ease of debugging. 

```go
package raft

import "log"

// Debugging
const Debug2A = true
const Debug2B = false
const Debug2C = false
const Debug2D = false

func DPrintf2A(format string, a ...interface{}) (n int, err error) {
	if Debug2A {
		log.Printf(format, a...)
	}
	return
}

func DPrintf2B(format string, a ...interface{}) (n int, err error) {
	if Debug2B {
		log.Printf(format, a...)
	}
	return
}

func DPrintf2C(format string, a ...interface{}) (n int, err error) {
	if Debug2C {
		log.Printf(format, a...)
	}
	return
}

func DPrintf2D(format string, a ...interface{}) (n int, err error) {
	if Debug2D {
		log.Printf(format, a...)
	}
	return
}
```

# Deadlock Detection
In normal case, we use `sync.Mutex` as mutex, but we could use `deadlock.Mutex` as mutex to detect deadlock. This is developed by sasha-s and [here](https://github.com/sasha-s/go-deadlock) is the repository.
