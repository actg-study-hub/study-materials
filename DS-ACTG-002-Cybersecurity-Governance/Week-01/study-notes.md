# Week 01 — Cybersecurity Governance & Fundamentals

> **Original community study notes (not official course material).** Based on the learning topics of DS-ACTG-002 Week 1. This guide combines the three lecture sessions: concepts, threat actors, and attack vectors/malware. **Updated: 2026-11-06.**

## Learning outcomes

Explain security objectives and ethics; classify controls by **what they are** and **what they do**; understand asset/change management, physical security and awareness; identify common threat actors, attack vectors and malware classes.

## Session 1 — Core concepts and controls

### 1. Information security, cyber security and ethics

- **Information security** protects information in all forms.
- **Cybersecurity** concerns the digital systems, networks and data exposed to cyber threats.
- **Ethics** and authorization matter: effective security actions still need legitimate purpose, proportionality and accountability.

The **CIA triad**:

| Objective | Meaning | Original example |
| --- | --- | --- |
| Confidentiality | Prevent disclosure to unauthorized parties | Limit access to employee salaries |
| Integrity | Prevent unauthorized or incorrect modification | Verify that exam scores match approved entries |
| Availability | Keep systems/data usable when required | Backup power and failover for critical servers |

Related properties: **authenticity** (genuine identity/source), **non-repudiation** (evidence supporting that an actor performed an action), **privacy**, **accountability**, and **safety**. Distinct concerns can overlap in a real incident.

### 2. Due care vs due diligence

- **Due care:** Take reasonable protective steps, such as establishing an access-control policy.
- **Due diligence:** Verify that protective measures keep operating effectively, such as reviewing access logs and periodically testing enforcement.

A control that was approved once but never checked again can decay in effectiveness.

### 3. Classify controls on two axes

**Implementation type** asks *how is the control implemented?*

| Type | Examples |
| --- | --- |
| Technical / logical | Firewalls, encryption, antivirus, IDS/IPS |
| Administrative / organizational | Policies, risk assessments, approval processes, staff training |
| Physical | Locks, doors, fences, guards, equipment-room controls |

**Functional type** asks *what job does it perform?* One implementation may support multiple functions.

| Function | Purpose | Example |
| --- | --- | --- |
| Directive | Tell people what to do | Required-use policy or warning banner |
| Deterrent | Discourage misuse | Warning notices or visible guards |
| Preventive | Block unwanted events | Authentication, access restrictions |
| Detective | Identify and report suspicious events | IDS, logs reviewed/alerted on, motion detection |
| Corrective | Contain or correct an identified problem | Disable compromised account, isolate infected host |
| Recovery | Restore service or data | Backups, disaster recovery, rebuilding |
| Compensating | Alternative protection when a preferred control is unavailable | Extra monitoring and restricted access while a patch is delayed |

**Example:** An IDS is typically detective; an IPS can actively block certain traffic and therefore has a preventive role. A backup is primarily recovery, not detection.

### 4. Defence in depth

Combine multiple independent safeguards: physical restrictions, network segmentation, authentication, encryption, monitoring and awareness. One firewall or one purchased product does **not** make an organization secure.

### 5. Asset management

Assets include **tangible** equipment, **intangible** information/IP, **human** expertise and **infrastructure** such as networks and power systems. Management begins with **identification**, then inventory, classification, ownership, protection, monitoring and secure disposal.

For a basic asset record, document an identifier, owner, business importance, location, data handled, dependencies and lifecycle status.

### 6. Change management

A controlled change generally includes request, impact/risk assessment, approval, implementation, testing, documentation and rollback planning.

**Original example:** Replacing a production firewall without assessing affected services or arranging approval can cause unnecessary outage and control gaps.

### 7. Physical security and power resilience

Cybersecurity depends on the physical environment. Server-room locks, guards, CCTV, fire detection and environmental monitoring help protect confidentiality, integrity and availability. **UPS**, generators, power conditioning and cooling protect availability when electricity or environmental conditions deteriorate. Controls should be maintained and tested, not merely installed.

### 8. Security awareness vs training

