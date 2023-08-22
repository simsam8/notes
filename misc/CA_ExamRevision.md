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


## 2 Practice Quiz 

1. Given the following performance of two programs on three CPUs,
    use the geometric mean to calculate which computer is the fastest.

    ||CPU A|CPU B|CPU C|
    |--|--|--|--|
    |P1|40|15|20|
    |P2|40|1000|150|

- [ ] CPU A is faster
- [x] CPU B is faster 
- [ ] CPU C is faster


CPU A: 1
CPU B: 3.06
CPU C: 1.37


2. Calculate the average CPI for the following instruction frequencies:

|Instruction|Frequency|CPI_instruction|
|--|--|--|
|ALU|40%|4|
|Load|30%|5|
|Branch|25%|4|

For 5M instructions?

ALU: 0.4*4
Load: 0.3*6 
Store: 0.05*5 
Branch: 0.25*4 

Answer = 4.65



3. For the CPU described in Question 2, what is the execution 
    time in ms, supposing a CPU frequency of 2GHz?

Answer:
(5*10^6 * 4.65)/2*10^9 = 11.625 ms


## 1.1.6 Amdahl's Law

### Amdahl's Law

"If 50% of the execution time is sequential, the maximum speedup
is 2, no matter how many cores/processes you use"

S = speedup 
s = 1 - f = serial_fraction
f = 1 - s = parallel_fraction
p = # processor_cores

Time = 1 = s + f/p

S = 1/(s+f/p) = 1/(1-f+(f/p))

### Amdahl's Law Generalization
- Suppose we can improve fraction f by factor F 
- What will be overall improvement?


S = 1/(s+f/p) = 1/(1-f+(f/p))


S = speedup 
s = 1 - f = fraction we cannot improve 
f = 1 - s = fraction we can improve 
F = improvement factor

## 1.1.7 Amdahl's Law Example

- FP instructions improved to run 2X as fast, but only 10% 
    of all executed instructions are FP 

    S = 1/(1-f+f/F) = 1/(0.9+0.1/2) = 1/0.95 = 1.053

- We want overall speedup of 2 and can accelerate FP 
    instructions by 4X 
    
    - What should be the fraction of FP instructions?

    S = 1/(1-f+f/F) -> 2 = 1/(1-f+f/4) -> f = 0.5/0.75 = 66.7%


### Amdahl's Law Implications

2 independent parts A and B. AAAAAAAABBBBB
Make B 5x faster             AAAAAAAAB
Make A 2x faster             AAAABBBBB


- Implications: 
    - Make the common case fast
    - Law of diminishing returns: optimizations will have
        less and less effects

### Design Principl.s to Make Processors Faster

- Take advantage of parallelism
    - Pipelining, ILP(Instruction level), DLP(data level), TLP(thread level)


- Principle of locality
    - Programs spend 90% of their execution time 
        in 10% of their code 
    - Can predict with reasonable accuracy which instructions and data 
        program will use in near future

- Make the common case fast 
    - Amdahl's law


### Summary
- Aspects of computer performance:
    latency, throughput, availability,...
- Computer architects focus on CPU time 
- SPEC is successful desktop benchmark suite 
    - EEMBC used in embedded domain

- Use geometric mean to summarize execution time ratios

ExecutionTimeRatio = ExecutionTime_reference/ExecutionTime_new

- Amdahl's law implies design rule "make the common case fast"

S = 1/(s+f/p) = 1/(1-f+f/p)

- CPU performance equation 

T = (N_instr x CPI)/f


- Design principles
    - Exploit parallelism 
    - Exploit locality 
    - Make the common case fast

### Test Yourself

- What is a benchmark? 
- Are real applications used to measure CPU performance?
- What is SPEC? 
- We can improve 75% of the total execution time of our 
    application by a factor of 3. What is the overall speedup?

    - [ ] 3.0 
    - [ ] 1.5 
    - [x] 2.0 
    - [ ] 1.2



## 1.1.8 Introduction to Embedded Systems

### What are Embedded Systems?

- Embedded system = computer system with dedicated function 
    lodged in other devices 

    - Hard to define boundry between embedded and general purpose computing

### Examples of Embedded Systems
- Everyday machines and devices 
    - Watches, cameras, microwaves, washing machines, TVs,...

