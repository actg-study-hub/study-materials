# Week 01 — Network Security: Fundamentals, TCP/IP and Network Attacks

> **Unofficial, independently written study guide.** Structured to follow the three Week 1 sections of DS-ACTG-003: (1) fundamental network elements, (2) TCP/IP native protocols and their weaknesses, and (3) network-level attacks. Includes extra explanatory context clearly marked **Additional context**. No lecture slides or graded assessment questions are reproduced. **Updated: 2026-11-06.**

## Learning outcomes

After studying this page you should be able to:

1. Identify network elements and explain IP, MAC, switching, routing and common topologies.
2. Map familiar protocols to TCP/IP layers and explain what each protocol actually does.
3. Recognize the security implications of ARP, ICMP, TCP, UDP, DNS and insecure application protocols.
4. Distinguish **passive** from **active** attacks and describe interception, generation, impersonation, modification, denial of service, spoofing, poisoning, redirection, rogue devices and reconnaissance.
5. Interpret basic observations from an authorized packet capture without overclaiming what the evidence proves.

---

## Section 1 — Basic fundamentals and network elements

### 1. What constitutes a network?

A communication network connects at least two nodes so information can move over wired or wireless media. A typical exchange involves a **sender**, **receiver**, **message**, **protocol**, **networking software** and **interconnection devices**.

| Element | What it does | Example |
| --- | --- | --- |
| Host / endpoint | Originates or receives communications | Laptop, server, phone, printer |
| Packet / frame | Carries payload plus routing/delivery metadata | IP packet inside an Ethernet frame |
| Protocol | Defines rules for communication | IP, TCP, DNS |
| Network interface | Connects a host to a link | Ethernet NIC or Wi-Fi adapter |
| Switch | Primarily forwards frames on a LAN using MAC information | Access switch |
| Router | Forwards packets between IP networks based on routing decisions | LAN gateway |
| Firewall | Applies permitted/denied traffic policy | Stateful filtering at a perimeter or host |

**Addressing distinction:**

