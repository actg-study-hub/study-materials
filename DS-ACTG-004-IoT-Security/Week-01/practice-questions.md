# IoT Security Week 01 — Independently Written Practice

**Original scenarios for general learning.** Not course graded/non-graded questions, restricted CTF content, hints, or assessment solutions. Try each before expanding the explanation.

### 1. A greenhouse measures humidity and opens a water valve. Which component senses and which acts?
<details><summary>Explanation</summary>The humidity probe is a **sensor**; the electrically controlled valve is an **actuator**.</details>

### 2. A low-power sensor communicates over a non-IP wireless link, but its records must reach an Internet backend. What is an important function of the hub?
<details><summary>Explanation</summary>The **gateway** bridges the local device protocol to an IP-capable network/service.</details>

### 3. A reporting portal displays historical readings to an operator. Which conceptual IoT layer provides the user-facing portal?
<details><summary>Explanation</summary>The **application layer** provides interfaces to users.</details>

### 4. A cloud service deduplicates messages and stores device events for later use. Which layer does this primarily represent?
<details><summary>Explanation</summary>The **middleware layer**, which processes and stores information for applications.</details>

### 5. An outdoor sensor is reachable by passersby. What type of risk becomes more relevant?
<details><summary>Explanation</summary>**Physical exposure/tampering** and access to local hardware interfaces.</details>

### 6. A once-local appliance now has Wi-Fi, remote vendor APIs and mobile sign-in. What changed from a security perspective?
<details><summary>Explanation</summary>The **attack surface** and dependencies expanded: new communication and account-access paths need protection.</details>

### 7. A backend correctly encrypts messages but accepts commands from anonymous clients. What critical protection is absent?
<details><summary>Explanation</summary>**Authentication/authorization** at the API or broker. Encryption alone does not control who may act.</details>

### 8. A messaging service forwards measurements to multiple dashboard clients subscribing to named channels. Which messaging pattern is illustrated?
<details><summary>Explanation</summary>**Publish/subscribe**, often implemented using a broker and topics in MQTT.</details>

### 9. Multiple deployed devices share the same factory management password. What design change would reduce this weakness?
<details><summary>Explanation</summary>Use secure enrollment and **unique device credentials**, and disable unnecessary exposed services.</details>

### 10. A manufacturer cannot associate individual physical devices with firmware versions. Which baseline capability is especially relevant?
<details><summary>Explanation</summary>**Device Identification** helps establish a reliable inventory.</details>

### 11. A sensor accepts unsigned firmware from an unverified source. Which capability is lacking?
<details><summary>Explanation</summary>**Software Update** must support secure, authorized and authenticated updates.</details>

### 12. A camera stores protected footage but exposes live footage through a public stream without access checks. Which capabilities are implicated?
<details><summary>Explanation</summary>**Data Protection** and **Logical Access to Interfaces**. Protecting stored data does not excuse unprotected streaming.</details>

### 13. A deployed gateway knows that its integrity verification failed but never reports this to its administrator. What does it need?
<details><summary>Explanation</summary>**Cybersecurity State Awareness** to make relevant security-state information available.</details>

### 14. Two devices satisfy the same security objective using different software and hardware designs. Does the NISTIR 8259A baseline forbid this?
<details><summary>Explanation</summary>**No.** The baseline describes desired capabilities, not a unique implementation.</details>

### 15. A connected pump can affect water pressure if a malicious command is accepted. What additional impact type belongs in the risk assessment?
<details><summary>Explanation</summary>**Physical/safety impact**, alongside confidentiality, integrity and availability.</details>

[Return to study notes](study-notes.md).