- Automobiles, airplanes, trains 
- Handheld digital devices 
    - PDAs, cell phones, music players,...
- Video game consoles, set-top boxes
- Printers, network swithes
- ... 


### Characteristics and Requirements of Embedded Systems 
- Execute 1 or few applications 
    - Lower compatibility barriers

- Real-time constraints
- Minimize cost
- Minimize power consumption
- Minimize memory
- Physical dimensions
- Interface with physical world


### Real-Time Consraints 
- Real-time performance requirement: (segment of)
    application has absolute maximum execution time

- Hard real-time system 
    - all deadlines are hard 
    - missed deadline = total system failure
    - Ex: airbag

- Soft real-time system 
    - some deadlines are soft 
    - soft deadline may occasionally be missed 
    - Ex: video player

### Implementation Alternatives 

- General purpose processors (GPPs)
- Application-specific instruction set processors (ASIPs)
- Reconfigurable hardware (FPGAs)
- Application-specific integrated circuits(ASICs)

vvv Performance and power, ^^^ Flexebility



### Exercise
- What are embedded systems? 
- What is the main difference between hard and soft real-time systems?


### Practice Quiz
1. What is the difference between a hard and soft real-time system?
- [x] in a hard-real time systems all deadlines must be met while 
        in a soft-real time system occasionally some deadlines may 
        be missed. 
- [ ] in a soft-real time system all deadlines must be met while in a 
        hard-real time system occasionally some deadlines may 
        be missed


## Practice Quiz 

1. What is an embedded system? 
- [ ] Every computing system is an embedded system 
- [x] A computing system with dedicated function, often with
        real-time constraints, is an embedded system
- [ ] A general purpose computer with less than 1GB of RAM is 
        an embedded system 
- [ ] A system which has an ARM processor is an embedded system


2. Faster execution time always means less energy
- [ ] True
- [x] False


3. Why is it important to minimize energy consumption in an embedded system?
- [ ] restricted availability of energy 
- [ ] limited battery capacity 
- [x] both (a) and (b)


## Review Quiz 1.1

1. What is the best metric for comparing performance?
- [ ] arithmetic mean 
- [x] geometric mean 
- [ ] median 
- [ ] maximum performance 
- [ ] harmonic mean 


2. Calculate the execution time in ms, supposing to have a CPU 
    with the following instruction frequencies: 

    | Instruction    | Frequency    | CPI_instr    |
    |---------------- | --------------- | --------------- |
    | ALU    | 45%    | 5    |
    | Load    | 25%    | 6    |
    | Store   | 10%   | 5   |
    | Branch   | 20%   | 3   |
     

    For 2M instructions and a CPU frequency of 3GHz?

    Answer: T = 2*10^6 x (.45*5+.25*6+.1*5+.2*3)/3*10^9
            = 3.233x10^-3 s = 3.233 ms


3. Which of the following is an energy efficiency metric?
- [ ] FLOPS 
- [ ] MIPS 
- [x] Performance per watt
- [ ] Power consumption


4. Both power consumption and performance per watt matters for an embedded system
- [x] True 
- [ ] False



## 1.2.1 Highlights of MIPS64 Architecture

### Module Objectives 

After this module you are able to 
- describe main features of MIPS64 ISA 
- translate (C-) code to MIPS64 assembly 
- optimize MIPS64 code


### MIPS 64 
- Simple load-store instruction set 
- Designed for pipelining efficiency 
- Efficient instruction set for compiler to target


### Registers

- 32 64-bit general-purpose registers (GPRs)
    - R0,R1,...,R31
- R0 is always 0


- 32 floating-point registers (FPRs)
    - F0,F1,...,FP31
    - hold single- or double-
        precision FPs (float,double)
    - when used as single-precision,
        half of FPR is unused

- Instructions for moving between GPRs and FPRs


### Special Registers

- Few special registers: 
    - hi and lo:
        - (2n)-bit product of n-bit multiply 
        - quotient and remandier of division
    - floating-point status register 
    - Execption program counter
- Instructions for moving special registers from/to GPRs


### Data Types
- Integer: 
    - 8-bit bytes (char)
    - 16-bit half words (short,Unicode)
    - 32-bit words
    - 64-bit double words

