---
title: Generic.Client.Profile
hidden: true
tags: [Client Artifact]
---

This artifact collects profiling information about the running
client. This is useful when you notice a high CPU load in the client
and want to know why.

The following options are most useful:

1. Goroutines: This shows the backtraces of all currently running
   goroutines. It will generally show most of the code working in the
   current running set of queries.

2. Heap: This shows all allocations currently in use and where they
   are allocated from. This is useful if the client is taking too
   much memory.

3. Profile: This takes a CPU profile of the running process for the
   number of seconds specified in the Duration parameter. You can
   read profiles using:

```
go tool pprof -callgrind -output=profile.grind profile.bin
kcachegrind profile.grind
```

Note that this really only makes sense when another query is running
at the same time since this artifacts itself will not be doing very
much other than just measuring the state of the process.


```yaml
name: Generic.Client.Profile
description: |
  This artifact collects profiling information about the running
  client. This is useful when you notice a high CPU load in the client
  and want to know why.

  The following options are most useful:

  1. Goroutines: This shows the backtraces of all currently running
     goroutines. It will generally show most of the code working in the
     current running set of queries.

  2. Heap: This shows all allocations currently in use and where they
     are allocated from. This is useful if the client is taking too
     much memory.

  3. Profile: This takes a CPU profile of the running process for the
     number of seconds specified in the Duration parameter. You can
     read profiles using:

  ```
  go tool pprof -callgrind -output=profile.grind profile.bin
  kcachegrind profile.grind
  ```

  Note that this really only makes sense when another query is running
  at the same time since this artifacts itself will not be doing very
  much other than just measuring the state of the process.


parameters:
  - name: Allocs
    description: A sampling of all past memory allocations
    type: bool
  - name: Block
    description: Stack traces that led to blocking on synchronization primitives
    type: bool
  - name: Goroutine
    description: Stack traces of all current goroutines
    type: bool
  - name: Heap
    description: A sampling of memory allocations of live objects
    type: bool
  - name: Mutex
    description: Stack traces of holders of contended mutexes
    type: bool
  - name: Profile
    description: CPU profile
    type: bool
  - name: Trace
    description: CPU trace
    type: bool
  - name: Logs
    description: Get logs
    type: bool
  - name: QueryLogs
    description: Get recent queries logs
    type: bool
  - name: Metrics
    description: Get client metrics
    type: bool
  - name: Verbose
    description: Print more detail
    type: bool
  - name: Duration
    description: Duration of sampling for Profile and Trace.
    default: "30"

sources:
  - query: |
      SELECT Type,
             if(condition=get(field="OSPath"),
                then=upload(name=Type + ".bin", file=OSPath)) AS File,
             get(member="Line") AS Line
      FROM profile(allocs=Allocs, block=Block, goroutine=Goroutine,
                   heap=Heap, mutex=Mutex, profile=Profile, trace=Trace,
                   logs=Logs, queries=QueryLogs, metrics=Metrics,
                   debug=if(condition=Verbose, then=2, else=1),
                   duration=atoi(string=Duration))

```
