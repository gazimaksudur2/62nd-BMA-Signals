# 62nd BMA Special Course (Signals / CSE) — Actual Exam Questions & Model Answers

> **Source:** These are the actual descriptive questions from the 62nd BMA Special Course (Signals Corps / CSE) written examination. Each question carried **10 marks**. Use these as the highest-priority study material for future sittings.

---

## Question (a) — Cache Memory (10 marks)

**Q.** What is cache memory? Differentiate between L1, L2, and L3 cache memory. Why is cache memory faster than RAM/main memory? How does cache memory make CPU performance faster?

---

### Model Answer

**What is cache memory?**  
Cache memory is a small, extremely fast memory unit placed between the CPU and main memory (RAM). It stores copies of frequently accessed or recently used data and instructions so the CPU can retrieve them quickly without waiting for the slower RAM. Without cache, the CPU would stall every time it needed data, because RAM access time (∼60–100 ns) is much slower than CPU clock cycles (< 1 ns).

---

**L1, L2, and L3 Cache — Comparison**

| Feature | L1 Cache | L2 Cache | L3 Cache |
|---|---|---|---|
| Full name | Level 1 | Level 2 | Level 3 |
| Location | Inside CPU core (on-die) | Inside CPU core or very close | Shared across all cores, still on the chip |
| Size | 32 KB – 512 KB per core | 256 KB – 4 MB per core | 4 MB – 64 MB shared |
| Speed | Fastest (~1–4 clock cycles) | Medium (~5–15 clock cycles) | Slowest of the three (~30–60 clock cycles) |
| Access order | First to be checked | Checked if L1 misses | Checked if L2 misses |
| Cost | Most expensive per bit | Moderate | Relatively cheaper per bit |

**Access hierarchy:**
```
CPU Core
  │
  ├──► L1 Cache  (hit? → return data instantly)
  │       │ miss
  ├──► L2 Cache  (hit? → return data in ~10 cycles)
  │       │ miss
  ├──► L3 Cache  (hit? → return data in ~40 cycles)
  │       │ miss
  └──► RAM (main memory) (~200+ cycles)
                │ miss
          Storage / Virtual Memory (millions of cycles)
```

---

**Why is cache memory faster than RAM?**

1. **Technology:** Cache uses SRAM (Static RAM) which stores data in flip-flops (no refresh needed). RAM uses DRAM (Dynamic RAM) which stores data in capacitors and must be continuously refreshed — a slower process.
2. **Physical proximity:** Cache is embedded directly on the CPU chip (L1/L2) or very close to it (L3), so electrical signals travel a shorter distance.
3. **Width and bandwidth:** Cache has a wider bus to the CPU, allowing more data transfer per clock cycle.
4. **No refresh overhead:** SRAM does not need to pause for refresh cycles, unlike DRAM.

---

**How cache memory improves CPU performance**

1. **Reduces latency (cache hit):** When the CPU finds the data it needs in cache (a *cache hit*), it retrieves it in 1–4 cycles instead of ∼200 cycles from RAM. Modern programs achieve >95% hit rates.
2. **Exploits locality of reference:**
   - *Temporal locality:* recently accessed data is likely to be accessed again soon (loop variables).
   - *Spatial locality:* data near recently accessed memory is likely to be needed next (arrays).
3. **Enables higher CPU clock speeds:** Without cache, CPUs would spend most of their time waiting for RAM (the "memory wall"). Cache removes this bottleneck.
4. **Instruction cache (I-cache):** Stores frequently executed instructions so the CPU does not re-fetch them from RAM.
5. **Data cache (D-cache):** Stores data operands; L1 is usually split into separate I-cache and D-cache for parallel access.

**In summary:** Cache memory acts as a high-speed buffer that feeds the CPU with data at near-processor speed, dramatically reducing the time the CPU wastes waiting for main memory.

---

## Question (b) — Flowchart: Smart Parking System (10 marks)

**Q.** Draw a flowchart for a smart parking system.

---

### Model Answer

**System description:** A smart parking system detects whether a parking slot is available when a vehicle arrives, assigns a slot, tracks occupancy, and releases the slot when the vehicle leaves.

