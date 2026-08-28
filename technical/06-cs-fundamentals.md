# CS Fundamentals — Technical Study Notes

> **Why it is asked:** These topics appeared in the **62nd BMA Special Course** (Signals / CSE) actual exam, each carrying 10 marks. They were not covered in earlier past papers but are now confirmed exam topics. Study this file alongside `01-networking.md` and `03-programming.md`.

---

## 1. Cache Memory

### What is cache memory?

Cache memory is a small, extremely fast memory unit built into or very close to the CPU. It stores copies of recently used or frequently accessed data and instructions, so the CPU can retrieve them without waiting for the slower main memory (RAM).

**Problem it solves:** The CPU can execute instructions in under 1 nanosecond, but fetching data from RAM takes 60–100 nanoseconds — a huge speed mismatch. Cache bridges this gap.

### Cache hierarchy: L1, L2, L3

```
CPU Core
  │
  ├──► L1 Cache  (~1–4 cycles)   ← Fastest, smallest
  │       │ miss
  ├──► L2 Cache  (~5–15 cycles)  ← Medium speed
  │       │ miss
  ├──► L3 Cache  (~30–60 cycles) ← Shared across cores, largest
  │       │ miss
  └──► RAM       (~200+ cycles)  ← Main memory
```

| Feature | L1 | L2 | L3 |
|---|---|---|---|
| Location | Inside CPU core | Inside/near CPU core | On-chip, shared by all cores |
| Size | 32 KB – 512 KB | 256 KB – 4 MB | 4 MB – 64 MB |
| Speed | Fastest | Medium | Slowest of three |
| Type | SRAM | SRAM | SRAM |
| Split | Often split: I-cache + D-cache | Unified | Unified |

### Why cache is faster than RAM

| Reason | Cache (SRAM) | RAM (DRAM) |
|---|---|---|
| Technology | Flip-flops; no refresh needed | Capacitors; needs constant refresh |
| Physical location | On the CPU die | Separate chip on motherboard |
| Access path | Very short, wide bus | Longer bus, narrower |
| Refresh overhead | None | Periodic refresh cycles pause access |

### How cache improves CPU performance

1. **Cache hit:** CPU finds data in cache → retrieves in 1–4 cycles, not 200+.
2. **Temporal locality:** recently used data is likely needed again (loop counters, variables).
3. **Spatial locality:** nearby memory is likely needed next (array elements, instructions in sequence).
4. **Prefetching:** the cache controller predicts what data the CPU will need next and loads it before the request arrives.
5. **Modern hit rates:** well-written programs achieve > 95% L1 hit rates, meaning the CPU almost never waits for RAM.

---

## 2. Data Structures

### What is a data structure?

A data structure is a systematic way of organising and storing data in memory so that operations (insert, delete, search, sort) can be performed efficiently. The right choice of data structure can reduce an algorithm's time from hours to milliseconds.

### Linear vs Non-linear

| Feature | Linear | Non-linear |
|---|---|---|
| Arrangement | Sequential — one after another | Hierarchical or interconnected |
| Traversal | Single pass sufficient | Needs special traversal (BFS/DFS) |
| Memory | Usually contiguous | Not necessarily contiguous |
| Levels | Single level | Multiple levels |
| Examples | Array, Linked List, Stack, Queue | Tree, Graph, Heap |

```
LINEAR:   [10] → [20] → [30] → [40]   (array / linked list)

NON-LINEAR (tree):
              [10]
             /    \
           [20]  [30]
           /
         [40]
```

### Stack (LIFO)

A stack follows **Last In, First Out** — the last element inserted is the first removed.

**Operations:**
- `push(x)` — add x to top
- `pop()` — remove and return top
- `peek()` — view top without removing
- `isEmpty()` — check if empty

```
push(10) → push(20) → push(30)

    │ 30 │ ← TOP
    │ 20 │
    │ 10 │
    └────┘

pop() → returns 30; stack: [20, 10]
```

**Applications:** browser Back button, undo/redo, function call stack, balanced parentheses checking.

### Queue (FIFO)

A queue follows **First In, First Out** — the first element inserted is the first removed.

**Operations:**
- `enqueue(x)` — add x to rear
- `dequeue()` — remove from front
- `front()` — view front element
- `isEmpty()` — check if empty

```
enqueue(10), enqueue(20), enqueue(30)

FRONT → [10][20][30] ← REAR

dequeue() → returns 10; queue: [20][30]
```

**Applications:** CPU process scheduling, print spooler, network packet queuing, ticketing systems.

### Stack vs Queue

| Feature | Stack | Queue |
|---|---|---|
| Principle | LIFO | FIFO |
| Insert at | Top (`push`) | Rear (`enqueue`) |
| Remove from | Top (`pop`) | Front (`dequeue`) |
| Real example | Call stack | Printer queue |

---

## 3. SDLC — Software Development Life Cycle

### Definition

SDLC is a structured process that defines the stages for planning, building, testing, deploying, and maintaining software. It ensures software is developed systematically with high quality and within budget.

### The 7 phases

