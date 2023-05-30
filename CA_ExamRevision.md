# Revision

## 1.1.1 Definiton and Objectives

### What is Computer Architecture

- "Computer Architecture is the science and
art of selecting and interconnecting hardware
components to create computers that meet
functional, performance and cost goals"
- "Computer Architecture is not about using
computers to design buildings"

### Specialization Objectives - Fundamentals

- Review performance, instructions, pipelining, and caches

### Specialization Objectives - Dynamic Exploitation of ILP

- Out-of-order execution, register renaming, branch predicion,
speculation, ...


### Specialization Objectives - SIMD instructions

- Accelerate applications using SIMD instructions

### Specialization Objectives - Core Multithreading

- Name and describe different core multithreading techniques

### Specialization Objectives - Memory Hierarchy

- Describe and apply advanced cache optimizations

### Specialization Objectives - Multicores

- Snoopy cache coherence, distributed shared memory, atomic RMW
instructions, ...



## 1.1.2 Performance Measurement

### Intel Atom Processor SPECint*_rate_base2006

SPEC CPU2006:

- Measures integer and floating point operations performance
- Contains 12 integer and 17 floating point applications
- Compute intensive, concentrates on CPU and memory


### Performance per Watt with Linpack

Linpack* benchmark

- performs double precisions vector and matrix operations.
- often used by HPC community to measure FLOPS of a 
    processor or coprocessor.

### Aspects of Computer Performance

- Time 
    - Response time / latency / execution time
        - time between start and completion of event/
        task / program (n seconds)

    - Throughput/rate 
        - rate of processing work (n jobs / second)


- Other aspects:
    - Availability, scalability, performance per Watt, ...


### How to Measure Time?
#
- Wall-clock time = elapsed time 
- Multiprogrammed CPU works on other 
    process when current process stalled for I/O 
- CPU time = time CPU is computing

### Practice Quiz
1. Which of the following is wrong:
    - [ ] The wall-clock time is the total elapsed time, including IO, operating systems overhead, etc
    - [ ] Multi-threading improves the throughput of a process 
    - [ ] The CPU time does not include the IO time 
    - [x] Multi-threading improves the execution time of a process



## 1.1.2 Benchmarks

### Benchmarks

- Test drive before buying new car
- Test drive before buying new PC?
- **Benchmark**:  used to evaluate performance
- **Benchmark suite**: set of such programs 

- 5 types of programs used to evaluate performance:
    - Real applications
        - portability problems
        - important activity has to be eliminated

    - Modified (or scripted) applications
        - enhance portability
        - focus on particular aspect of system performance
            - e.g., remove I/O to create CPU-oriented Benchmarks
        - scripts to reproduce interactive behaviour

    - Kernels
        - Small, key pieces from real programs
        - Livermore loops and Linpack
        - Best used to isolate performance of individual features

    - Toy Benchmarks
        - Quicksort, Sieve of Eratosthenes, ...
        - Small, easy but not useful to evaluate performance
    - Synthetic Benchmarks
        - "Typical" instruction mixes
        - Whetstone and Dhrystone


### Benchmark Suites

- Benchmark suite = collection of benchmarks 
- Most successful standardization attempt:
    - SPEC(Standard Performance Evaluation Corporation)

- Focuses on CPU performance
- Current generation: SPEC CPU2006
    - 12 int benchmarks: CINT2006
    - 17 FP benchmarks: CFP2006


### Some Other SPEC Benchmarks
- Graphics benchmarks:
    - SPECviewperf: OpenGL 3D rendering performance
    - SPECapc: apps making extensive use of graphics 

- Server apps have significant I/O activity
    - SPECSFS: file server benchmark 
    - SPECWeb: web server benchmark


### Embedded Benchmarks
- Less developed than desktop and server benchmarks
- Most designers devise benchmarks that reflect their application 
- One attempt: EDN Embedded Microprocessor Benchmark Consortium (EEMBC)
- Kernels and benchmarks from 5 application domains
    - Automotive/industrial
    - Consumer
    - Network
    - Office automation
    - Telecommunications

### Summary
- Aspects of computer performance: 
    latency, throughput, availability, ...
- Computer architects focus on CPU time 
- SPEC is successful desktop benchmark suite 
    - EEMBC used in embedded domain


### Test Yourself
- What is a benchmark?
- Are real applications used to measure CPU performance?
- What is SPEC?


## 1 Practice Quiz Fundamentals

1. What is the throughput?
- [ ] performance per Watt (the number of FIOPs per Watt)
- [x] rate of processing work (n/jobs/second)
- [ ] the time between start and completion of event/task/program(n seconds)
- [ ] the percentage of time a system is up and running

2. What is SPEC?
- [ ] is a benchmark suite developed to measure performance based
     on the latest Java application feature 
- [ ] is a benchmark that evaluates the power and performance 
     characteristics of volume server class computers 
- [ ] is the worldwide standard for measuring graphick performance 
     based on professional applications 
- [x] is a benchmark suite designed to provide performance measurements 
     that can be used to compare computer-intensive workloads on 
     different computer systems


3. What is the goal of the EEMBC benchmark?
- [x] to evaluate performance of embedded microprocessors
- [ ] to evaluate integer computation performance 
- [ ] to measure the energy effeciency of different computer systems 
- [ ] to evaluate floating point performance 



## 1.1.4 Summarizing Performance

### Summarizing Performance
- If there is 1 program, it is clear which computer is faster
- When there is >1 program, things become tricky
    - How do you aggregate their performance?

