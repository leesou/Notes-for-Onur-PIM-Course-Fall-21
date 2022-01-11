# Onur PIM Course #3

## UPMEM DPU: Throughput

+ The arithmetic throughput of a DPU saturates at 11​ or more tasklets.
  - consistent for different data types

+ INT32 ADD/SUB are 17% faster than INT64 ADD/SUB
  - Arithmetic Throughput = $\frac{frequency_{DPU}}{\#instructions}$​
  - When the pipeline is full, one instruction retires at each cycle.
  - Microbenchmark of INT64 has one more instruction (7) than that of  INT32 (6).

+ Huge throughput difference between ADD/SUB and MUL/DIV.
  - DPUs don't have a 32-bit multiplier.
  - MUL/DIV implementation is based on bit shifting and addition in 1 cycle.
    - MUL/DIV take a maximum of $\#bit\_width$ cycles.

+ DPUs provide native hardware support for 32/64 bit integer addition and subtraction. DPUs do not natively support 32-/64-bit multiplication and division, and floating point operations.
  - MUL/DIV and float/double operations are emulated by the UPMEM runtime library.

## UPMEM DPU: WRAM Bandwidth

STREAM benchmark: COPY, ADD, SCALE, TRIAD

WRAM bandwidth = $\frac{Bytes\times frequency_{DPU}}{\#instructions}$

+ All 8-byte WRAM loads/stores take 1 cycle when the DPU pipeline is full.
+ The sustained bandwidth provided by DPU's internal WRAM is independent of memory access pattern.

## UPMEM DPU: MRAM Latency and Bandwidth

Latency of a single DMA transfer for different transfer sizes.

STREAM benchmark

Strided/Random access pattern

### Bandwidth

MRAM Bandwidth = $\frac{size\times frequency_{DPU}}{MRAM Latency}$, MRAM Latency = $\alpha + \beta\times size$

+ DPU's MRAM bank access latency increases linearly with transfer size.
+ The maximum theoretical MRAM bandwidth is 2 bytes per cycle.
+ Read/Write accesses to MRAM are symmetric.
+ The sustained MRAM bandwidth increases with data transfer size.
  - Use large DMA transfer sizes when all accessed data is going to be used.
  - Fetch more bytes than necessary within a 128-byte limit.

+ Larger transfers require more WRAM, which may limit then umber of tasklets.
  - Choose the data transfer size between the MRAM bank and the WRAM based on WRAM usage.

### STREAM

COPY-DMA saturates with two tasklets.

COPY--6, ADD--6, SCALE/TRIAD--11

The latency of MRAM access becomes longer than pipeline latency after 4/6 tasklets for COPY/ADD.

+ When the access latency to an MRAM bank is larger than the pipeline latency, DPU saturates earlier. This is a memory-bound workload. 
+ Otherwise, for compute-bound workload, DPU saturates at 11 tasklets.

### Access Pattern

For strided access patterns with a stride smaller than 16 8-byte elements, fetch a large contiguous chunk from MRAM bank.

For strided access patterns with larger strides and random access patterns, fetch only the data elements that are needed from an MRAM bank.

## UPMEM DPU: Throughput vs. Operational Intensity

Characterize memory/compute bound regions for different datatypes and operations. (Roofline model)

operational intensity (OI): the number of arithmetic operations performed per byte accessed from MRAM

+ The arithmetic throughput of a DPU saturates at (very) low operational intensity. DPU is a compute-bound processor.

## Takeaways

+ UPMEM PIM architecture is fundamentally compute-bound. The most suitable workloads are memory-bound.
