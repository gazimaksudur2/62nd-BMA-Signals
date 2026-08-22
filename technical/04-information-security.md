# Information Security — Technical Study Notes

> **Why it is asked:** DES and Firewall appear as 5–10 mark questions in the 54th and 55th BMA papers. Phishing and DDoS are confirmed 60th BMA viva topics and are useful T/F material. SQL injection appeared in the 55th paper.

---

## 1. DES — Data Encryption Standard

> **Note on naming:** The exam papers write "Digital Encryption System (DES)" — this is informal/incorrect terminology. The correct full name is **Data Encryption Standard**. Both are acceptable in the exam context; know the correct name as well.

**What it is:** DES is a symmetric-key block cipher published by NIST in 1977. It was the US federal standard for encryption until it was replaced by AES (Advanced Encryption Standard) in 2001.

**Key parameters:**
- **Key size:** 56 bits (+ 8 parity bits = 64 bits total)
- **Block size:** 64 bits
- **Number of rounds:** 16
- **Structure:** Feistel network

**How DES works (simplified):**
```
Plaintext (64 bits)
      │
  Initial Permutation (IP)
      │
  ┌───┴───────────────────────────┐
  │  16 Rounds (Feistel rounds)   │
  │  Each round uses a 48-bit     │
  │  subkey derived from the 56-  │
  │  bit master key               │
  └───────────────────────────────┘
      │
  Final Permutation (IP⁻¹)
      │
  Ciphertext (64 bits)
```

**Symmetric vs Asymmetric encryption:**

| Feature | Symmetric | Asymmetric |
|---|---|---|
| Key count | 1 key (same for encrypt/decrypt) | 2 keys (public + private) |
| Speed | Fast | Slow |
| Key distribution | Difficult (key must be shared securely) | Easy (public key shared freely) |
| Examples | DES, AES, 3DES | RSA, ECC, DSA |
| Typical use | Bulk data encryption | Key exchange, digital signatures |

**Why DES is weak today:** 56-bit key → only 2^56 ≈ 72 quadrillion combinations, which modern hardware can brute-force in hours. **3DES** (Triple DES) applies DES three times. Replaced by **AES-128/256** in practice.

---

## 2. Firewall

**Definition:** A firewall is a network security device (hardware or software) that monitors and controls incoming and outgoing network traffic based on predefined security rules. It acts as a barrier between a trusted internal network and an untrusted external network (Internet).

**Types:**

| Type | How it works |
|---|---|
| **Packet filter** | Inspects each packet's IP/port headers; allows or blocks based on rules |
| **Stateful inspection** | Tracks active connections; allows packets only if they belong to an established session |
| **Application (proxy)** | Deep packet inspection at Layer 7; understands application protocols (HTTP, FTP) |
| **Next-generation (NGFW)** | Combines all above + intrusion detection, SSL inspection, application awareness |

**How a firewall rule works:**
```
Incoming packet: src=203.x.x.1:1234, dst=10.0.0.5:80
Rule: ALLOW any → 10.0.0.5:80 (HTTP traffic)
      DENY  any → 10.0.0.5:22 (block SSH from outside)
→ packet to port 80 is allowed; packet to port 22 is dropped
```

---

## 3. Phishing

**Definition:** Phishing is a social engineering attack in which an attacker impersonates a trusted entity (bank, government, company) via email, SMS, or a fake website to trick the victim into revealing sensitive information (passwords, credit card numbers) or installing malware.

**Common types:**
- **Email phishing:** Fake email from "your bank" with a link to a fake login page.
- **Spear phishing:** Targeted at a specific individual or organisation.
- **Smishing:** Phishing via SMS.

**Defence:** Verify sender addresses, never click suspicious links, use multi-factor authentication (MFA).

---

## 4. DDoS — Distributed Denial of Service

**Definition:** A DDoS attack floods a target server or network with traffic from many compromised machines (a *botnet*) simultaneously, exhausting resources and making the service unavailable to legitimate users.

**How it differs from DoS (Denial of Service):**
- **DoS:** Single attacker / machine → target.
- **DDoS:** Many machines (botnet) → target simultaneously. Much harder to block.

**Mitigation:** Traffic filtering, rate limiting, CDN load distribution, scrubbing centres.

---

## 5. SQL Injection

**Definition:** SQL injection is an attack where malicious SQL code is inserted into input fields to manipulate backend queries, allowing attackers to bypass security, access, or modify data.

**Example:**
*   **Input:** `' OR '1'='1' --`
*   **Resulting Query:** `SELECT * FROM users WHERE username='admin' OR '1'='1' --' AND password='...'`
*   **Impact:** The `'1'='1'` condition is always true, and `--` comments out the password check. The attacker successfully bypasses authentication.

**Prevention:**
*   **Parameterized Queries (Prepared Statements):** Treat input strictly as data, not executable code.
*   **Input Validation:** Sanitize and restrict inputs to expected formats.
*   **Principle of Least Privilege:** Limit database account permissions to the bare minimum.
  