- Example:

    ||CPU A|   CPU B|   CPU C| 
    |--|--|--|--|
    |Program 1|   1    |    10 |     20 |
    |Program 2|   1000 |   100 |    20  |
    |Total    |   1001 |   110 |   40 |


#### Practice Quiz

1. When is C1 better than C2?
- [x] w1 > 50% and w2 <= 50%
- [ ] always
- [ ] w1 > 25% and w2 <= 75%
- [ ] w1 > 90.9% and w2 <= 9.1%
- [ ] never



- What if programs not run equally often?
- Two approaches:
    - Weighted execution time 
    - Normalize execution times to a reference machine
        and take average

### Weighted Execution Time 

- Program P_i has weight Weight_i
    - indicates frequency
    - weights add up to 1 
- Program P_i takes time Time_i
- Weighted arithmetic mean: sum(Weight_i x Time_i)


### Weighted Execution Time Examples

||CPU A|CPU B|CPU C|
|--|--|--|--|
|Program P1|1|10|20| 
|Program P2|1000|100|20| 
|Arithmetic mean|500.5|55|20|
|Weighted mean(W1=0.8,W2=0.2)|200.8|28|20|
|Weighted mean(W1=0.9,W2=0.1)|100.9|19|20|


### Test Yourself
- We need to buy a new computer 
- Mostly we run 2 programs: P1 and P2
- We run these on 3 computers C1, C2, and C3 and obtain


||C1|C2|C3|
|--|--|--|--|
|Program P1|1|    10|   100|
|Program P2|100|  10|   1| 
|Sum|             101|  20|   101|   


- When is C1 the best buy? (What frequencies should P1 and P2 have?)
- When C2? When C3?


Solution:

- Frequency (weight) P1: W1
- Weight P2: W2 = 1-W1
- C1: W1x1 + W2x100
- C2: W1x10 + W2x10
- C3: W1x100 + W2x1

- C1 better than C2:
    - W1 + 100W2 < 10W1 + 10W2
    - 90W2 < 9W1 
    - 90W2 < 9(1-W2)
    - 99W2 < 9 
    - W2 < 9/99 = 1/11 =(aproximate) 9.1%
    - W1 > 10/11 =(aproximate) 90.9%

TODO: calculate the other two



### Normalized Execution Time 

- Normalize execution time to a reference computer 

TODO: fill in with formula

 ExecutionTimeRatio = ExecutionTime_reference/ExecutionTime_new

 - Used by SPEC, called SPECRatio
 - But do NOT use arithmetic mean to average normalized execution times


### Normalized Execution Time Arithmetic Mean Example 

- Do NOT use arithmetic mean to average normalized execution times 


||CPU A|   CPU B|   CPU C|
|Program 1|   1|       10|      20|
|Program 2|   1000|    100|     20|


||Normalized to A|||         |Normalized to B||
|--|--|--|--|--|--|--|
||                    A|       B|       C|       A|       B|       C|
|Program 1|           1.0|     0.1|     0.05|    10.0|    1.0|     0.5|
|Program 2|           1.0|     10.0|    50|      0.1|     1.0|     5.0|
|Arithmetic mean|     1.0|     5.05|    25.025|  5.05|    1.0|     2.75|


### Geometric Mean
- Use geometric mean instead
    - independent of refrence 
    - but no physical meaning

TODO: fill in with formula

n_root(multiply_n(ExecutionTimeRatio_i))



||Normalized to A||||Normalized to B||
|--|--|--|--|--|--|--|
||                    A|       B|       C|       A|       B|       C|
|Program 1|           1.0|     0.1|     0.05|    10.0|    1.0|     0.5|
|Program 2|           1.0|     10.0|    50|      0.1|     1.0|     5.0|
|Geometric mean|      1.0|     1.0|     1.58|    1.0|     1.0|     1.58|


## 1.1.5 CPU Performance Equation

### CPU Performance Equation

TODO: fill in with formula

T = N_instr x CPI x t_cycle = (N_instr x CPI)/f 

- N_instr = # instructions executed (instruction count)
- CPI = Cycles Per Instruction
- t_cycle = cycle time = duration of clock cycle
- f = clock frequency

## Improving Performance 

- CPU performance equation shows how to improve performance
- Unfortunately factors are interdependent -> trade-off

Reduce      How                                         Side effect
N_instr     Increase capability/complexity of instrs    CPI/t_cycle increases
CPI         Simpler instrs requiring fewer cycles       N_instr increases
t_cycle     Less work per cycle                         CPI increases


### Calculating Execution Time 
- Program executes 5M instrs w/ instr mix:

|Instruction     |Frequency   |CPI_instr|
|--|--|--|
|ALU             |50%         |3| 
|Load            |20%         |5| 
|Store           |10%         |4| 
|Branch          |20%         |3|


- CPU has frequency of 2 GHz
- What is the execution time?

CPI = sum_instr(Freq_instr = CPI_instr)

CPI = 0.5 * 3 + 0.2 * 5 + 0.1 * 4 + 0.2 * 3 = 3.5


T = N_instr x CPI x t_cycle = (N_instr x CPI)/f 


T = (5*10^6 * 3.5)/2*10^9 = 8.75*10^-3 = 8.75ms


### Test Yourself

- Measurements:
    - Frequency of FP ops: 25%
    - Average CPI of FP ops: 4.0
    - Average CPI of other instrs: 1.33 
    - Frequency of FPSQR: 2%
    - CPI of FPSQR: 20 

- 2 design alternatives:
    - Decrease CPI of FPSQR to 2.0 
    - Decrease average CPI of all FP ops to 2.5 

- Which one is best?