- **IPv4 address**: 32-bit logical network-layer identifier, usually written as four decimal octets (e.g. \`192.0.2.10\`).
- **IPv6 address**: 128-bit logical identifier, written in hexadecimal groups (e.g. \`2001:db8::10\`).
- **MAC address**: link-layer address used in local frame delivery (often 48 bits on Ethernet), e.g. \`02:42:ac:1c:32:0b\`.
- **Subnet / prefix**: for example, \`192.0.2.0/24\` contains 256 IPv4 addresses; in a conventional IPv4 unicast subnet, the network and broadcast addresses are not normally allocated to hosts, leaving 254 host addresses. This host-count rule is *not universal* (e.g. /31 point-to-point links).

A MAC address is **not** a globally reliable proof of device identity: modern systems may randomize or change MAC addresses.

### 2. Same network vs different network

When a destination is on the local subnet, an Ethernet host usually finds the destination's MAC address and sends it a frame directly over the local segment. For a remote destination, the host typically sends the frame to the **next-hop router** (default gateway), whose MAC address it resolves instead.

**Example:** Host A at \`172.28.50.11/24\` sends to Host B at \`172.28.50.12/24\` on the same segment. It resolves B's MAC by ARP. If it sends to \`172.28.60.2\`, it normally needs a route via an appropriate gateway. A lack of connectivity across separate Docker bridge networks does not, on its own, identify precisely which routing or firewall rule is responsible.

### 3. Network topologies

| Topology | Concept | Security / resilience consideration |
| --- | --- | --- |
| Star | Endpoints connect to a central switch/device | Central node is a key dependency |
| Bus | Nodes share a common backbone/medium | Shared medium and fault isolation challenges |
| Ring | Nodes form a closed path | Failure handling depends on ring protocol and redundancy |
| Mesh | Multiple interconnections | Resilience is improved, with greater complexity |
| Tree / hierarchical | Branching access, distribution and core | Clear aggregation, but important upstream dependencies |

Network growth, mobile/IoT devices and cloud services increase complexity and potential attack surfaces. **CIA objectives** remain the core: confidentiality, integrity and availability.

### 4. Related infrastructure concepts (**additional context**)

- **DHCP** automates address configuration through a DHCP exchange. An address assigned by Docker's **IPAM** does **not** demonstrate DHCP protocol traffic.
- **DNS** resolves names to resource records; it is not an IP-address assignment protocol.
- **NAT** translates network address information at a gateway in certain configurations. Do not infer a specific translation merely because internet access works.
- **Bridged vs NAT virtual networking** and **Docker bridge networks** are different abstractions; they are not interchangeable proof of the same networking behavior.

---

## Section 2 — TCP/IP stack and protocol weaknesses

### 5. The layered view

| TCP/IP layer | Rough OSI mapping | Representative concepts |
| --- | --- | --- |
| Application | OSI application/presentation/session | DNS, HTTP, SMTP, FTP |
| Transport | OSI transport | TCP, UDP |
| Internet | OSI network | IPv4/IPv6, ICMP, routing |
| Link / network access | OSI data link + physical | Ethernet, Wi-Fi, ARP on IPv4 LANs |

**Encapsulation:** Application data is carried in a transport segment/datagram; the transport data goes in an IP packet; the IP packet travels inside a link-layer frame. At a router, link-layer framing generally changes across hops, while IP-layer forwarding continues (subject to special network functions such as NAT).

The original Internet protocols were not uniformly designed with built-in authentication, encryption and integrity protection. Additional mechanisms such as **TLS** and **IPsec** address particular risks; they do not retroactively make every protocol or deployment secure.

### 6. ARP — Address Resolution Protocol

**Purpose:** On an IPv4 Ethernet-like LAN, ARP associates an IPv4 address with the link-layer MAC address needed to deliver a frame.

**Typical exchange:**

1. Host A needs the MAC for a neighboring IPv4 address.
2. A broadcasts an **ARP Request** ("Who has this IP?").
3. The owner responds with an **ARP Reply**, normally unicast.
4. A may store the mapping in its ARP/neighbor cache.

**Main weakness:** Traditional ARP has no built-in cryptographic validation of replies. Malicious updates can cause **ARP spoofing/poisoning**, potentially enabling traffic interception or denial of service on the affected local network.

**Defensive ideas:** DHCP snooping plus Dynamic ARP Inspection where appropriately supported, switch port controls, segmentation, monitoring, and higher-layer encryption. Those protections must be correctly designed and configured.

> **Scope:** ARP is for IPv4 neighbor resolution on applicable links; IPv6 uses **Neighbor Discovery Protocol (NDP)**, not ARP.

### 7. ICMP — control and diagnostic feedback

**Purpose:** ICMP communicates IP-related diagnostics and error information. The familiar \`ping\` utility typically uses **ICMP Echo Request / Echo Reply**; \`traceroute\` exploits TTL/hop-limit behavior and may use UDP, ICMP or TCP probes depending on implementation.

**Common misunderstanding:** ICMP is not inherently malicious and is not just "the ping protocol". Blindly blocking every ICMP message can interfere with useful error signaling or path-MTU discovery.

**Abuse examples:** Flooding/resource exhaustion and misleading control messages in vulnerable contexts.

### 8. TCP vs UDP

| Feature | TCP | UDP |
| --- | --- | --- |
| Connection model | Connection-oriented byte stream | Connectionless datagrams |
| Reliability and ordering | Retransmission, ordered byte stream | No built-in retransmission or ordering |
| Basic setup | Usually SYN → SYN-ACK → ACK | No TCP-style handshake |
| Overhead | Stateful transport management | Smaller basic header |
| Example uses | HTTPS over TCP, SSH, SMTP | DNS, real-time applications; QUIC runs over UDP |

**Security concepts:**

- TCP's handshake does **not** authenticate the remote application or encrypt application data.
- **SYN flooding** can exhaust resources related to connection attempts.
- UDP's lack of connection state can be useful for spoofed-source and reflection/amplification attacks when services are misconfigured.
- Neither TCP nor UDP alone guarantees confidentiality.

**Additional context:** HTTPS usually secures HTTP with TLS. Modern **HTTP/3** uses QUIC over UDP, so "HTTPS always uses TCP" would be incorrect.

### 9. Common application protocols and protection

| Protocol | Function | Typical security consideration |
| --- | --- | --- |
| HTTP | Transfers web requests/responses | Plain HTTP lacks transport encryption |
| HTTPS | HTTP over a secured transport | TLS provides authentication and confidentiality/integrity when correctly validated |
| DNS | Resolves domain names/resource records | Spoofing/cache-poisoning risks; **DNSSEC** authenticates signed DNS data, while DoT/DoH encrypt resolver transport |
| FTP | Transfers files | Traditional FTP is plaintext; use a secure alternative when appropriate |
| SMTP | Transfers email | Transport encryption and sender authentication require correct deployment; email content protection is separate |
| MIME | Defines Internet message format extensions | **A format specification**, not a standalone security/encryption protocol |

**Security layers added over time:** TLS, IPsec, DNSSEC, DNS over HTTPS/TLS, and email protection such as S/MIME or OpenPGP address different concerns. For example **DoH encrypts DNS transport** but does not by itself guarantee DNS record authenticity end-to-end.

---

## Section 3 — Taxonomy of network-level attacks

### 10. Passive vs active

- **Passive attack:** Observes, captures or analyzes communications without intentionally altering them. Example: unauthorized traffic monitoring.
- **Active attack:** Injects, modifies, blocks, redirects or impersonates network communications or systems. Example: ARP cache poisoning.

**Important nuance:** Reconnaissance can be passive (traffic observation) or active (sending scan probes).

### 11. High-level attack actions

| Action | Meaning | Illustrative effect |
| --- | --- | --- |
| Interception | Unauthorized access to traffic | Confidentiality loss |
| Generation / fabrication | Injected or forged messages | False traffic/events |
| Impersonation | Pretending to be another party | Loss of authenticity |
| Modification | Changing in-transit data | Integrity loss |
| Interruption / DoS | Making a service unavailable | Availability loss |

### 12. Recognizing common attacks

| Attack category | Core idea | Common mitigation direction |
| --- | --- | --- |
| **Spoofing** | Forge identifying information (e.g. source address) | Strong authentication, source validation, filtering |
| **Poisoning** | Insert false information into a cache or protocol state | Integrity checks, switch protections, DNSSEC where applicable |
| **Man-in-the-middle** | Position an attacker between communicating endpoints | TLS with validation, network security and monitoring |
| **DoS / DDoS** | Overwhelm or prevent service | Rate limiting, resilient architecture, upstream response |
| **Redirection / hijacking** | Force traffic to an unintended destination | Authenticated routing/name resolution, TLS validation |
| **Rogue device/service** | Unauthorized or manipulated network device/service | Inventory, access controls, network access security |
| **Reconnaissance** | Map hosts, services, dependencies or traffic | Exposure management, logging, segmentation |

These are conceptual categories: a real attack may involve more than one (for example spoofing and poisoning to enable interception).

### 13. Example analysis — without attacking anything

**Scenario:** A host suddenly associates the gateway IPv4 address with a new MAC and begins sending traffic through an unexpected device.

- **Observation:** Neighbor-cache change (possible indication, not proof).
- **Hypothesis:** ARP poisoning or legitimate gateway/interface replacement.
- **Potential objective impact:** Confidentiality (interception), integrity (modification), availability (blackholing).
- **Verification:** Compare authorized switch/device records, ARP captures, interface changes, and traffic flows.
- **Protection:** Layer-2 controls plus TLS-based application protection.

A single ARP table entry is not enough to attribute an attack. Avoid diagnosing causes from one packet or one screenshot.

---

## Practical study workflow (authorized lab only)

The [Docker lab guide](docker-lab.md) is a companion to this theory.

| Learning goal | Observation | What it actually demonstrates |
| --- | --- | --- |
| IPv4 subnet connectivity | \`ping -c 4 <peer>\` | Echo exchange succeeded/failed in that environment |
| Neighbor discovery (IPv4) | \`ip neigh\`, \`tcpdump -i eth0 arp\` | Seen ARP frames and current cached mappings |
| ICMP request/reply | \`tcpdump\` + Wireshark | Captured request/reply types and addressing |
| Route tracing | \`traceroute\` | Responses observed from routers/hops, subject to filtering |
| Separate Docker networks | Send packets across test networks | An observed connectivity outcome, not automatically its cause |

**Evidence limits:** Seeing Docker automatically allocate an IP is **not** capturing DHCP. A one-hop traceroute does **not** prove behavior of a separate physical router. Successful outbound web access does **not** independently reveal NAT translations.

### Simple Wireshark display filters

These filters select packets; they do **not** send attacks.

| Filter | Purpose |
| --- | --- |
| \`arp\` | ARP frames |
| \`icmp\` | IPv4 ICMP |
| \`tcp\` | TCP |
| \`udp\` | UDP |
| \`dns\` | Traffic decoded as DNS |
| \`ip.addr == 172.28.50.11\` | IPv4 packets involving this sample address |

## Common mistakes to avoid

- **IP != MAC**: logical network address vs link-layer address.
- **Switch != router**: switching typically uses L2 frame delivery; routing connects IP networks.
- **ARP != DNS**: mapping local IPv4 to MAC vs resolving names/resource records.
- **TCP != TLS**: transport reliability is different from authenticated encryption.
- **ICMP != TCP/UDP application data**: ICMP handles IP-related control/diagnostic messages.
- **Ping failure != conclusive proof of offline host**: filtering, routes and firewalls can affect it.
- **Public-facing service != automatically vulnerable**: risk depends on exposure and controls.

## Independent practice

Use the [self-check questions](practice-questions.md) before expanding the explanations.

## Public, primary reference material

- [RFC 791 — Internet Protocol (IPv4)](https://www.rfc-editor.org/rfc/rfc791)
- [RFC 826 — Ethernet Address Resolution Protocol](https://www.rfc-editor.org/rfc/rfc826)
- [RFC 792 — Internet Control Message Protocol](https://www.rfc-editor.org/rfc/rfc792)
- [RFC 9293 — Transmission Control Protocol](https://www.rfc-editor.org/rfc/rfc9293)
- [RFC 768 — User Datagram Protocol](https://www.rfc-editor.org/rfc/rfc768)
- [RFC 1034 — Domain Names: Concepts and Facilities](https://www.rfc-editor.org/rfc/rfc1034)
- [RFC 8446 — TLS 1.3](https://www.rfc-editor.org/rfc/rfc8446)
- [RFC 9000 — QUIC](https://www.rfc-editor.org/rfc/rfc9000)
- [NIST CSRC Glossary](https://csrc.nist.gov/glossary)
- [Wireshark Documentation](https://www.wireshark.org/docs/)

**Note:** All explanations here are original prose. The course outline determined the topics; details marked "Additional context" extend beyond the minimum Week 1 outline. This is a community learning aid, not a substitute for the course or a claim of official endorsement.
