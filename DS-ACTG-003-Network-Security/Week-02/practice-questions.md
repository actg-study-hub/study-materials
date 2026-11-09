# Week 02 — Original Self-Assessment

These **independently written** scenarios are not sourced from any graded or non-graded assessment. Attempt each before expanding the explanation.

### 1. A thermostat reading crosses an untrusted network in plaintext. Which security goal is exposed?
<details><summary>Answer and explanation</summary>Confidentiality: passive listeners may read the measurement. An authenticated encrypted channel can help.</details>

### 2. A defender needs to examine TCP sockets listening on their own Linux workstation. What tool is suitable?
<details><summary>Answer and explanation</summary>Use <code>ss</code>, such as <code>ss -lnt</code>, for local listening TCP sockets.</details>

### 3. A browser shows an unexpected warning from a compromised webpage that runs injected JavaScript. What attack category fits?
<details><summary>Answer and explanation</summary>Cross-site scripting (XSS): attacker-controlled code executes in the browser.</details>

### 4. What is the difference between a worm and a trojan?
<details><summary>Answer and explanation</summary>A worm can spread autonomously; a trojan conceals malicious functionality and does not have to self-replicate.</details>

### 5. Several coordinated compromised sources overwhelm one website. How is this classified?
<details><summary>Answer and explanation</summary>Distributed Denial of Service (DDoS), an availability threat.</details>

### 6. A gateway receives many incomplete TCP establishment requests. Which step of the normal handshake is missing?
<details><summary>Answer and explanation</summary>Many handshakes may fail to complete the final ACK after SYN and SYN-ACK.</details>

### 7. A host associates the default gateway's IPv4 address with an unexpected MAC address. What type of local risk warrants investigation?
<details><summary>Answer and explanation</summary>Potential ARP spoofing/poisoning; confirm against known-good topology and alerts rather than assuming every mapping change is malicious.</details>

### 8. In a WLAN threat model, what three elements should be reviewed?
<details><summary>Answer and explanation</summary>The radio transmission medium, access point and client stations.</details>

### 9. Why is a hidden SSID insufficient as a primary protection?
<details><summary>Answer and explanation</summary>SSID concealment is not cryptographic authentication or encryption and can be bypassed.</details>

### 10. Which legacy Wi-Fi design used RC4 with a short 24-bit IV?
<details><summary>Answer and explanation</summary>WEP. IV reuse and other design weaknesses make WEP obsolete.</details>

### 11. What two services does AES-CCMP combine?
<details><summary>Answer and explanation</summary>Confidentiality via counter-mode encryption and authenticated integrity via CBC-MAC.</details>

### 12. Why is a single blanket statement that all WPA3 networks use AES-256 inaccurate?
<details><summary>Answer and explanation</summary>WPA3 has distinct Personal and Enterprise modes; 192-bit Enterprise security mode differs from WPA3-Personal.</details>

### 13. A corporate laptop requests network access through an AP and a central server verifies identity. Name the three 802.1X roles.
<details><summary>Answer and explanation</summary>Supplicant (laptop), authenticator (AP) and authentication server (often RADIUS-backed).</details>

### 14. In a port-controlled network, which messages must be allowed before ordinary data access is authorized?
<details><summary>Answer and explanation</summary>The authentication exchange over the logical uncontrolled path; ordinary protected traffic remains controlled.</details>

### 15. A company wants to centrally organize employee group membership and directory attributes. Which protocol family is relevant?
<details><summary>Answer and explanation</summary>LDAP for directory access, distinct from network AAA protocols such as RADIUS and TACACS+.</details>

### 16. A Wi-Fi router offers a quick PIN enrollment mechanism. What security review question should the administrator ask?
<details><summary>Answer and explanation</summary>Whether WPS is necessary and whether its enrollment mechanism has known vulnerabilities; disable unnecessary insecure setup options.</details>

[Back to study notes](study-notes.md)
