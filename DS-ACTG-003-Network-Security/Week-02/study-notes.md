# Network Security — Week 02 Study Notes

> Independently authored explanatory notes for general study. They are not verbatim lecture notes and do not include assessment questions. Consult [public references](references.md).

## CIA-based analysis of network attacks

| Security objective | Typical failure | Example | Defensive approach |
| --- | --- | --- | --- |
| Confidentiality | Unauthorized disclosure | Plaintext credentials observed on a shared link | Secure transports, remove obsolete services |
| Integrity | Unauthorized modification | False local IP-to-MAC mappings or tampered messages | Authenticated messages, network monitoring |
| Availability | Lost or degraded access | Service resource exhaustion | Monitoring, rate limits, upstream mitigation, resilience |

Attacks can cross categories. A network intermediary might observe, alter and drop traffic.

## Reconnaissance and defensive diagnostic tools

- **Wireshark/tcpdump:** packet capture and protocol analysis. Capturing encrypted frames does not automatically reveal plaintext.
- **Nmap:** identifies reachable ports and services when assessing an **authorized** target.
- **ss:** inspects local sockets and connections on Linux.
- **ping:** tests for ICMP Echo response; silence does not establish that a host is offline.
- **traceroute:** estimates visible intermediate routing hops.
- **CVE/NVD:** catalog known vulnerabilities; matching a version is only one step in applicability analysis.

**Safe local exercise:** run `ss -lnt` on your own Linux host; determine whether each listening socket is bound to loopback or a network interface. Do not scan external systems without permission.

## Packet spoofing and MitM

On a local IPv4 network, ARP associates an IP address with a link-layer MAC address. A deceptive ARP update can create an incorrect mapping, potentially redirecting traffic toward an adversary.

- **Spoofing:** falsifying an address or identity.
- **MitM:** positioning an adversary in a communication path.
- **Tampering:** modifying transmitted data.

Correctly authenticated TLS can continue to protect the application payload even when an attacker can see or relay encrypted packets. Network segmentation, switch features, verified communications and anomaly detection strengthen defenses.

## DoS, DDoS and TCP connection exhaustion

A **DoS** impairs the availability of a service; a **DDoS** coordinates impacts from multiple sources. A normal TCP connection begins with **SYN → SYN-ACK → ACK**. Abnormally large numbers of unfinished connections can consume server resources.

The defensive toolkit includes SYN cookies where applicable, connection/resource limits, filtering, monitoring and upstream capacity planning. Avoid performing packet floods even in a shared lab unless the scope and limits are explicitly authorized.

## Authentication, malware and web risks

**Authentication** verifies an asserted identity; **authorization** decides permitted actions; **accounting** records relevant use.

Credential guessing, phishing and identity impersonation may undermine authentication. Physical credential protection and user awareness complement technical measures.

Common malware families:
- **Virus:** replicates by infecting software/files.
- **Worm:** can propagate without a user launching every new infection.
- **Trojan:** conceals malicious functionality and need not self-replicate.
- **Ransomware:** restricts access, often encrypting data for extortion.

Web application examples:
- **SQL injection:** untrusted input influences queries; use parameterized SQL.
- **Command injection:** untrusted input becomes an OS command; avoid unsafe shell composition.
- **XSS:** attacker-controlled content executes in a user's browser; use context-aware output encoding.

Validate inputs, patch software, minimize privilege, monitor systems and maintain recoverable backups.

## Wireless link-level threat model

Wireless communication travels over a shared radio medium. Assess three attack points: **transmission medium**, **access point**, and **client/station**. Possible concerns include passive interception, replay, impersonation, interference, misconfiguration and vulnerable endpoints.

Hiding an SSID and MAC filtering are not adequate substitutes for cryptographic authentication.

### Wi-Fi security evolution

| Technology | Characteristic | Security perspective |
| --- | --- | --- |
| WEP | RC4 and short 24-bit initialization vector | Broken; never deploy |
| Original WPA | TKIP, based on RC4; longer 48-bit IV | Transitional/obsolete |
| WPA2 | AES-CCMP in secure configurations | Widely used; patch and configure carefully |
| WPA3 | SAE in Personal; stronger Enterprise options | Appropriate modern choice when supported |

**AES-CCMP:** counter mode (CTR) supports confidentiality; CBC-MAC supports authentication and integrity.

**KRACK** describes key-reinstallation weaknesses in affected WPA2 implementations. It does not mean every WPA2 connection can simply be decrypted. WPA3-Personal does **not** universally require AES-256; WPA3-Enterprise offers a distinct **192-bit security mode**. WPA2/WPA3 transition mode can support older devices, with possible security tradeoffs.

## IEEE 802.1X / EAP

**IEEE 802.1X:** port-based access control. **EAP:** extensible authentication framework.

| Role | Typical component | Function |
| --- | --- | --- |
| Supplicant | Laptop or mobile station | Requests access |
| Authenticator | Access point | Relays authentication and enforces access |
| Authentication Server | RADIUS-backed service | Evaluates identity/authorization policy |

The **uncontrolled** logical path permits necessary authentication messages before authorization. The **controlled** path restricts ordinary traffic until access is granted.

Conceptual lifecycle: **Discovery → Authentication → Key establishment → Protected transfer → Termination**.

A **PMK** (Pairwise Master Key) supports generation of a **PTK** (Pairwise Transient Key), whose constituent keys may include **KCK** (handshake integrity), **KEK** (key-material encryption) and **TK** (traffic protection). Exact derivation and lengths depend on security mode.

**EAP-TLS** uses certificates and can support mutual authentication if certificate validation is correctly configured. Weak or legacy EAP methods lack equivalent guarantees. WPA2-Personal PSK is not itself EAP/RADIUS-based.

## AAA, directory services and convenient setup

- **RADIUS:** common network AAA protocol; conventional authentication uses **UDP 1812**, accounting **UDP 1813**. EAP messages can be carried within RADIUS.
- **TACACS+:** AAA protocol commonly associated with network-device administration; uses **TCP 49**.
- **LDAP:** directory-access protocol supporting retrieval and management of organizational directory entries; relates to the **X.500** directory model. It is not interchangeable with RADIUS.
- **RADIUS over TLS:** adds transport security to RADIUS; assess implementation and current standards.
- **WPS:** simplifies Wi-Fi enrollment. Legacy PIN modes have had important security weaknesses. Disable unnecessary WPS mechanisms and prefer properly configured WPA2-AES/WPA3.

## Recall checklist

- [ ] Explain the CIA triad using an original attack scenario for each property.
- [ ] Distinguish packet capture, port discovery and local socket inspection.
- [ ] Explain spoofing versus MitM, without assuming TLS is broken.
- [ ] Describe a TCP handshake and why incomplete connections matter.
- [ ] Compare virus, worm, trojan and ransomware.
- [ ] Compare SQL injection, command injection and XSS.
- [ ] List three wireless attack points and basic controls.
- [ ] Compare WEP, WPA/TKIP, WPA2/CCMP and WPA3.
- [ ] Identify supplicant, authenticator, authentication server, PMK and PTK.
- [ ] Distinguish RADIUS, TACACS+, LDAP and WPS.