```
           ┌─────────────────────┐
           │        START        │
           └──────────┬──────────┘
                      │
           ┌──────────▼──────────┐
           │  Vehicle arrives at │
           │  entrance sensor    │
           └──────────┬──────────┘
                      │
           ┌──────────▼──────────┐
           │  Is any parking     │
           │  slot available?    │
           └──────────┬──────────┘
                      │
          ┌───────────┴───────────┐
         YES                      NO
          │                        │
┌─────────▼──────────┐  ┌──────────▼──────────┐
│ Display slot number│  │ Display "Parking     │
│ and open entry gate│  │  Full" message       │
└─────────┬──────────┘  └──────────┬──────────┘
          │                        │
┌─────────▼──────────┐  ┌──────────▼──────────┐
│ Vehicle enters and │  │ Redirect vehicle     │
│ parks in slot      │  │ or wait in queue     │
└─────────┬──────────┘  └──────────┬──────────┘
          │                        │
┌─────────▼──────────┐             │ (loop back)
│ Update slot status │─────────────┘
│ → OCCUPIED         │
│ Decrement counter  │
└─────────┬──────────┘
          │
┌─────────▼──────────┐
│  Vehicle ready to  │
│  exit? (sensor)    │
└─────────┬──────────┘
          │ YES
┌─────────▼──────────┐
│ Calculate parking  │
│ duration and fee   │
└─────────┬──────────┘
          │
┌─────────▼──────────┐
│ Process payment    │
│ (cash / card / app)│
└─────────┬──────────┘
          │ Payment confirmed
┌─────────▼──────────┐
│ Open exit gate     │
│ Update slot status │
│ → AVAILABLE        │
│ Increment counter  │
└─────────┬──────────┘
          │
┌─────────▼──────────┐
│  More vehicles to  │
│  process?          │
└─────────┬──────────┘
          │YES           NO
          │◄─────────────┘
          │                      ┌──────────┐
          └──────────────────────►   STOP   │
                                 └──────────┘
```

**Flowchart symbols used:**

| Shape | Meaning |
|---|---|
| Rectangle | Process step |
| Diamond | Decision (Yes/No) |
| Rounded rectangle | Start / Stop (terminal) |
| Arrow | Flow direction |

**Key logic points for 10-mark answer:**
- Entry sensor detects vehicle arrival
- Availability check (decision diamond)
- Slot assignment and gate control
- Occupancy counter update (increment/decrement)
- Exit detection, fee calculation, payment, gate release
- Loop: system remains active for next vehicle

---

## Question (c) — Data Structures: Linear vs Non-linear, Stack, Queue (10 marks)

**Q.** What is a data structure? Differentiate between linear and non-linear data structures. Explain with examples: Stack and Queue.

---

### Model Answer

**What is a data structure?**  
A data structure is a systematic way of organising, storing, and managing data in computer memory so that it can be accessed and modified efficiently. The choice of data structure directly affects the performance of an algorithm.

Examples: Array, Linked List, Stack, Queue, Tree, Graph, Hash Table.

---

**Linear vs Non-linear Data Structures**

| Feature | Linear | Non-linear |
|---|---|---|
| Arrangement | Elements in a sequence (one after another) | Elements in a hierarchical or interconnected structure |
| Traversal | Easily traversable in a single run | Requires special traversal (BFS, DFS) |
| Memory use | Often stored in contiguous memory | Not necessarily contiguous |
| Levels | Single level | Multiple levels |
| Examples | Array, Linked List, Stack, Queue | Tree, Graph, Heap |
| Complexity | Simpler to implement | More complex |

**Memory layout comparison:**
```
LINEAR (array):    [10] → [20] → [30] → [40] → [50]
                    ↑  sequential, one path

NON-LINEAR (tree):        [10]
                         /    \
                       [20]  [30]
                       /  \
                     [40] [50]
                    multiple paths, hierarchical
```

---

**Stack**

A **stack** is a linear data structure that follows the **LIFO** principle — **Last In, First Out**. The element inserted last is removed first, like a stack of plates.

