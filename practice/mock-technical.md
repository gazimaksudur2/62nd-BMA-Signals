# Mock Technical Paper — 100 Marks, 1 Hour

> **Instructions:** This paper follows the 54th BMA format (Part A: 20 MCQ, Part B: 80 descriptive). Set a timer for **60 minutes**. Complete Part A first (aim for ~12 minutes), then Part B. Answer key with model answers is at the end — do not read until you finish.

---

## PART A — Multiple Choice (20 marks, 1 mark each)

Circle the correct option for each question.

**1.** How many layers does the OSI model have?  
(a) 4  (b) 5  (c) 6  (d) 7

**2.** ARP maps:  
(a) MAC → IP  (b) IP → MAC  (c) IP → port  (d) domain → IP

**3.** Which protocol automatically assigns IP addresses?  
(a) ARP  (b) DNS  (c) DHCP  (d) RARP

**4.** TCP uses which connection mechanism?  
(a) 2-way handshake  (b) 3-way handshake  (c) 4-way handshake  (d) None

**5.** SSH operates on port:  
(a) 20  (b) 22  (c) 23  (d) 25

**6.** A router operates at which OSI layer?  
(a) Layer 1  (b) Layer 2  (c) Layer 3  (d) Layer 4

**7.** IPv6 addresses are how many bits?  
(a) 32  (b) 64  (c) 128  (d) 256

**8.** Which of the following is NOT a network topology?  
(a) Bus  (b) Ring  (c) Diamond  (d) Mesh

**9.** DES uses a key size of:  
(a) 32 bits  (b) 56 bits  (c) 128 bits  (d) 256 bits

**10.** What does DHCP stand for?  
(a) Dynamic Host Configuration Protocol  
(b) Data Host Control Protocol  
(c) Dynamic HTTP Configuration Protocol  
(d) Direct Host Control Program

**11.** Which SQL function returns the largest value in a column?  
(a) `SUM`  (b) `COUNT`  (c) `MAX`  (d) `AVG`

**12.** Which OOP concept allows a child class to inherit from a parent class?  
(a) Encapsulation  (b) Polymorphism  (c) Abstraction  (d) Inheritance

**13.** The kernel runs in:  
(a) User mode  (b) Kernel mode  (c) Safe mode  (d) Application mode

**14.** The following C loop computes what?  
```
while (m != n) { if (m > n) m = m-n; else n = n-m; }
```  
(a) LCM  (b) x mod y  (c) GCD  (d) x + y

**15.** WiMAX is defined by IEEE standard:  
(a) 802.3  (b) 802.11  (c) 802.15  (d) 802.16

**16.** FDMA divides access by:  
(a) Time  (b) Code  (c) Frequency  (d) Amplitude

**17.** Which of the following is a symmetric encryption algorithm?  
(a) RSA  (b) DES  (c) DSA  (d) ECC

**18.** The first step of the DHCP process is:  
(a) Offer  (b) Request  (c) Acknowledge  (d) Discover

**19.** A candidate key is:  
(a) Any set of attributes that uniquely identifies a row  
(b) A minimal set of attributes that uniquely identifies a row  
(c) The same as a foreign key  
(d) An attribute that can be NULL

**20.** Which attack floods a target with traffic from many machines?  
(a) Phishing  (b) SQL injection  (c) DDoS  (d) Man-in-the-middle

---

## PART B — Descriptive (80 marks)

*Answer any **6** of the following 8 questions. Each question is worth approximately 13 marks. Show structure: definition → key points → diagram where applicable.*

---

**B1.** Write the OSI model layers and describe the function of each layer. (13 marks)

**B2.** What is DHCP? Explain its four-step process (DORA) with a diagram. (13 marks)

**B3.** What is DNS? Illustrate the DNS resolution process with a diagram. (13 marks)

**B4.** (a) Define primary key and candidate key with examples. (7 marks)  
(b) Explain functional dependency and give one example of a transitive dependency. (6 marks)

**B5.** (a) What is DES? State its key parameters and how it encrypts data. (8 marks)  
(b) What is a Firewall? Name two types and explain one. (5 marks)

**B6.** Write the following C programs: (13 marks)  
(a) Print the Fibonacci series for the first n terms. (7 marks)  
(b) Convert a string from lowercase to uppercase. (6 marks)

**B7.** (a) What is the Kernel? List its five main functions. (7 marks)  
(b) What is OOP? Define any three of its four pillars. (6 marks)

**B8.** (a) What is FDMA? Give two advantages and two disadvantages. (7 marks)  
(b) Write the Shannon–Hartley theorem and explain its significance. (6 marks)

---

---

# ANSWER KEY — Part A

| Q | Answer | Q | Answer |
|---|---|---|---|
| 1 | (d) 7 | 11 | (c) MAX |
| 2 | (b) IP → MAC | 12 | (d) Inheritance |
| 3 | (c) DHCP | 13 | (b) Kernel mode |
| 4 | (b) 3-way handshake | 14 | (c) GCD |
| 5 | (b) 22 | 15 | (d) 802.16 |
| 6 | (c) Layer 3 | 16 | (c) Frequency |
| 7 | (c) 128 | 17 | (b) DES |
| 8 | (c) Diamond | 18 | (d) Discover |
| 9 | (b) 56 bits | 19 | (b) Minimal set |
| 10 | (a) Dynamic Host Configuration Protocol | 20 | (c) DDoS |