- Operations process 64-bit integers 
    - Bytes, half words, words are zeor extended (lbu, lhu, lwu) or 
        sign extended (lb,lh,lw)


- Floating-point 
    - 32-bit single-precision (float)
    - 64-bit double-precision (double)


### Practice Quiz

1. How can you emulate register indirect addressing mode in MIPS64?
- [ ] By using R0 as base register 
- [ ] Combining register direct and immediate
- [x] By using displacement 0 in register indirect with displacement
- [ ] Cannot be emulated


## 1.2.2 MIPS64 Addressing Modes and Instruction Formats


### Addressing Modes 

| Mode    | Example    | Meaning    | When used    |
|---------------- | --------------- | --------------- | --------------- |
| Register direct    | add R1,R2,R3    | R1 = R2+R3    | when value is in register    |
| Immediate    | addi R1,R2,#3   | R1 = R2+3   | for constants   |
| Reg ind w/ displ   | lw R1,100(R2)   | R1 = Mem[R2+100]   | for array elements   |

- Register indirect: displacement is 0 
- Absolute addressing: R0 base register
- Mode bit specifies Big Endian / Little Endian
- Data type specified in opcode
    lb,lh,lw,ld,l.s,l.d

- Memory accesses must be aligned


## 1.2.3 MIPS64 Operations

### Operations 
- Four broad classes 
    - loads and store 
    - ALU operations 
    - Branches and jumps
    - Floating-point



### Floating-point Operations 
- Arithmetic instructions: ADD.{S,D},SUB.{S,D},MUL.{S,D},DIV.{S,D}
- Paired single operations perform 2 FP operations on each half of 
    FP register: {ADD,SUB,MUL,DIV}.PS
- Multiply-add: MADD.{S,D,PS}
- Moves: MOV.{S,D}
- Compares: C.{LT,LE,EQ}.{S,D}F0,F1 
    - set bits in FP status register 
- Branches: BC1{T,F}
    - branch on coprocessor 1 (= floating-point unit) true, false


- Conversion: 
    - cvt.d.s F0,F1 ; F0 = (double)F1 (convert single to double)
    - cvt.w.d F0,F1 ; F0 = (int)F1(convert double to word)

- Moves between FPRs and GPRs:
    - MFC R1,F1 ; R1 = F1 
    - MTC1 F1,R1 ; F1 = R1


## 1.2.4 Basic Code Optimizations

### Practice Quiz
1. When can we move branch testing condition to the end?
- [ ] Loop not executed at all 
- [x] Loop executed at least once
- [ ] Loop executed n times 
- [ ] Loop executed at least 2 times


### Loop Unrolling 
- In general 
    - loop upper bound n unknown 
    - n no multiple of loop unrolling factor k 

- Then need 2 loops: 
    - 1 unrolled that iterates [n/k] times
    - Copy of original that iterates n mod k times
        - But mod expensive operation that shoud be avoided



## Review Quiz 2 
1. Load-store architecture only allows memory to be accessed by 
    load and store instructions
- [x] True
- [ ] False


2. What is the difference between DADD and DADDU instructions? 
- [x] DADD is a double word add instruction and supports overflow 
        detection while DADDU is double word unsigned add instruction and 
        does not support overflow detection
- [ ] DADD is a double word add and does not support overflow detection 
        while DADDU is double word unsigned add and supports overflow detection


3. Assume a loop with n iterations has been unrolled by a factor of k. 
    How many times the second loop should iterate when n%k != 0?
- [ ] ceil(n%k)
- [ ] ceil(n/k)
- [ ] floor(n%k)
- [x] floor(n/k)


4. What are the disadvantages of loop unrolling?
- [x] Loop unrolling increases the number of instructions 
- [x] Loop unrolling may increase instruction cache misses


5. What are three basic code optimization techniques?
- [x] elimination of induction variables
- [x] loop unrolling 
- [ ] hardware prefetching 
- [ ] set associative cache 
- [x] elimination of redundant branches



## 1.3.1 Pipelining Principles 

### Module Objectives 
After this module you are able to 

- describe pipeline concept
- list 5 stages in classical pipline and 
    what happens in each 
- describe which features of MIPS ISA 
    make pipelining easy 
- describe pipelining hazards and potential solutions


### Pipelining - The Idea

