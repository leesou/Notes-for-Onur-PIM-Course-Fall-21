#  Onur PIM Course #1

## Papers

+ arxiv-2105.03814: experimental analysis of UPMEM
+ MICRO 21-Ke et al.: AxDIMM+NDP to accelerate recommendation system
+ MICRO 17-Seshadri et al: Ambit
+ ASPLOS 21-Hajinazar at al: SIMDRAM
+ PEI: PIM-Enables Instructions

## System Trends

+ Data access is a major bottleneck
+ Energy consumption is a key limiter
+ Data movement energy dominates compute

## Perils of Processor-Centric Design

+ imbalances systems
  - Processing done in one place
  - Everything else just stores and moves data -- data moves a lot
+ complex and bloated processor
  - tolerate data access 
  - complex hierarchies and mechanisms

+ conclusion: energy inefficient, low performance, complex

## Data Movement

+ dominates performance, major system energy bottleneck

## Near Data Processing

+ 3D stacked DRAM
+ compute in memory controller
+ compute in memory module (DIMM)

## Possible Designs

+ fixed-function units: each PIM unit is used for special applications
+ reconfigurable architechtures: FPGA, CGRA
+ general purpose: programmable cores
+ processing-using memory: Ambit/SIMDRAM

## Two Directions

+ minimally changing memory chips
+ exploiting 3D stack

## Minimally Changing Memory Chips

DRAM has great capability to perform bulk data movement and computation with small changes

+ Exploit internal bandwidth to move data
+ Exploit analog computation capability
+ ...

Now systems--Bulk data copy

+ high latency
+ high bandwidth utilization
+ cache pollution
+ unwanted data movement

Future systems--in-memory copy

+ None of disadvantages mentioned above remains.

RowClone: In-DRAM Row Copy

## Exploiting 3D-Stacked Memory

graph processing bottlenecks -- pagerank algorithm

+ frequent random memory access
+ little amount of computation

Two questions in 3D-stacked PIM

+ how to accelerate applications (architecture, programming model, mechanisms)
+ what's the minimal PIM support we can provide
  - without changing the system significantly

PIM-enabled instructions -- ISA extensions