---

# ANSWER KEY — Part B (Model answers)

## B1 — OSI Model (13 marks)

See `technical/01-networking.md` → Section 1.

**Marking guide:** 1 mark per layer name + 1 mark per function = 14 marks; any 13 accepted.

Layers (bottom to top):
1. Physical — raw bits, cables, signals. Devices: hubs, cables.
2. Data Link — MAC addressing, framing, error detection. Devices: switches.
3. Network — logical addressing, routing. Protocol: IP. Devices: routers.
4. Transport — end-to-end delivery; TCP (reliable) or UDP (fast). Flow and error control.
5. Session — manages sessions (open/maintain/terminate). NetBIOS, RPC.
6. Presentation — encryption, compression, data format translation. SSL/TLS.
7. Application — user-level services. HTTP, FTP, DNS, SMTP.

---

## B2 — DHCP (13 marks)

Definition: DHCP automatically assigns IP address, subnet mask, gateway, DNS server, and lease time to devices. (2 marks)

Four steps DORA: (4 × 2 = 8 marks)
1. Discover — client broadcasts DHCPDISCOVER
2. Offer — server replies DHCPOFFER with candidate IP
3. Request — client broadcasts DHCPREQUEST accepting offer
4. Acknowledge — server sends DHCPACK confirming lease

Diagram showing broadcast arrows between client and server (3 marks)

---

## B3 — DNS (13 marks)

Definition + hierarchy (4 marks): Root → TLD → Second-level → Subdomain. UDP port 53.

Resolution steps (6 marks):
1. Check local cache
2. Query recursive resolver (ISP)
3. Resolver asks root server
4. Root refers to TLD server
5. TLD refers to authoritative server
6. Authoritative returns IP; result cached

Diagram (3 marks)

---

## B4 — DBMS Keys and FD (13 marks)

**(a) Primary vs candidate key (7 marks)**
- Candidate key: minimal set of attributes uniquely identifying a row (2 marks)
- Primary key: the one selected candidate key; must be NOT NULL and UNIQUE (2 marks)
- Example with Student table showing two candidates, one chosen as PK (3 marks)

**(b) Functional dependency + transitive example (6 marks)**
- FD definition: X → Y means knowing X determines Y (2 marks)
- Example: Employee(EmpID, DeptID, DeptName) — EmpID → DeptID → DeptName is transitive (2 marks)
- Explain violation and fix: split into Employee(EmpID, DeptID) and Department(DeptID, DeptName) (2 marks)

---

## B5 — DES and Firewall (13 marks)

**(a) DES (8 marks)**
- Full name: Data Encryption Standard; symmetric block cipher (2 marks)
- Key: 56 bits; Block: 64 bits; Rounds: 16 (3 marks)
- Feistel structure, initial permutation → 16 rounds → final permutation (3 marks)

**(b) Firewall (5 marks)**
- Definition: monitors/controls network traffic by rules (2 marks)
- Types: packet-filtering and stateful inspection defined (2 marks)
- One type explained in detail (1 mark)

---

## B6 — C Programs (13 marks)

**(a) Fibonacci — 7 marks**
```c
#include <stdio.h>
int main(void) {
    int n, a = 0, b = 1, next;
    scanf("%d", &n);
    for (int i = 0; i < n; i++) {
        printf("%d ", a);
        next = a + b; a = b; b = next;
    }
    return 0;
}
```
Marks: correct includes (1), correct logic a+b (2), correct loop (2), correct output (2).

**(b) Lowercase to uppercase — 6 marks**
```c
#include <stdio.h>
int main(void) {
    char s[100];
    scanf("%s", s);
    for (int i = 0; s[i] != '\0'; i++)
        if (s[i] >= 'a' && s[i] <= 'z')
            s[i] -= 32;
    printf("%s\n", s);
    return 0;
}
```
Marks: null-check loop (2), ASCII subtraction logic (2), correct output (2).

---

## B7 — Kernel and OOP (13 marks)

**(a) Kernel — 7 marks**
- Definition + kernel/user mode distinction (2 marks)
- 5 functions: process, memory, device, file system, system calls — 1 mark each (5 marks)

**(b) OOP — 6 marks**
- Brief definition of OOP (1 mark)
- Any three pillars, 1.5 marks each: definition + example (4.5 → round to 5 marks)

---

## B8 — FDMA and Shannon–Hartley (13 marks)

**(a) FDMA — 7 marks**
- Definition: separate frequency bands per user (2 marks)
- 2 advantages (2 marks): simple, no synchronisation
- 2 disadvantages (2 marks): wasteful when idle, limited capacity
- Diagram of frequency bands (1 mark)

**(b) Shannon–Hartley — 6 marks**
- Formula: C = B × log₂(1 + S/N) (2 marks)
- Each variable defined (2 marks)
- Significance: fundamental upper bound; motivates modern techniques (2 marks)
