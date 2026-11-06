# DS-ACTG-003 — Week 01 Original Self-Assessment

> **Independent practice only** — not transcribed or adapted from an active graded test. Attempt each question first, then expand the answer.

## Part A — Basic concepts

### 1. A workstation has an IPv4 address and a MAC address. Which one does a router normally examine to choose the next IP network?

<details><summary>Answer and explanation</summary>

**The destination IP address.** Routers make forwarding decisions using the IP routing table. Link-layer MAC addressing is used on each applicable hop to deliver frames locally.

</details>

### 2. Two hosts are on the same IPv4 Ethernet subnet. What problem does ARP solve?

<details><summary>Answer and explanation</summary>

It discovers an **IPv4-to-MAC mapping** for the appropriate local destination. DNS answers a different question: how a domain name maps to records such as IP addresses.

</details>

### 3. A company's endpoints connect to a single central switch. Which physical topology best describes this?

<details><summary>Answer and explanation</summary>

**Star topology.** The switch is a central dependency; its failure may disconnect attached endpoints.

</details>

### 4. A backup power system keeps a network service online during a short outage. Which CIA objective does it primarily support?

<details><summary>Answer and explanation</summary>

**Availability.** The aim is to keep an authorized service usable when required.

</details>

## Part B — Protocols

### 5. A capture shows an ARP Request but no ARP Reply. Does that alone prove there was no valid peer?

<details><summary>Answer and explanation</summary>

**No.** A reply may have been missed because of capture placement, timing, filtering or because the cache state changed. Check the relevant interfaces and neighbor tables before drawing conclusions.

</details>

### 6. Why can a successful TCP three-way handshake not by itself prove the connection is encrypted?

<details><summary>Answer and explanation</summary>

TCP establishes a transport connection and provides ordering/retransmission. **Encryption and application-endpoint authentication require additional protocols**, often TLS.

</details>

### 7. Which transport protocol offers no built-in ordered reliable byte stream: TCP or UDP?

<details><summary>Answer and explanation</summary>

**UDP.** Its base service sends datagrams without guaranteeing delivery or ordering. Applications may implement additional reliability above UDP (for example QUIC).

</details>

### 8. What do ICMP Echo Request and Echo Reply commonly help diagnose?

<details><summary>Answer and explanation</summary>

Reachability and round-trip behavior between communicating nodes, subject to filtering and network conditions. A failed ping does not conclusively prove the node is powered off.

</details>

### 9. Does DNS over HTTPS automatically mean DNS data is cryptographically authenticated all the way from its authoritative source?

<details><summary>Answer and explanation</summary>

**No.** DoH encrypts DNS transport between the client and a resolver. **DNSSEC**, when validated and correctly deployed, addresses authenticity of signed DNS data. The two protections solve different problems.

</details>

## Part C — Security and investigations

### 10. An attacker silently captures traffic without injecting or modifying packets. Passive or active?

<details><summary>Answer and explanation</summary>

**Passive interception/observation.** It can compromise confidentiality even without visible network disruption.

</details>

### 11. An attacker sends forged neighbor-mapping information so a victim forwards LAN traffic through the attacker's machine. What is this called?

<details><summary>Answer and explanation</summary>

**ARP spoofing/poisoning.** It may enable man-in-the-middle interception or disruption. A new ARP mapping alone is insufficient proof of malicious behavior.

</details>

### 12. A botnet overwhelms a public server with coordinated traffic. Which security objective is primarily harmed?

<details><summary>Answer and explanation</summary>

**Availability** through distributed denial of service (DDoS). Additional damage is possible, but denial of service focuses on resource/service disruption.

</details>

### 13. A hostname that usually points to a legitimate service is altered to resolve to an attacker-controlled destination. Which concepts are relevant?

<details><summary>Answer and explanation</summary>

**DNS poisoning/hijacking and traffic redirection** may be involved, depending on how the DNS answer or resolver configuration was changed. TLS certificate validation can help prevent successful impersonation of the target application.

</details>

### 14. Is a port scan passive reconnaissance?

<details><summary>Answer and explanation</summary>

**Generally no.** A port scan sends probes, so it is **active reconnaissance**. Observing existing traffic without probes is passive reconnaissance.

</details>

### 15. Docker assigns a container an IP address automatically. Has a DHCP Discover/Offer/Request/Acknowledge exchange been proven?

<details><summary>Answer and explanation</summary>

**No.** Docker network IPAM can assign addresses without DHCP packets. A claim about DHCP requires evidence of actual DHCP messages or another verified DHCP mechanism.

</details>

### 16. A packet capture contains four ICMP Echo Requests and four Echo Replies, but an unrelated machine cannot reach the same network. What can you safely claim?

<details><summary>Answer and explanation</summary>

The captured pair exchanged four observed request/reply pairs **in that setup**. The separate failure needs its own investigation; the successful local test does not prove end-to-end reachability from other networks.

</details>

## Revision checklist

- [ ] Distinguish IP, MAC and DNS names.
- [ ] Explain same-subnet forwarding and the default gateway.
- [ ] Map ARP, ICMP, TCP/UDP and DNS to the right layers.
- [ ] Explain what TCP, TLS and HTTPS each add.
- [ ] Describe passive vs active attacks.
- [ ] Recognize spoofing, poisoning, DoS, redirection, rogue services and reconnaissance.
- [ ] Separate observed packet-capture facts from hypotheses.
- [ ] Explain why Docker IPAM is not equivalent to DHCP.

Revisit the [study notes](study-notes.md) or run the [authorized Docker lab](docker-lab.md).