```
1. Planning ──► 2. Requirements ──► 3. Design ──► 4. Implementation
     ▲                                                     │
     │                                                     ▼
7. Maintenance ◄── 6. Deployment ◄── 5. Testing ◄─────────┘
```

| Phase | What happens | Output |
|---|---|---|
| 1. Planning | Scope, budget, timeline, feasibility study | Project plan |
| 2. Requirements | Gather what the software must do (functional + non-functional) | SRS document |
| 3. System Design | Architecture, database schema, UI mockups, module breakdown | HLD / LLD documents |
| 4. Implementation | Developers write code following design docs; use version control | Source code |
| 5. Testing | Find and fix bugs; unit, integration, system, UAT | Test reports |
| 6. Deployment | Release to production; user training | Live application |
| 7. Maintenance | Bug fixes, updates, new features post-launch | Patches, new versions |

### SDLC models

| Model | Characteristic | Best for |
|---|---|---|
| Waterfall | Sequential; each phase done before next | Fixed requirements, small projects |
| Agile | Iterative sprints; working software delivered often | Changing requirements |
| Spiral | Repeated loops with risk analysis | High-risk, large systems |
| V-Model | Each dev phase matched with a test phase | Safety-critical systems |

---

## 4. Flowcharts

### What is a flowchart?

A flowchart is a diagrammatic representation of an algorithm or process using standard symbols connected by arrows showing the flow of execution.

### Standard symbols

| Symbol | Shape | Meaning |
|---|---|---|
| Terminal | Oval / rounded rectangle | Start or Stop |
| Process | Rectangle | An action or calculation step |
| Decision | Diamond | A Yes/No question; branching point |
| Input/Output | Parallelogram | Read input or print output |
| Arrow | Line with arrowhead | Direction of flow |
| Connector | Circle | Connects parts of the chart on the same page |

### Example — Flowchart to check if a number is even or odd

```
    ┌───────────┐
    │   START   │
    └─────┬─────┘
          │
    ┌─────▼──────────────┐
    │ INPUT number N     │
    └─────┬──────────────┘
          │
    ┌─────▼──────────────┐
    │  Is N % 2 == 0?    │
    └─────┬──────────────┘
          │
    ┌─────┴──────┐
   YES           NO
    │             │
┌───▼──────┐  ┌──▼───────┐
│Print EVEN│  │Print ODD  │
└───┬──────┘  └──┬────────┘
    │             │
    └──────┬──────┘
           │
    ┌──────▼──────┐
    │    STOP     │
    └─────────────┘
```

---

## Q&A Bank

### True / False

**T1.** L1 cache is larger but slower than L2 cache.  
→ **False** — L1 is **smaller** and **faster** than L2.

**T2.** Cache uses SRAM technology, which is faster than DRAM used in RAM.  
→ **True**

**T3.** A stack follows the FIFO (First In, First Out) principle.  
→ **False** — A stack follows **LIFO**. A queue follows FIFO.

**T4.** In SDLC, testing comes before deployment.  
→ **True**

**T5.** A tree is an example of a linear data structure.  
→ **False** — A tree is a **non-linear** data structure.

**T6.** The Waterfall model supports iterative development.  
→ **False** — Waterfall is sequential; **Agile** is iterative.

---

### MCQ

**Q1.** Which cache level is located inside the CPU core and is the fastest?  
(a) L3  (b) L2  (c) L1  (d) RAM  
→ **(c)** L1

**Q2.** Cache memory uses which type of RAM?  
(a) DRAM  (b) SRAM  (c) SDRAM  (d) Flash  
→ **(b)** SRAM (Static RAM)

**Q3.** Which data structure would you use to implement a browser's Back button?  
(a) Queue  (b) Linked List  (c) Stack  (d) Graph  
→ **(c)** Stack (LIFO — the last page visited is the first to go back to)

**Q4.** Which data structure would you use to model CPU process scheduling?  
(a) Stack  (b) Queue  (c) Tree  (d) Hash Table  
→ **(b)** Queue (FIFO — first process in is first to be served)

**Q5.** In SDLC, which phase produces the Software Requirements Specification (SRS)?  
(a) Planning  (b) Requirements Analysis  (c) Design  (d) Testing  
→ **(b)** Requirements Analysis

**Q6.** Which SDLC model is best suited for projects with changing requirements?  
(a) Waterfall  (b) V-Model  (c) Agile  (d) Sequential  
→ **(c)** Agile

**Q7.** A diamond shape in a flowchart represents:  
(a) A process step  (b) Start or Stop  (c) Input/Output  (d) A decision  
→ **(d)** A decision (Yes/No branch)

---

### Common Traps

| Misconception | Correction |
|---|---|
| "Cache is part of RAM" | Cache is **separate** from RAM; it is SRAM on the CPU chip |
| "More cache always means better performance" | Cache helps only when data fits and locality is high; badly written code sees little benefit |
| "Stack and queue are the same since both are linear" | Linear structure type is the same, but the access order (LIFO vs FIFO) and use cases are completely different |
| "SDLC = Waterfall" | SDLC is a framework; Waterfall is one model that implements it |
| "Testing is the last phase of SDLC" | Testing comes before deployment; maintenance continues after deployment |
