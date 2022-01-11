# Onur PIM Course #2

## Real PIM Architechtures I

+ UPMEM (2019)
+ FIMDRAM (2021)--3D HBM
+ AxDIMM (2021)

## UPMEM DIMMs' Architecture

doi: 10.1109/HOTCHIPS.2019.8875680

+ E19: 8 chips/DIMM (1 rank). DPUs @ 267MHz
+ P21: 16chips/DIMM(2 ranks). DPUs @ 350 MHz

accelerator model

+ UPMEM DIMMs coexist with conventional DIMMs
+ Integretion follows an accelerator model
+ Can be seen as a loosely coupled accelerator:
  - explicit data movement 
  - explicit kernel launch

UPMEM DIMMs resemble GPU, but have much larger memory capacity, distributed memory space

DPUs cannot be shared across multiple CPU processes.

UPMEM don't need for OS, ans has no side channels.

UPMEM Programming Example -- Vector Addition

+ Partition input arrays across: DPUs/Tasklets (software threads on a DPU)

Data Transfer

+ CPU-DPU/DPU-CPU transfers
  - serial: a single DPU
  - parallel: multiple DPUs
  - broadcast: multiple DPUs with a single buffer

+ Inter-DPU communication
  - no direct communication channel between DPUs
  - take places via host CPU

DPU

+ construction
  - DMA engine
  - 24KB IRAM for instructions
  - 64KB WRAM for data
  - in-order pipeline
+ pipeline
  - 14 stages
+ ISA

https://dpu.dev: C代码到DPU汇编代码的转换器