**Operations:**
- `push(x)` — insert element x at the top
- `pop()` — remove and return the top element
- `peek()` — view the top element without removing
- `isEmpty()` — check if stack is empty

**Visual example:**
```
After push(10), push(20), push(30):

    │ 30 │  ← TOP (last in, first out)
    │ 20 │
    │ 10 │
    └────┘

pop() returns 30 → stack becomes: [20, 10]
pop() returns 20 → stack becomes: [10]
```

**Real-world uses:**
- Browser **Back** button (history stack)
- Undo function in text editors
- Function call stack in programming
- Expression evaluation (e.g. checking balanced parentheses)

---

**Queue**

A **queue** is a linear data structure that follows the **FIFO** principle — **First In, First Out**. The element inserted first is removed first, like a queue of people at a counter.

**Operations:**
- `enqueue(x)` — insert element x at the rear
- `dequeue()` — remove and return element from the front
- `front()` — view the front element
- `isEmpty()` — check if queue is empty

**Visual example:**
```
Enqueue 10, 20, 30:

FRONT → [10] [20] [30] ← REAR

dequeue() returns 10 → FRONT → [20] [30] ← REAR
dequeue() returns 20 → FRONT → [30] ← REAR
```

**Real-world uses:**
- **CPU scheduling** (process queue)
- Print spooler (jobs print in order received)
- Network packet queuing
- Ticket booking systems

---

**Stack vs Queue — Summary**

| Feature | Stack | Queue |
|---|---|---|
| Principle | LIFO (Last In First Out) | FIFO (First In First Out) |
| Insertion | At the top (`push`) | At the rear (`enqueue`) |
| Deletion | From the top (`pop`) | From the front (`dequeue`) |
| Example | Call stack, undo history | Print queue, scheduling |

---

## Question (d) — OSI Model (10 marks)

**Q.** Write the OSI model layers and briefly describe their functions with examples.

---

### Model Answer

The **OSI (Open Systems Interconnection)** model is a conceptual framework that standardises the functions of a communication system into **7 distinct layers**. Each layer has a specific role and communicates with the layer directly above and below it.

```
Layer 7  ┌──────────────────────────────────────────────────┐
         │ APPLICATION     User-facing network services      │
         │ Protocols: HTTP(80), FTP(21), SMTP(25), DNS(53)   │
Layer 6  ├──────────────────────────────────────────────────┤
         │ PRESENTATION    Data format, encryption, compress │
         │ Protocols: SSL/TLS, JPEG, MPEG                    │
Layer 5  ├──────────────────────────────────────────────────┤
         │ SESSION         Establish, manage, close sessions │
         │ Protocols: NetBIOS, RPC, PPTP                     │
Layer 4  ├──────────────────────────────────────────────────┤
         │ TRANSPORT       End-to-end delivery, flow control │
         │ Protocols: TCP (reliable), UDP (fast)             │
Layer 3  ├──────────────────────────────────────────────────┤
         │ NETWORK         Logical addressing and routing    │
         │ Protocols: IP, ICMP, ARP   Devices: Routers       │
Layer 2  ├──────────────────────────────────────────────────┤
         │ DATA LINK       MAC addressing, framing, CRC      │
         │ Protocols: Ethernet, PPP   Devices: Switches      │
Layer 1  ├──────────────────────────────────────────────────┤
         │ PHYSICAL        Raw bits on cables/radio          │
         │ Media: Copper cable, fibre, radio  Devices: Hubs  │
         └──────────────────────────────────────────────────┘
```

**Layer-by-layer description:**

| # | Layer | Function | Protocol/Device example |
|---|---|---|---|
| 7 | Application | Provides network services directly to user applications (web browsing, email, file transfer) | HTTP, HTTPS, FTP, DNS, SMTP |
| 6 | Presentation | Translates data formats between application and network; handles encryption/decryption and compression | SSL/TLS, JPEG, ASCII, MPEG |
| 5 | Session | Establishes, maintains, and terminates communication sessions between applications | NetBIOS, RPC |
| 4 | Transport | Provides end-to-end communication; TCP gives reliable ordered delivery; UDP gives fast best-effort delivery; manages port numbers | TCP, UDP |
| 3 | Network | Handles logical (IP) addressing and routes packets across multiple networks | IP, ICMP, ARP; Routers |
| 2 | Data Link | Packages bits into frames; uses MAC addresses for delivery on the local network; performs error detection (CRC) | Ethernet (802.3), PPP; Switches |
| 1 | Physical | Transmits raw binary bits (0s and 1s) over a physical medium (copper wire, fibre optic, radio wave) | Hubs, cables, repeaters |