- Laundry Example: Ann, Ben, Cathy, Dave each have one load
    of clothes to wash, dry, and fold
- Washer takes 30 minutes
- Dryer takes 40 minutes 
- "Folder" takes 20 minutes


Sequential laundry: 
- Do everything then start the next one 


Pipelined Laundry: Start work ASAP
- Ideal speedup = # stages
- Do we achieve this? 
- Why? -> binary compatibility


## 1.3.2 Canonical 5 Stage Pipeline

### Classical 5-Stage Pipeline

- Instruction fetch (IF)
- Instruction decode (ID) read source registers
- Execute (EX)
- Memory access (MEM)
- Write Back (WB)

| cycle1    | cycle2    | cycle3    | cycle4    | cycle5    |
|---------------- | --------------- | --------------- | --------------- | --------------- |
| IF    | ID    | EX    | MEM    | WB   |



### Practice Quiz 

1. What is the ideal speedup due to pipelining?
- [ ] # executed instructions
- [x] # stages



## 1.3.3 MIPS Pipeline Features and Pipeline Hazards

### What Makes Pipelining Easy? 
- All MIPS instructions same lenght
- Few instructions formats 

- Only load ant store access memory 
    - Assume support for "add memory"
    - addmem R1,R2,4(R3) ; R1 = R2 + Memory[4+R3]


### What Makes Pipelining Challenging? 
- Structural Hazards 
    - HW(hardware) cannot support papallel execution of instr stages

- Control Hazards 
    - delay between fetching and performing branch/jump

- Data Hazards 
    - Instr needs result of other instr still in pipeline


## 1.3.4 Structural Hazards and Data Hazards

### Structural Hazards 
- Suppose 1 memory w/1 port 

### Data Hazards 
- When does register file access take place?


### Practice Quiz
1. What is a data hazard?
- [x] a hazard occuring because an instruction depends upon the 
        result of a prior instruction 
- [x] a hazard occuring because the hardware cannot execute 
        the instructions in parallel 
- [ ] a hazard occurring because of a branch


### Forwarding / Bypassing

- Don't wait until result writte back to RF but forward it to 
    next stage immediately


## 1.3.5 Load-use Data Hazard


### Hata Hazard Even with Forwarding

- Load-use data hazard

### Hazard Detection Unit 
- Detects data hazard 
    - ID/EX.instr==Id && (ID/EX.rt==IF/ID.rs||ID/EX.rt==IF/ID.rt)

- Stalls pipeline 
    - prevent write to PC and IF/ID 
    - insert no-op into EX stage


### Scheduling to Avoid Load Hazards 
- Produce fast code for 
    - a-f stored in memory


## 1.3.6 Control Hazards

### Control Hazards
- In current pipelined datapath, branch takes effect at end of MEM stage


### Practice Quiz 
1. How can we avoid data hazard? 
- [ ] prediction 
- [x] forwarding 
- [ ] caching 
- [ ] pipelining



### Branch Penalty Impact

- Assume
    - ideal CPI = 1 
    - 30% branches 
    - 50% branches taken 
    - 3-cicly penalty on taken branches

- Actual CPI = 1 + 0.3x0.5x3 = 1.45

### Reducing Branch Delay 
- 2 part solution:
    - Determine branch taken / not taken sooner AND 
    - Compute branch target address earlier

- MIPS solution: 
    - Move branch condition evaluation to ID stage 
    - Calculate branch target address in ID stage 
        - Extra adder in ID stage 
    - 1-cycle penalty for branch versus 3

- MIPS branches test if reg=0, reg!=0,
    reg1=reg2, reg1!=reg2,...



## 1.3.7 Deal with Branch Hazards 

### Recap 
- Canonical pipeline 
- Pipeline hazards 
    - Structural hazards 
    - Data hazards 
    - Control hazards 
    
- Possible solution 
    - Replicate Functional units (FUs) 
    - Forwording - instr reordering 
    - Early branch execution


### 4 Branch Hazard Alternatives 

1. Stall until branch direction is clear
2. Predict Branch Not Taken 
    - Execute successor instrs
    - "Squash" instr in pipeline if branch actually taken
3. Predict Branch Taken 
    - 53% MIPS branches taken on average 
    - But haven't calculated branch target adress in MIPS 
        - Canonical MIPS pipeline still incurs 1 cycle branch penalty 
        - Other processors: branch target known before branch decision