- **Awareness:** Make people recognize a risk and choose safer behavior (e.g., simulated phishing followed by a short debrief).
- **Training:** Teach and practice a specific skill (e.g., learning how to report an incident with the ticketing tool).

Exercises, onboarding, repetition and feedback turn rules into habits. A simulation can support awareness or training depending on its stated learning objective.

## Session 2 — Threat actors and cybercrime

A **threat actor** is an entity capable of causing harm intentionally or unintentionally. Motivation helps prioritize defenses but is not proof of attribution.

| Actor category | Typical motivations and concerns |
| --- | --- |
| Cybercriminal groups | Financial gain; fraud, extortion, data theft |
| State-aligned actors | Espionage, strategic access, disruption |
| Hacktivists | Ideological or political goals |
| Insiders | Error, disgruntlement, financial gain or coercion |
| Thrill seekers | Experimentation, attention, status |
| Terrorist organizations | Ideological disruption and fear |

**Sector-specific risk:** A hospital emphasizes patient safety and operational continuity; a retailer may prioritize payment/customer data; a public agency may face availability, sensitive information and disinformation risks. Never assume one sector has exactly one type of attack.

**Cognitive warfare:** Attempts to manipulate perceptions and decision-making through information influence. It intersects with phishing, deception and misinformation but is conceptually distinct from malware compromise.

## Session 3 — Attack vectors and malware

### 1. Entry paths (attack vectors)

- **Phishing / spear phishing:** Deceptive communications that entice recipients to reveal secrets or execute actions.
- **Smishing / vishing:** SMS-based and voice/telephone-based social engineering.
- **Malicious websites / drive-by attacks:** Users encounter a harmful site or content; exploitation depends on the environment.
- **Stolen credentials / identity spoofing:** Attacker impersonates a legitimate account or source.
- **Removable media / malicious peripherals:** Compromise through untrusted connected hardware.
- **Network attacks:** Abuse of exposed protocols, services, routing or name-resolution trust.
- **Supply-chain compromise:** Harmful changes enter through a vendor, software dependency, update or service relationship.

### 2. Common malware categories

| Category | Distinguishing feature |
| --- | --- |
| Virus | Infects host files/programs and generally requires execution to propagate |
| Worm | Self-propagates across reachable systems or networks |
| Trojan | Disguises malicious function as a desirable or legitimate program |
| Ransomware | Restricts data/system access, commonly through encryption, to extort payment |
| Spyware | Covertly collects information |
| Rootkit | Helps conceal malicious presence or privileged activity |
| Bot / botnet malware | Enables a compromised host to be remotely directed |

**Infection → execution → persistence → impact** is a useful conceptual sequence, but not every incident follows the same order. Privilege escalation, lateral movement and exfiltration are attacker activities, not malware types.

### 3. Defensive thinking

For any threat scenario, ask: **What asset? What entry path? What affected CIA objective? Which preventive/detective controls? How would we contain and recover?** Prefer layered mitigations instead of a single product.

## Exam-preparation distinctions

- Technical vs physical = **implementation**; detective vs recovery = **function**.
- Integrity = preventing unauthorized alteration; availability = continued access.
- Logs are detective when collected/inspected or alerted on, not merely stored.
- Deleting a compromised account or isolating malware = corrective action.
- Backups and disaster-recovery plans = recovery.
- Awareness and practical skills training are related but not identical.
- A successful phishing lure is an **attack vector**; ransomware is a **possible payload/impact**.

## Self-study

Work through [independent practice questions](practice-questions.md) before reading their explanations.

## Public sources and further reading

- [NIST CSRC Glossary](https://csrc.nist.gov/glossary)
- [CISA Cybersecurity Resources](https://www.cisa.gov/resources-tools)
- [ENISA Threat Landscape](https://www.enisa.europa.eu/topics/cyber-threats/threat-landscape)
- [MITRE ATT&CK](https://attack.mitre.org/) — attack technique reference.
- [NIST Cybersecurity Framework](https://www.nist.gov/cyberframework)

These are learning pointers. No copyrighted standards, official lecture images or assessed questions are reproduced here.