**Memory aid (top → bottom):** "All People Seem To Need Data Processing"

**How data travels (encapsulation):**
When you load a webpage, data travels down through all 7 layers at the sender (adding a header at each layer), across the network, then back up through all 7 layers at the receiver (stripping each header).

---

## Question (e) — C Program: Employee Salary and Bonus (10 marks)

**Q.** Write a complete C program that:
- Takes an **Employee ID** (integer)
- Takes a **Base Salary** (integer)
- Calculates a **Bonus** based on:
  - 10% if base salary < 20,000
  - 15% if base salary ≥ 20,000 and < 40,000
  - 20% if base salary ≥ 40,000
- Outputs the **bonus value** and **gross salary**

---

### Model Answer

```c
#include <stdio.h>

int main(void) {
    int    emp_id;
    int    base_salary;
    double bonus_rate;
    double bonus;
    double gross_salary;

    /* Input */
    printf("Enter Employee ID     : ");
    scanf("%d", &emp_id);

    printf("Enter Base Salary (Tk): ");
    scanf("%d", &base_salary);

    /* Validate: salary must be positive */
    if (base_salary <= 0) {
        printf("Error: Base salary must be a positive value.\n");
        return 1;
    }

    /* Determine bonus rate based on salary slab */
    if (base_salary < 20000) {
        bonus_rate = 0.10;   /* 10% */
    } else if (base_salary < 40000) {
        bonus_rate = 0.15;   /* 15% */
    } else {
        bonus_rate = 0.20;   /* 20% */
    }

    /* Calculate bonus and gross salary */
    bonus        = base_salary * bonus_rate;
    gross_salary = base_salary + bonus;

    /* Output */
    printf("\n--- Salary Statement ---\n");
    printf("Employee ID   : %d\n",   emp_id);
    printf("Base Salary   : Tk %d\n", base_salary);
    printf("Bonus Rate    : %.0f%%\n", bonus_rate * 100);
    printf("Bonus Amount  : Tk %.2f\n", bonus);
    printf("Gross Salary  : Tk %.2f\n", gross_salary);

    return 0;
}
```

**Sample outputs:**

```
--- Run 1 ---
Enter Employee ID     : 1021
Enter Base Salary (Tk): 15000

--- Salary Statement ---
Employee ID   : 1021
Base Salary   : Tk 15000
Bonus Rate    : 10%
Bonus Amount  : Tk 1500.00
Gross Salary  : Tk 16500.00

--- Run 2 ---
Enter Employee ID     : 1045
Enter Base Salary (Tk): 32000

--- Salary Statement ---
Employee ID   : 1045
Base Salary   : Tk 32000
Bonus Rate    : 15%
Bonus Amount  : Tk 4800.00
Gross Salary  : Tk 36800.00

--- Run 3 ---
Enter Employee ID     : 1099
Enter Base Salary (Tk): 55000

--- Salary Statement ---
Employee ID   : 1099
Base Salary   : Tk 55000
Bonus Rate    : 20%
Bonus Amount  : Tk 11000.00
Gross Salary  : Tk 66000.00
```

**Logic breakdown (for descriptive marks):**

| Condition | Bonus rate | Example (salary=15000) |
|---|---|---|
| `base_salary < 20000` | 10% | 15000 × 0.10 = 1500 |
| `base_salary >= 20000 && < 40000` | 15% | 32000 × 0.15 = 4800 |
| `base_salary >= 40000` | 20% | 55000 × 0.20 = 11000 |

**Key C concepts used:**
- `scanf` / `printf` for I/O
- `if-else if-else` for conditional salary slab selection
- `double` for bonus to preserve decimal values
- Input validation (negative salary check)

---