4. Delayed Branch 
    - Define branch to take place after a following instr
    - Instr fetched until then are always executed
    - MIPS uses this 
        - single branch delay slot 
        - instr after branch is always executed 
        - all MIPS processors implement it, even if not needed. Why?


### Practice Quiz
1. MIPS uses single branch delay slot 
- [x] True 
- [ ] False


## 1.3.8 Scheduling Instructions for Branch Delay Slot

### Delayed Branch 

- Where to get instructions to fill branch delay slot? 
    - Frlom before branch 
    - From target address: only valuable when branch taken 
    - From fall through: only valuable when branch not taken

- If compiler cannot find such an instruction, it must insert a nop(non operation)
    - e.g. add r0,r0,r0


### Scheduling Branch Delay Slot: From before 

- Delay slot scheduled w/ instr from before the branch
- Branch may net be dependent on the instr 
- Best choice, always improves performance

### Scheduling Branch Delay Slot: From Target 

- Delay slot scheduled from branch target 
- Must be OK to execute that instr if branch is not taken
- Target instr may need to be copied because it can be reached 
    by another path
- Good choice if branch taken with high probability



### Scheduling Branch Delay Slot: From Fall Through 
- Delay slot scheduled from fall through path 
- Must be OK to execute that instr if branch taken 
- Improves performance when branch is not taken with high probability


## Delayed Branch Conclusion 
- Compiler effectiveness for single branch delay slot: 
    - 60% of branch delay slots filled 
    - 80% of instrs executed in branch delay slots useful 
    - 60% x 80% =(prox) 50% of slots usefully filled


- Downside
    - Modern cores deeper pipelines and multiple issue ->  
        branch delay grows and > 1 delay slot needed
    - Delayed branch replaced by more expensive but more flexible
        dynamic approaches (branch prediction)
    - Growth in #transitors made dynamic approaches relatively cheaper

## 1.3.9 Module Summary

### Summary 
- Can increase frequency & performance by pipelining instrs 
- Canonical pipeline: IF ID EX MEM WB 
- MIPS ISA designed w/ pipelining in mind 
    - All instrs 4 bytes 
    - Src regs always in same fields
    - Load/store architecture

| Pipelining hazard   | Possible solutions    |
|--------------- | --------------- |
| Structural hazard   | Replicate functional units   |
| Data hazard   | Forwarding - Hazard detection - Instr reordering   |
| Control hazard   | Early branch execution - Branch delay slots - Branch prediction   |


### Practice Quiz 
1. What are the reasons for NOT using branch delay slots 
    in the modern processors? 
- [x] mode flexible approaches such as dynamic branch prediction available
- [x] hard to find several independent instructions for delay slots
- [x] modern processors use deeper pipelines


## 1.3.10 Exercise

- Show how code will be executed on 5-stage pipeline with full 
    forwarding HW by completing table below
    - Place IF,ID,EX,MEM, or WB in the box if instr in 1st 
        column is in that stage


## 3 Review Quiz

1. What makes pipelining challenging? 
- [x] structural hazards
- [x] control hazards
- [x] data hazards

2. What is the penalty of a branch in MIPS? 
- [x] 1CC 
- [ ] 2CC 
- [ ] 3CC 
- [ ] 4CC 

3. The instruction in the branch delay slot is always executed 
- [x] True 
- [ ] False

4. Who inserts instruction in the branch delay slot? 
- [ ] student 
- [x] compiler 
- [ ] professor 
- [ ] programmer


## 1.4.1 Multicycle Operations

### Module Objectivel 

After this module you are able to 
- extend canonical MIPS pipeline with multicycle operations 
- identify hazards in longe pipelines and potential solutions 
- describe MIPS R4000 pipeline 
- optimize code for particular pipeline organization

### Multicycle Operations 
- Certain instructions (e.g., mul, div, FP operations) do not execute in 1 cycle

- Must handle multicycle operations 
    - Introduce several execution pipelines 
    - Allow multiple outstanding operations
    
### Multiple Functional Units

- IF 
- ID 
    - EX 
    - M(FP/int multiplier)
    - A (FP adder)
    - DIV (FP/int divider)
- MEM 
- WB
