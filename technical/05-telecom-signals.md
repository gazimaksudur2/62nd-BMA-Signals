# Telecom & Signals Overlap — Technical Study Notes

> **Why it is asked:** This section reflects the Signals Corps context of the exam. FDMA/TDMA appeared as a 10+10 mark question in the 36th paper. WiMAX, GPRS, EDGE, and CDMA were short-note choices in the same paper. Shannon–Hartley is a dedicated question in the source file. Modulation and multiplexing are confirmed 60th BMA viva topics.

---

## 1. Modulation

**Definition:** Modulation is the process of altering one or more properties of a high-frequency carrier signal (amplitude, frequency, or phase) to encode information for transmission.

**Why needed:** A low-frequency voice or data signal cannot travel long distances on its own. Modulation shifts it to a high-frequency carrier that can propagate efficiently over radio/wire channels.

**Three basic types:**

| Type | What changes | Full name |
|---|---|---|
| AM | Amplitude | Amplitude Modulation |
| FM | Frequency | Frequency Modulation |
| PM | Phase | Phase Modulation |

Digital modulation variants: ASK (Amplitude Shift Keying), FSK (Frequency Shift Keying), PSK (Phase Shift Keying), QAM (Quadrature Amplitude Modulation — used in 4G/5G).

---

## 2. Multiplexing

**Definition:** Multiplexing is the technique of combining multiple signals onto a single communication channel, so they share the medium efficiently.

**Why needed:** Running a separate physical cable or radio frequency for every single conversation or data stream is impractical. Multiplexing allows many users to share one channel.

```
User 1 ─┐
User 2 ─┤  Multiplexer ──── Single shared channel ──── Demultiplexer ─┬─ User 1
User 3 ─┤                                                              ├─ User 2
User 4 ─┘                                                              └─ ...
```

---

## 3. FDMA — Frequency Division Multiple Access

**Definition:** FDMA divides the available frequency spectrum into non-overlapping sub-bands. Each user is assigned a unique frequency band for the entire duration of a call.

```
Frequency band (MHz)
├─ User 1: 800–810 MHz
├─ User 2: 810–820 MHz
├─ User 3: 820–830 MHz
└─ User 4: 830–840 MHz
```

**Advantages:**
- Simple to implement; well-understood technology
- No time synchronisation required between users
- No guard time needed between transmissions
- Low latency for voice communications

**Disadvantages:**
- Fixed bandwidth allocation is wasteful if a user is idle
- Inter-channel interference if guard bands are too narrow
- Limited capacity — spectrum is a finite resource
- Not suitable for bursty (variable) data traffic (e.g. internet)

---

## 4. TDMA — Time Division Multiple Access

**Definition:** TDMA assigns each user the entire frequency band, but only for a specific recurring time slot. Users take turns transmitting in rapid succession so each "slot" appears continuous.

```
Time ─────────────────────────────────────►
Frame: [ User 1 | User 2 | User 3 | User 1 | User 2 | User 3 | … ]
```

**Advantages:**
- Bandwidth is shared more efficiently for bursty traffic
- No inter-channel interference (same frequency, different times)
- Can support different numbers of users by reassigning slots
- Digital by nature — easy to integrate with modern networks

**Disadvantages:**
- Requires precise time synchronisation between all users
- Guard times between slots reduce efficiency
- More complex receiver design
- Transmission delay (must wait for your slot)

**Used in:** GSM 2G mobile network (each GSM channel = 8 TDMA time slots).

---

## 5. CDMA — Code Division Multiple Access

**Definition:** CDMA allows all users to transmit simultaneously on the same frequency. Each user's data is spread across the full bandwidth using a unique orthogonal code. At the receiver, only the matching code extracts the intended signal; others appear as background noise.

**Key idea:** Distinguish users by unique *codes* rather than frequency or time.

**Advantages:**
- Soft capacity — adding users degrades quality gradually (no hard limit)
- Resistant to interference and eavesdropping (spread-spectrum)
- Frequency reuse factor of 1 (all cells use the same frequency)

**Disadvantages:**
- Requires precise power control (near–far problem)
- Self-interference from all simultaneous users ("noise floor" rises)
- Complex code assignment and management

**Used in:** 3G (WCDMA / CDMA2000), GPS.

---

## 6. GPRS — General Packet Radio Service

**What it is:** GPRS is a 2.5G packet-switching overlay on GSM networks, enabling mobile Internet access. Data is sent in packets rather than a dedicated circuit.

- Speed: 56–114 kbps (theoretical)
- First "always-on" mobile data service
- Used TCP/IP over cellular radio

---

## 7. EDGE — Enhanced Data rates for GSM Evolution