---

## Q&A Bank

### True / False

**T1.** DES uses a 56-bit key and processes data in 64-bit blocks.  
→ **True**

**T2.** DES is an asymmetric encryption algorithm.  
→ **False** (DES is a **symmetric** cipher — the same key is used to encrypt and decrypt.)

**T3.** A firewall can completely prevent all cyber attacks.  
→ **False** (A firewall filters traffic by rules but cannot protect against insider threats, zero-day exploits, or application-layer attacks it is not configured for.)

**T4.** In a DDoS attack, the traffic originates from a single machine.  
→ **False** (DDoS uses *distributed* sources — a botnet of many machines. A single machine is a simple DoS.)

**T5.** Phishing is a type of social engineering attack.  
→ **True**

**T6.** SQL injection inserts malicious SQL code via user input fields.  
→ **True**

---

### MCQ

**Q1.** How many rounds does DES perform during encryption?  
(a) 8  (b) 10  (c) 16  (d) 32  
→ **(c)** 16

**Q2.** Which type of encryption uses a single key for both encryption and decryption?  
(a) Asymmetric  (b) Hash  (c) Symmetric  (d) Public-key  
→ **(c)** Symmetric

**Q3.** A firewall primarily operates at which OSI layers?  
(a) Layers 1–2  (b) Layers 3–4 (and Layer 7 for NGFW)  (c) Layer 6 only  (d) Layer 5 only  
→ **(b)**

**Q4.** DDoS stands for:  
(a) Data Denial of Service  (b) Distributed Denial of Service  (c) Direct Denial of Service  (d) Dynamic Denial of Service  
→ **(b)**

**Q5.** Which of the following best prevents SQL injection?  
(a) Using a firewall  (b) Using parameterised queries  (c) Increasing password length  (d) Using HTTPS  
→ **(b)**

---

### Descriptive Q&A

**Q.** What is DES (Digital Encryption System / Data Encryption Standard)? Explain. (10 marks)

**A.**  
DES, formally the **Data Encryption Standard**, is a symmetric-key block cipher standardised by the US National Institute of Standards and Technology (NIST) in 1977. "Symmetric" means the *same key* is used for both encryption and decryption.

**Key parameters:**
- Key size: **56 bits** (effective) + 8 parity bits = 64 bits total
- Block size: **64 bits**
- Number of rounds: **16 Feistel rounds**

**How it works:**
1. The 64-bit plaintext block undergoes an **Initial Permutation (IP)**.
2. The block is split into two 32-bit halves: Left (L) and Right (R).
3. **16 rounds** of Feistel operations are performed. In each round:
   - Right half is expanded to 48 bits.
   - XOR-ed with a 48-bit round subkey (derived from the 56-bit master key).
   - Passed through S-boxes (substitution) → 32 bits.
   - Passed through a P-box (permutation).
   - XOR-ed with the Left half → becomes new Right; old Right becomes new Left.
4. After 16 rounds, a **Final Permutation (IP⁻¹)** produces the 64-bit ciphertext.

**Weakness:** The 56-bit key is too short by modern standards; it was broken by brute force in 1998 in under 23 hours. **3DES** (Triple DES) applies DES three times as a workaround. DES was replaced by **AES** (2001) as the federal standard.

**Symmetric vs Asymmetric:**
- Symmetric (e.g. DES, AES): one key, fast, used for bulk data.
- Asymmetric (e.g. RSA): public/private key pair, slower, used for key exchange and digital signatures.

---

**Q.** Write about the Firewall. (10 marks)

**A.**  
A **firewall** is a security system that monitors and controls incoming and outgoing network traffic according to predetermined security rules. It creates a boundary between a trusted internal network (e.g. an organisation's LAN) and an untrusted external network (e.g. the Internet).

**How a firewall works:**  
The firewall inspects each packet or session and compares it against a **rule set** (access control list). Packets matching "ALLOW" rules pass through; others are blocked or dropped.

**Types of firewalls:**
1. **Packet-filtering firewall:** Examines IP/TCP/UDP headers (source/destination IP and port). Stateless — fast but limited.
2. **Stateful inspection firewall:** Tracks the state of active connections; knows whether a packet is part of an established session. More secure than packet filtering.
3. **Application-layer firewall (proxy):** Understands application protocols (HTTP, FTP); can inspect payload content; provides deep packet inspection.
4. **Next-generation firewall (NGFW):** Combines stateful inspection, application awareness, intrusion prevention, and SSL decryption.

**Benefits:**
- Blocks unauthorised access to internal systems
- Filters malicious traffic (e.g. known attack signatures)
- Logs traffic for monitoring and audit

**Limitations:**
- Cannot stop threats that originate inside the network
- Cannot inspect encrypted traffic without SSL decryption capability
- Rules must be maintained and updated regularly
