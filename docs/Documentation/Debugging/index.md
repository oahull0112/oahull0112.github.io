#Debugging Overview

Debugging code can be difficult on a good day, and parallel code introduces additional complications. Thankfully, we have a few tools available on NREL HPC machines to help us debug parallel programs. The intent of this guide is to serve as an overview of the types of information one can obtain with a parallel debugger on a supercomputer, and how this information can be used to solve problems in your code. Ultimately, the various parallel debugging and profiling tools tend to work similarly, providing information about individual task and thread performance, parallel memory usage and stack tracing, task-specific bottlenecks and fail points, and more.

We offer several suites of parallel tools: 

* the [ARM Forge suite](https://developer.arm.com/documentation/101136/latest/) (DDT - debugger)
* the [Intel oneAPI HPC Toolkit]() 
* HPE’s tool suite (Kestrel-only):
	* [Cray Debugger Support Tools (CDST)](https://support.hpe.com/hpesc/public/docDisplay?docId=a00113947en_us&page=Cray_Debugger_Support_Tools_CDST.html), including [gdb4hpc](https://support.hpe.com/hpesc/public/docDisplay?docLocale=en_US&docId=a00115304en_us&page=Debug_Crashed_Applications_With_gdb4hpc.html), a command-line parallel debugger based on [GDB](gdb.md).
	* [Cray Performance Measurement and Analysis Tools (CPMAT)](https://support.hpe.com/hpesc/public/docDisplay?docId=a00113947en_us&page=Cray_Performance_Measurement_and_Analysis_Tools_CPMAT.html)

For a low-overhead serial debugger available on all NREL machines, see our [GDB documentation](gdb.md).

To skip to a walk-through example of parallel debugging, click [here](#walk-through).

## Key Parallel Debugging Features

Parallel debuggers typically come equipped with the same features available on serial debuggers (breakpoint setting, variable inspection, etc.). However, unlike serial debuggers, parallel debuggers provide valuable MPI task- and thread-specific information, too. We present some key parallel features here.

Note that while we present features of ARM DDT below, we stress that the many parallel debugging tools function in similar ways and offer similar features.


### Fail points
Sometimes, some MPI tasks will fail at a particular point while others will not. This could be for a number of reasons (MPI task-defined variable goes out of bounds, etc.). Parallel debuggers can help us track down which tasks and/or threads are failing, and why. For example, in DDT, when the debugger detects that a task is failing, it prompts us to pause the program. On pausing, we can inspect which tasks are failing, and at which line in the code they are failing.

### Parallel variable inspection
Other times, your code may not fail, but will produce an obviously incorrect answer. Such a situation is even less desirable than your code failing outright, since tracking down the problem variables and problem tasks is often more difficult.

In these situations, the parallel variable inspection capabilities of parallel debuggers are valuable. We can first check if our code runs as expected when we run in serial. If so, the fault doesn’t lie with the parallelism of your code, and you can proceed using serial debugging techniques. If the code succeeds in serial but yields incorrect results in parallel, then the code is likely afflicted with a parallel bug.

Inspecting key parallel variables may help in identification of this bug. For example, we can inspect the variables that dictate how the parallel code is divided amongst MPI tasks. Is it as expected? Such a process will vary greatly on a code-by-code basis, but inspecting task-specific variables is a good place to start.

![doiownc](assets/images/debug_tools/DDT_BGW_doiownc.png)

The above images shows a comparison across 8 MPI tasks of the first entry of the “doiownc” variable of the BerkeleyGW code. In BerkeleyGW, this variable states whether or not the given MPI task “owns” a given piece of data. Here, we can see that Task 0 owns this piece of data, while tasks 1-7 do not.


### Parallel memory debugging

In addition to detecting seg faults and out-of-bounds errors as discussed in [fail points](#fail-points), parallel debuggers may offer more advanced memory debugging features. For example, DDT allows for advanced heap debugging. 

### Walk-through

To highlight some of the above features, we've introduced an out-of-bounds error to the BerkeleyGW code. We’ve changed a writing of the `pol%gme` variable from:

```
do ic_loc = 1, peinf%ncownactual
  do ig = 1, pol%nmtx
    pol%gme(ig, ic_loc, iv_loc, ispin, irk, freq_idx) = ZERO
  enddo
enddo
```

To
```
do ic_loc = 1, peinf%ncownactual
  do ig = 1, pol%nmtx
    pol%gme(ig, ic_loc, iv_loc, ispin, irk, freq_idx+1) = ZERO
  enddo
enddo
```

With this change, the sixth dimension of the array will go out of bounds. The details of the code aren’t important, just the fact that we know the code will fail!

Now, when we run the code in DDT, we receive the following error:

[FAILURE ERROR WINDOW IMAGE]

When we click `pause`, we are immediately taken to the line that caused the failure:

[IMAGE OF pol%gme HIGHLIGHTED]

We can inspect the local variables in the righthand-side box.

One particularly useful feature is the “current stack.” When we click this header, we are taken to a stack trace. When we click on each line in the stack trace, it takes us to the corresponding line in the corresponding source file, making stack tracing an error fast and simple. This is a common component of debuggers, even serial debuggers, but paired with our ability to choose which MPI task to focus on, this is a powerful feature! We get a task-specific view of the issue.


Screenshot of GUI after pausing:



-	Acknowledge that it will be more complicated in reality
-	Main point is that it will point you to the exact line of code where it died, and also show you the whole stack trace/clickable

 


## Resources

Parallel debugging tools are complex, and usage of these tools can sometimes end in attempts to “debug the debugger.” Contact [HPC Help](mailto:hpc-help@nrel.gov) if you need assistance in getting started with a parallel debugger on an NREL system.

Refer to specific debugger pages, like the [DDT](Documentation/Development/Debug_Tools/ARM/ddt.md) page, on how to set-up and run the debugging program.

