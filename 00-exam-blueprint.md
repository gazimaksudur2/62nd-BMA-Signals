# Exam Blueprint — 62nd BMA Special Course (Signals / CSE)

## Overall structure

| Section | Marks | Qualifying | Time | Negative marking |
|---------|-------|-----------|------|-----------------|
| General Knowledge & Aptitude | 50 | 20–25 | 30 min | −0.5 per wrong MCQ (confirmed in at least one sitting) |
| Professional / Technical | 100 | 40 | 1 hour | None stated |

Both papers are sat on the same day. GK comes first.

---

## GK section — typical question types

| Type | Marks | Notes |
|------|-------|-------|
| Multiple choice | ~30 | Resistance/current, UN, national symbols, capitals … |
| Abbreviation expansion (5 items × 3 marks) | 15 | e.g. UNFPA, ISBN, a2i, WWW |
| Short write (national anthem, Bir Sreshtho list) | 5–10 | Awarded in some years, not all |

Total add up to 50. Pattern varies slightly; prepare for all three types.

---

## Technical section — two confirmed formats

### Format A — 54th BMA (closest modern CSE template)

| Part | Marks | Description |
|------|-------|-------------|
| Part A | 20 | 20 MCQ — networking concepts + C programming |
| Part B | 80 | 8–12 descriptive / program questions |

### Format B — 36th BMA (older template)

| Type | Marks |
|------|-------|
| True / False (10 statements × 2 marks) | 20 |
| Descriptive questions | 80 |

### Format C — 55th BMA

| Type | Marks |
|------|-------|
| MCQ | 40 |
| Written (3 out of 4 descriptive questions) | 60 |

**Prepare for all three formats.** The 62nd exam may mix them.

---

## High-frequency technical topics (ranked by past-paper appearances)

| Rank | Topic | Typical marks | Papers |
|------|-------|--------------|--------|
| 1 | OSI model / TCP/IP model | 10 | 36th, 49th, 54th, 55th |
| 2 | TCP vs UDP | 10 | 36th, 49th, 60th viva |
| 3 | Network topologies | 5–10 | 36th, 54th, 55th |
| 4 | ARP / RARP / DHCP | 5–10 | 54th, 55th, Medium prep |
| 5 | DNS (with diagram) | 5–10 | 54th |
| 6 | IPv4 vs IPv6 | 10–20 | 36th, 60th viva |
| 7 | C program (Fibonacci, factorial, case) | 10 | 54th, 55th |
| 8 | DES / Firewall | 5–10 | 54th, 55th |
| 9 | DBMS keys + functional dependency | 5–8 | 54th, 55th |
| 10 | Kernel | 5 | 54th, 55th, 60th viva |
| 11 | FDMA / TDMA | 10+10 | 36th |
| 12 | Subnetting (find network/broadcast IP) | 10 | 54th, 55th |

---

## Question formats you must practise

### True / False
A single statement; write "True" or "False" and optionally one line of justification.  
Example: *"UDP is a connection-oriented protocol."* → **False** (UDP is connectionless).

### MCQ
Four options (a)–(d). In negative-marking papers, skip if truly unsure.  
Example: *"ARP maps: (a) MAC→IP (b) IP→MAC (c) IP→port (d) domain→IP"* → **(b)**

### Descriptive / Short note (5 or 10 marks)
Recommended structure:
- **Definition** (1–2 sentences)
- **Key points / steps** (4–6 bullets or numbered list)
- **ASCII diagram** where natural (OSI stack, DNS hierarchy, DHCP flow)
- **Example** for DBMS topics

Budget: ~8 minutes per 10-mark answer.

### C program (10 marks)
Write working, compilable code. Use `#include <stdio.h>` and `int main(void)`.  
Do **not** use `#include <conio.h>`, `clrscr()`, or `void main()` — these are Turbo C extensions that examiners from modern universities may penalise.

---

## What to skip entirely

- Distributed DBMS, B-tree / hash index internals
- Full routing-protocol catalogs (OSPF details, BGP, EIGRP)
- AES internals, SHA specifics
- IoT protocols (Zigbee, Z-Wave, LoRaWAN)
- Electrical stream topics (op-amp, transformers) unless you are ECE-stream
