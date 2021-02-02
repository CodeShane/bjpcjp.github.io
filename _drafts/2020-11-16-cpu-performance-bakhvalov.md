---
title: CPU performance hacks - Denis Bakhvalov
tags: semiconductor cpu
date: 2020-11-16
layout: post
---

## Intro
* Why
* Who Needs It
* Definition
* Book Topics
* Not Included
* Summary

## Measuring Performance
* Noise
	- [Dynamic Frequency Scaling](https://en.wikipedia.org/wiki/Dynamic_frequency_scaling) - depends on core temp
	- ![1st run (cold) vs 2nd run (hot)](/cmos/cpu-tuning/bakhvalov-freq-scaling-cold-hot.png)
	- [Mytkowicz]() - UNIX envt size & link order changes performance in unpredictable ways.
	- Personal Experience: even running a task manager tool, like Linux top, can affect measurements since some CPU core will be activated and assigned to it. This might affect the frequency of the core that is running the actual benchmark.
	- [temci: advanced benchmarking tool (github)](https://github.com/parttimenerd/temci)

* Performance Measurement in Production
	- When an application runs on shared infrastructure (typical in a public cloud), there usually will be other workloads from other customers running on the same servers. With technologies like virtualization and containers becoming more popular, public cloud providers try to fully
utilize the capacity of their servers.
	- Large service providers use telemetry systems that monitor
performance on user devices. Ex: [Netflix Icarus](https://www.youtube.com/watch?v=4RG2DUK03_0)
	- One important caveat of monitoring production deployments is measurement overhead. 1% is acceptable max.
	- LinkedIn statistical methods: [quantile-based metrics, eg Page Load time](https://arxiv.org/abs/1903.08762)

* Auto Detection of Performance Regressions
	- [SW defects leak into production at alarming rates.](https://doi.org/10.1145/2254064.2254075)
	- Manual checks = boring, error-prone, time-consuming, daily rqmnt.
	- Automated threshold-based tools:
		* [evergreen CI (MongoDB)](https://github.com/evergreen-ci/evergreen)
		* [LUCI (Chromium)](https://chromium.googlesource.com/chromium/src.git/+/master/docs/tour_of_luci_ui.md)
		* [AutoPerf - uses HW counters](http://papers.nips.cc/paper/9337-a-zero-positive-learning-approach-for-diagnosing-software-performance-regressions.pdf)

* Manual Testing
	- Don't get a single measurement - run the benchmark multiple times.
	- [comparing 2 performance distributions](bakhvalov-perf-distributions.png)
	- Distribution plots help spot unwanted behavior. If the distribution is bimodal, the benchmark likely experiences two different types of behavior. A common cause of bimodally distributed measurements is code that has both a fast and a slow path, such as accessing a cache (cache hit vs. cache miss) and acquiring a lock (contended lock vs. uncontended lock). To “fix” this, different functional patterns should be isolated and benchmarked separately.
	- [Workload Modeling book](http://cs.huji.ac.il/~feit/wlmod/)
	- Critical to calculating accurate speedup ratios: collecting a rich
collection of samples, i.e., run the benchmark a large number of times. This may sound obvious, but it is not always achievable.[SPEC CPU 2017 benchmarks](http://spec.org/cpu2017/Docs/overview.html#benchmarks) = very expensive.
	- Checking for outliers: see [latency by Gil Tene](https://www.youtube.com/watch?v=lJ8ydIuPFeU)


* SW & HW Timers
	- system-wide hi-res timer = #ticks from epoch starting date. ns resolution, consistent across CPUs; retrieved with a system OS call.
		* ```std::chrono()``` (C++)
		* access = high latency, maybe 10X than executing ```RDTSC```.
	- time stamp counter (TSC) = HW register; monotonic; one per CPU.
		* ```__tdtsc()``` (C++); more accurate over small time period.
	- Timer API comparisons: [Cpp Performance Benchmarks wiki](https://gitlab.com/chriscox/CppPerformanceBenchmarks/-/wikis/ClockTimeAnalysis)

* Microbenchmarks
	- Available in most modern languages:
		* [C++, Google](https://github.com/google/benchmark)
		* [C#, Benchmark Dot Net](https://github.com/dotnet/BenchmarkDotNet)
		* [Julia, Benchmark Tools](https://github.com/JuliaCI/BenchmarkTools.jl)
		* [Java, Microbenchmark Harness](http://openjdk.java.net/projects/code-tools/jmh/etc)
	- Important: ensure that the scenario you want to test is actually executed by your microbenchmark at runtime. Optimizing compilers can
eliminate code that could make the experiment useless, or even worse, drive you to the wrong conclusion.
	- One way to keep the compiler from optimizing away important code is to use [DoNotOptimize](https://github.com/google/benchmark/blob/c078337494086f9372a46b4ed31a3ae7b3f1a6a2/include/benchmark/benchmark.h#L307) helper functions,
* Summary 

## CPU Microarchitecture
* ISAs
* Pipelining
	- ![DLX 5-stage example](cmos/cpu-tuning/bakhvalov-pipeline-5stage.png)
	- Pipeline hazards prevent the ideal pipeline behavior resulting in stalls. The three classes of hazards are __structural__ (resource conflicts), __data__ (dependencies: read-after-write, write-after-read, write-after-write) and __control__ (change in program flow) hazards.
	- [register renaming](https://en.wikipedia.org/wiki/Register_renaming)
	- [architectural state](https://en.wikipedia.org/wiki/Architectural_state)

* Instruction Level Parallelism (ILP)
	- OOO (out of order) execution
	- Superscalar engines and VLIW
	- Speculative Execution
	- Exploiting Thread-level Parallelism
		* Simultaneous Multithreading
	- Memory Hierarchy
		* Caches
			- Data placement
			- Data finding
			- Misses
			- Writes
			- HW/SW Prefetching
		* Main Memory
	- Virtual Memory
	- SIMD Multiprocessors
	- Modern CPU Design
		* Frontend
			- The CPU Front-End fetches 16 bytes per cycle of x86 instructions from the L1 I-cache. This is shared among the two threads, so each thread gets 16 bytes every other cycle. These are
complex, variable-length x86 instructions. The pre-decode and decode stages of the pipeline convert these complex x86 instructions into micro Ops (UOPs, see section 4.4) that are queued into the Allocation Queue (IDQ).
		* Backend
			- The heart of the CPU backend is the 224 entry ReOrder buffer (ROB). This unit handles data dependencies. The ROB maps the architecture-visible registers to the physical registers used
in the scheduler/reservation station unit. ROB also provides register renaming and tracks speculative execution. ROB entries are always retired in program order.

	- Performance Monitoring Unit
		* Counters
			- ![block diagram](/cmos/cpu-tuning/bakhvalov-cpu-monitoring-blocks.png)

* Thread Level Parallelism
* Memory Hierarchy
* Virtual Memory
* SIMD
* Modern CPU Design
* Performance Monitoring

## Terminology & Metrics
* "Retired" vs "Executed" Instructions
	- ```$ perf stat -e instructions ./a.exe```

* Utilization
* CPI, IPC
* Micro-ops
* Pipeline Slots
* Core vs Reference Cycles
* Cache Misses
* Mispredicted Branches

## Analysis Approaches
* Instrumentation
* Tracing
* Workload CZ
	- Counting Events
	- Manual Counters Collection
	- Multiplexing & scaling events

* Sampling
	- User-Mode & HW Events
	- Hotspots
	- Call Stacks
	- Flame Graphs

* Roofline Models
	- [NERSC docs](https://docs.nersc.gov/development/performance-debugging-tools/roofline/)
	- [Berkeley Labs](https://crd.lbl.gov/departments/computer-science/par/research/roofline/)
	- [Techdecoded](https://techdecoded.intel.io/)
	- [PerfPlot](https://github.com/GeorgOfenbeck/perfplot)

* Static Analysis
	- Static vs Dynamic Analysis
	- [list of tools](https://en.wikipedia.org/wiki/List_of_tools_for_static_code_analysis#C,_C++)
	- [IACA](https://software.intel.com/en-us/articles/intel-architecture-code-analyzer)
	- [LLVM MCA](https://llvm.org/docs/CommandGuide/llvm-mca.html)

* Compiler Optimizations

## CPU Features
* Top-Down Analysis
	- TMA in Intel VTune
	- TMA in Linux Perf
	- Identifying the Bottlenecks
	- Locate Place in Code
	- Fix
	- Summary

* Last Branch Records (LBRs)
	- Collecting LBR Stacks
	- Call Graphs
	- Hot Branches
	- Branch Mispredictions
	- Precise Machine Code Timing
	- Branch Outcome Probability
	- Other Use Cases

* Event-Based Sampling
	- Precise Events
	- Lower Sampling Overhead
	- Memory Accesses

* Intel CPU Traces
	- Workflow
	- Timing Packets
	- Trace Collection/Decoding
	- Usages

## Part 2: Source Code Tuning

## Front-end Optimizations
* Machine Code Layout
* Basic Block
* Basic Block Placement
* Basic Block Alignment
* Function Splits
* Function Groups
* Profile-Guided Optimizations
* ITLB Optimizations

## Back-end Optimizations
* Memory Bounding
	- Cache-Friendly Data Structs
		* Sequential Access
		* Appropriate Containers
		* Packed Data
		* Aligning, Padding
		* Dynamic Allocation
		* Hierarchy-Aware Tuning

	- Explicit Memory Prefetches
	- DTLB Optimization
		* Explicit Hugepages
		* Transparent Hugepages
		* Explicit vs Transparent

* Core Bounding
	- Inlining Functions
	- Loop Optimizations
		* Low Level
			> Loop-Invariant Code Motion (LICM)
			> Loop Unrolling
			> Loop Strength Reduction (LSR)
			> Loop Unswitching

		* High Level
			> Loop Interchanges
			> Loop Blocking (Tiling)
			> Loop Fusion / Distribution (Fission)
			> Discovering Opt. Opportunities
			> Opt. Frameworks

		* Vectorization
			> Compiler Auto-Vectorization
			> Finding Opportunities
			> Illegal Vectorization
			> Not-Beneficial
			> Loop Vectorized, but Scalar version used
			> Sub-Optimal Vectorization
			> Languages with Explicit Vectorization


## Speculation Improvements
* Replacing Branches with Lookups
* Replacing Branches with Predication

## Other Areas
* Compile-time Computation
* Compiler Intrinsics
* Cache Warming
* Detecting Slow FP Math
* System Tuning

## Multithreaded Apps
* Scaling & Overhead
* Parallel Efficiency Metrics
	- Effective CPU Utilization
	- Thread Count
	- Wait Time
	- Spin Time

* Intel VTune Profiler
	- Finding Locks
	- Platform View

* Linux Perf
	- Finding Locks

* Coz
	- [github](https://github.com/plasma-umass/coz)
	- [compare to sampling profilers](https://easyperf.net/blog/2020/02/26/coz-vs-sampling-profilers)

* eBPF and GAPP
* Coherence Issues
	- Cache Coherency Protocols
	- True Sharing
	- False Sharing


## Reducing Measurement Noise
* Dynamic Frequency Scaling (DFS)
* Simultaneous Multithreading
* Scaling Governor
* CPU Affinity
* Process Priority
* Filesystem Cache

## LLVM Vectorizer
* Loops w/ Unknown Trip Count
* Runtime Pointer Checks
* Reductions
* Inductions
* If Conversions
* Pointer Induction Variables
* Reverse Iterators
* Scatter / Gather
* Mixed-Type Vectorization
* Function Call Vectorization
* Superword-Level Vectorization
* Outer Loop Vectorization