## Question (f) — SDLC (10 marks)

**Q.** What do you understand by SDLC? Explain how it is utilised in software development.

---

### Model Answer

**What is SDLC?**  
SDLC stands for **Software Development Life Cycle**. It is a structured, systematic process (or methodology) that defines the stages involved in planning, creating, testing, deploying, and maintaining a software application. It provides a framework that guides development teams to produce high-quality software in a predictable, cost-effective, and timely manner.

SDLC is not a single method — it is a framework that various methodologies (Waterfall, Agile, Spiral, etc.) implement.

---

**Phases of the SDLC**

```
┌──────────────────────────────────────────────────────────────┐
│                    SOFTWARE DEVELOPMENT LIFE CYCLE           │
│                                                              │
│   1. Planning ──► 2. Requirements ──► 3. System Design      │
│        ▲                                      │              │
│        │                                      ▼              │
│   7. Maintenance ◄── 6. Deployment ◄── 5. Testing           │
│                                              ▲               │
│                                              │               │
│                                    4. Implementation ────────┘
└──────────────────────────────────────────────────────────────┘
```

**Phase-by-phase explanation:**

**1. Planning**
- Defines the project scope, purpose, timeline, and budget.
- Feasibility study: is the project technically possible and financially viable?
- Output: Project Plan, Feasibility Report.
- *Example:* Deciding to build a Smart Parking System app; estimating 6 months and 5 developers.

**2. Requirements Analysis**
- Gather and document what the software must do (functional requirements) and how it must perform (non-functional requirements like speed, security).
- Involves stakeholder interviews and workshops.
- Output: Software Requirements Specification (SRS) document.
- *Example:* "The system must detect available parking slots in real-time and support 100 concurrent users."

**3. System Design**
- Translate requirements into architecture and design blueprints.
- Covers database design (ER diagrams), system architecture (client-server), UI mockups, and module structure.
- Output: High-Level Design (HLD) and Low-Level Design (LLD) documents.
- *Example:* Designing the database schema for slot occupancy; designing the sensor API interface.

**4. Implementation (Coding)**
- Developers write source code based on the design documents.
- Follows coding standards; uses version control (e.g. Git).
- Output: Source code, build artifacts.
- *Example:* Writing the C program for salary calculation or the sensor data handler in Python.

**5. Testing**
- The software is tested to find and fix bugs and verify it meets requirements.
- Types: unit testing, integration testing, system testing, user acceptance testing (UAT).
- Output: Test reports, bug-fix patches.
- *Example:* Testing that the parking system correctly marks a slot as occupied when a vehicle parks.

**6. Deployment**
- The tested software is released to the production environment for end users.
- May involve phased rollout or parallel running with the old system.
- Output: Deployed application, deployment manual.
- *Example:* Installing the smart parking app on the parking facility's hardware.

**7. Maintenance**
- After deployment, the software is monitored and updated to fix bugs, improve performance, or add new features.
- Corrective, adaptive, perfective, and preventive maintenance types.
- Output: Updated versions, patch releases.
- *Example:* Adding support for a new payment gateway after launch.

---

**How SDLC is utilised in software development**

1. **Structured approach:** Breaks a large, complex project into manageable phases, reducing chaos.
2. **Quality control:** Testing phase ensures bugs are caught before deployment; requirements phase ensures the right product is built.
3. **Cost estimation:** Planning and requirements phases allow realistic budget and timeline forecasting.
4. **Risk management:** Identifying risks early (feasibility study) prevents costly surprises late in the project.
5. **Team coordination:** Clear phase boundaries let different teams (analysts, developers, testers) work in parallel without confusion.
6. **Documentation:** Each phase produces deliverables that serve as communication records and future maintenance guides.

**Popular SDLC models:**

| Model | Best for | Key characteristic |
|---|---|---|
| Waterfall | Fixed requirements, small projects | Sequential — each phase completes before the next starts |
| Agile | Changing requirements | Iterative sprints; working software delivered frequently |
| Spiral | High-risk, large systems | Combines Waterfall and prototyping with risk analysis at each loop |
| V-Model | Safety-critical systems | Each development phase has a corresponding test phase |