**What it is:** EDGE (also called 2.75G) enhanced GPRS by changing the radio modulation from GMSK to 8-PSK, allowing more bits per symbol.

- Speed: up to 384 kbps
- Backward compatible with GPRS infrastructure
- Paved the way for 3G

---

## 8. WiMAX — Worldwide Interoperability for Microwave Access

**What it is:** WiMAX is a wireless broadband standard defined by IEEE 802.16, designed as a "last-mile" alternative to DSL or cable modems, capable of covering metropolitan areas.

**Standards:**
- **IEEE 802.16-2004:** Fixed wireless (replace DSL/cable at home/office)
- **IEEE 802.16e-2005:** Mobile WiMAX (compete with cellular 3G/4G)

**Range:** Up to 50 km (line-of-sight fixed); ~3–10 km (non-line-of-sight mobile)  
**Speed:** Up to 70 Mbps (fixed)

**Advantages:** Large coverage area; high throughput; no physical cable required.  
**Disadvantages:** Requires licensed spectrum; physical obstacles degrade performance; largely superseded by LTE/4G.

---

## 9. Shannon–Hartley Theorem

**Theorem:** The channel capacity C is the theoretical maximum data rate over a channel with bandwidth B and signal-to-noise ratio SNR:

```
C = B × log₂(1 + S/N)
```

Where:
- **C** = channel capacity (bits per second)
- **B** = bandwidth of the channel (hertz)
- **S/N** = signal-to-noise ratio (as a linear power ratio, not dB)

**Example:** A channel with B = 1 MHz and S/N = 31:  
C = 1,000,000 × log₂(32) = 1,000,000 × 5 = **5 Mbps**

**Significance:**
- Sets a fundamental upper bound — no encoding technique can exceed this capacity for a given bandwidth and SNR, regardless of how clever.
- Increasing bandwidth OR SNR increases capacity; a noisy channel fundamentally limits achievable throughput.
- Foundation of modern communications engineering (4G, 5G, Wi-Fi channel design).

---

## Q&A Bank

### True / False

**T1.** FDMA divides the available spectrum into separate frequency bands for each user.  
→ **True**

**T2.** TDMA allows all users to transmit on the same frequency simultaneously.  
→ **False** (TDMA allows users to share the same frequency in *different time slots*, not simultaneously. CDMA allows simultaneous transmission.)

**T3.** WiMAX is defined by IEEE standard 802.16.  
→ **True**

**T4.** The Shannon–Hartley theorem gives the minimum data rate for a noisy channel.  
→ **False** (It gives the *maximum* channel capacity — a theoretical upper bound.)

**T5.** GPRS was a circuit-switched enhancement to GSM.  
→ **False** (GPRS is **packet-switched** — that is exactly what made it useful for Internet data.)

**T6.** CDMA identifies users by assigning unique orthogonal codes.  
→ **True**

---

### MCQ

**Q1.** Which multiple access technique divides frequency spectrum into sub-bands per user?  
(a) TDMA  (b) CDMA  (c) FDMA  (d) OFDMA  
→ **(c)** FDMA

**Q2.** In the Shannon–Hartley formula C = B log₂(1 + S/N), what does B represent?  
(a) Bit rate  (b) Bandwidth in Hz  (c) Signal power  (d) Noise power  
→ **(b)** Bandwidth in hertz

**Q3.** EDGE improved upon GPRS primarily by:  
(a) Increasing bandwidth allocation  (b) Changing to packet switching  (c) Using 8-PSK modulation  (d) Adding IPv6 support  
→ **(c)**

**Q4.** WiMAX IEEE standard 802.16e-2005 covers:  
(a) Fixed satellite communications  (b) Mobile WiMAX  (c) Fixed wired broadband  (d) Bluetooth  
→ **(b)**

---

### Descriptive Q&A

**Q.** What is FDMA? State its advantages and disadvantages. (10 marks)

*(Full model answer is in the FDMA section above — repeat key points in exam.)*

**Q.** What is TDMA? State its advantages and disadvantages. (10 marks)

*(Full model answer is in the TDMA section above — repeat key points in exam.)*

**Q.** Write the Shannon–Hartley theorem and explain its significance. (5 marks)

**A.**  
The Shannon–Hartley theorem states:

**C = B × log₂(1 + S/N)**

This equation gives the maximum theoretical data rate (channel capacity **C** in bps) that can be reliably transmitted over a channel of bandwidth **B** Hz with signal-to-noise ratio **S/N**.

Significance:
- Represents a fundamental physical limit — no communication technique can exceed this capacity for given B and S/N.
- Increasing SNR (better signal or less noise) raises capacity.
- Increasing bandwidth raises capacity proportionally.
- Motivates modern techniques like MIMO and adaptive modulation (4G/5G) to approach the Shannon limit.
