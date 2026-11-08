# Week 02 — Cybersecurity Landscape

> Independently written educational explanations following the topic sequence of the module. **Not official teaching content, not a transcript, and not a graded-assessment answer key.** Consult [public standards and references](references.md) to verify technical details.

## Learning outcomes

Explain system and network protection mechanisms; compare cryptographic functions and secure key management; recognize certificates and their limits; choose appropriate authenticators and authorization models; map cyber operations with Kill Chain and ATT&CK; separate CTI intelligence levels; identify AI-related security opportunities and risks; and understand post-quantum migration.

---

# Session 1 — Technologies

## 1. System security: protecting the endpoint

A strong encrypted network channel cannot compensate for a compromised endpoint. If malware can read plaintext after decryption, transport protection alone is insufficient.

**System components and security boundaries:** CPU executes instructions; memory contains active code/data; storage contains durable data; firmware initializes the machine; hardware security components such as TPMs provide specialized capabilities. Attackers may target vulnerabilities at multiple layers.

**Defense categories**
- **Patch management** mitigates known OS/application vulnerabilities.
- **CPU/OS defenses** include execution privileges, NX/DEP (non-executable memory), ASLR (address-space randomization) and control-flow defenses such as shadow stacks.
- **Monitoring** includes endpoint antimalware, firewalls and intrusion detection.
- **Virtualization** can isolate workloads, although hypervisor vulnerabilities remain possible.
- **Trusted computing** uses hardware-backed functions, including verified boot processes, protected keys and attestations.

### Privilege levels — an educational model

| Level | Concept |
| --- | --- |
| **Ring 3** | User-mode applications (less privileged) |
| **Ring 0** | OS kernel execution (privileged) |
| **“Ring −1”** | Informal shorthand for hypervisor/virtualization execution context |

Rings 1 and 2 are rarely used by general-purpose OS application models. **Important nuance:** Linux `root` or Windows Administrator is an *OS account privilege*, not the same thing as executing arbitrary code in CPU Ring 0.

### VMs, isolation and trusted computing

A **Type 1 hypervisor** operates directly over physical hardware to manage guest virtual machines. Each guest typically has its own operating-system kernel; containers instead usually share a host kernel. Isolation lowers cross-workload exposure, but neither model guarantees perfect security.

**UEFI Secure Boot** checks signatures/policy for parts of the boot path. A **TPM** can support measured boot, key protection, sealed storage and attestation; **TEE** denotes hardware-supported isolation for selected computations. These are distinct mechanisms, sometimes used together.

## 2. Network protection: TLS, firewalls and intrusion detection

The Internet communication stack separates functions: applications (e.g., HTTPS), transport (TCP/UDP), IP, link (Ethernet/Wi-Fi), and physical media.

**TLS** protects compatible application communications through authenticated key establishment and record protection. In standard TLS 1.3 handshakes, fresh (ephemeral) Diffie–Hellman material supports **forward secrecy**: later compromise of a server's long-term authentication key does not, *by itself*, disclose earlier session traffic secrets. It can still enable future impersonation; forward secrecy does not protect endpoints from malware.

### Network segmentation / DMZ

A **firewall** evaluates traffic against policy (addresses, ports, connection state and/or application properties depending on product). A **demilitarized zone (DMZ)** commonly hosts selected externally reachable services in a separated network. Internal segments may have stricter access controls. Segmentation reduces lateral movement opportunities; it is not a substitute for securing the exposed service.

### IDS approaches

| Approach | Basis | Strength | Limitation |
| --- | --- | --- | --- |
| **Signature-based** | Matches documented patterns/rules | Effective for known observable behaviors | May miss novel or altered behaviors |
| **Anomaly-based** | Compares activity with a baseline/model | May catch unusual, previously unknown patterns | Can produce false positives / require careful tuning |

An **IDS** detects and alerts; an **IPS** can enforce blocking decisions. The distinction depends on deployment and configuration.

## 3. Cryptography fundamentals

Cryptography can support **confidentiality**, **integrity**, **authentication**, and **digital signatures / authenticated public-key distribution**. It does **not** guarantee bug-free applications.

| Mechanism | Core concept | Examples |
| --- | --- | --- |
| **Symmetric encryption** | Same shared secret protects and recovers data | AES (with a suitable mode such as GCM) |
| **Asymmetric encryption / key agreement** | Related public/private keys or key pairs | RSA, elliptic-curve Diffie–Hellman |
| **Digital signatures** | Private key signs; corresponding public key verifies | RSA-PSS, ECDSA |
| **Cryptographic hash** | Fixed-length digest; not reversible decryption | SHA-256 |

**Hashing alone does not prove sender authenticity.** It needs authenticated context such as a MAC or validated signature.

### Why hybrid cryptography?

Public-key operations are relatively expensive and generally handle key establishment or protection of a compact secret. Efficient **symmetric authenticated encryption** then secures bulk application data. TLS 1.3 illustrates this combination.

### Key management

Key strength also depends on correctly implemented algorithms and the entire **key lifecycle**: generation, distribution, storage, rotation, use, revocation and destruction. A stolen private or symmetric secret defeats many cryptographic assurances irrespective of algorithm strength.

If each pair among *n* nodes needs a distinct shared secret, the number of unique pairwise keys is **n(n − 1)/2**. Ten nodes require 45 such keys; 100 require 4,950. PKI provides a scalable mechanism to authenticate public keys using trust anchors rather than directly sharing distinct secrets with every participant.

## 4. PKI and X.509 certificates

**Problem:** A public key published on a network may be silently replaced by an attacker. If a client trusts the substituted key as belonging to the intended recipient, confidentiality or authentication can fail.

**PKI** supplies certificate issuance and validation infrastructure to authenticate bindings between names/identities and public keys.

Typical X.509 certificate contents: subject, public key, issuer, serial number, validity period, extensions (e.g., subject alternative names, key usage), and issuer's signature.

**Certificate chain:** trusted **root CA** → issuing **intermediate CA** → **end-entity/server certificate**. A browser validates signatures and policy constraints, hostname, time validity and relevant certificate status conditions.

**Trust confusion:** A correct HTTPS certificate supports an authenticated, encrypted connection to a domain; it **does not prove** the website owner is ethical, its content is truthful, or its software is free of vulnerabilities. A malicious website can obtain a valid certificate.

## 5. Authentication and Identity & Access Management (IAM)

**Identification:** claiming an identity; **authentication:** verifying control of the expected authenticators; **authorization:** deciding which actions are permitted.

Three authenticator-factor categories:
- **Know:** passphrase or PIN.
- **Have:** hardware security key, token or a suitable bound device.
- **Are/do:** biometric or behavioral characteristic.

**MFA** combines *independent factor types*, e.g., a passphrase and possession of a security token. Two passwords are not two factors. Stronger authentication is selected in proportion to service **risk, sensitivity and cost**. Security keys/passkeys can offer stronger phishing resistance than many SMS-based approaches.

**Password security:** prefer unique, long passwords, password managers and immediate credential replacement if compromise is suspected. Avoid fixed periodic rotations without risk-based reason, and apply the organization's current policy.

### Federated identity

Users authenticate through an **Identity Provider (IdP)**, whose authentication result is consumed by a **Service Provider (SP) / Relying Party** under an established trust relationship.

- **OAuth 2.0** is principally an **authorization framework**, not a user-authentication protocol by itself.
- **OpenID Connect (OIDC)** is an authentication/identity layer on OAuth 2.0; it commonly issues ID tokens.
- **SAML** uses standardized assertions and is common in enterprise federation.

### Access control

| Model | Permission decisions depend on |
| --- | --- |
| **DAC** | Identity/owner-controlled permissions within system rules |
| **MAC** | Mandatory classification labels and centrally enforced policy |
| **RBAC** | Assigned role and the role's permissions |
| **ABAC** | Multiple attributes of user, resource, action and environment |

**RBAC** simplifies administration but can create **role explosion** when administrators define excessively granular roles. **ABAC** can express context-sensitive conditions such as active employee status + managed device + permitted department.

---

# Session 2 — Research Disciplines

## 6. Cyber operations and adversary behavior

**Offensive operations** target information/systems; **defensive operations** aim to prevent, detect, contain and respond to attacks. Authorized simulation commonly uses **red team** (adversary emulation) and **blue team** (defense).

Advanced targeted operations can involve multiple steps and extended timelines, with objectives such as espionage, sabotage or financial gain. They may cause collateral damage outside the intended victim.

### The Cyber Kill Chain

| Phase | What it represents |
| --- | --- |
| 1. **Reconnaissance** | Study potential target |
| 2. **Weaponization** | Prepare malicious capability |
| 3. **Delivery** | Bring payload/approach to target |
| 4. **Exploitation** | Trigger a vulnerability or weakness |
| 5. **Installation** | Establish malware/access mechanism |
| 6. **Command & Control** | Maintain communication with attacker-controlled infrastructure |
| 7. **Actions on Objectives** | Carry out the aim, e.g., information theft or sabotage |

The stages provide a useful model, **not a claim every attack follows the same sequence**. Early detection and disruption are especially valuable.

### MITRE ATT&CK

ATT&CK is a public, evidence-informed **knowledge base** of observed adversary behaviors, including mapping of groups and software to observed techniques.

- **Tactic = WHY**: the adversary's objective (e.g., initial access).
- **Technique = HOW**: the behavioral method (e.g., phishing).
- **Sub-technique**: a more specific variant.

ATT&CK supports threat modeling, detection engineering and incident analysis, but does not claim to represent every threat actor or intelligence service. The matrix and tactics evolve; check the official website for the version in use.

## 7. Cyber Threat Intelligence (CTI)

| Level | Typical content | Decision horizon |
| --- | --- | --- |
| **Technical** | IP/domain indicators, malware hashes, technical tools, observed artifacts | Short-term investigation/detection |
| **Operational / Tactical** | Campaigns, tactics/techniques/procedures (TTPs), adversary methods | Attack monitoring and operational planning |
| **Strategic** | Adversary motivations, long-term objectives, relevant industry risks | Leadership and investment priorities |

### Safe intelligence sharing: TLP

**Traffic Light Protocol** describes the permissible redistribution of information:
- **TLP:RED**: restricted to intended recipients.
- **TLP:AMBER**: limited sharing on a need-to-know basis within recipient's organization and with relevant clients/customers who need to protect themselves.
- **TLP:AMBER+STRICT**: further restricted to the recipient organization.
- **TLP:GREEN**: within the relevant community, not publicly.
- **TLP:CLEAR**: public sharing.

Apply the marking supplied by the originator and the current FIRST TLP guidance.

## 8. Artificial intelligence and cybersecurity

**AI4Cyber:** using AI for intrusion detection, malware analysis, CTI enrichment and incident-response support.

**Offensive AI:** AI-assisted deception (including synthetic media), attack automation and malicious-content development.

**Cyber4AI:** defending AI systems against threats including:
- **Training-data poisoning**: manipulating data used to fit or update a model.
- **Adversarial input**: crafting inference-time inputs to cause misclassification.
- **Prompt injection**: placing instructions in lower-trust content intended to redirect an AI application's behavior.
- **Jailbreaking**: trying to bypass model behavior constraints.
- **Supply-chain compromise**: threats through third-party models, libraries, data or services.

**ML paradigms:** supervised learning uses labeled examples; unsupervised learning finds patterns without target labels; reinforcement learning uses reward-based feedback. AI can help analysts but requires assessment of false positives, model limitations and oversight.

**EU AI Act:** an EU risk-based governance regime. Educational summaries often distinguish prohibited uses, high-risk systems, transparency duties and minimal-risk uses. Specific duties, definitions and phased application depend on the exact legal provisions and system use case; do not treat a simple four-tier diagram as a complete legal analysis.

## 9. Post-quantum cryptography (PQC)

A sufficiently capable **fault-tolerant quantum computer** running Shor's algorithm could undermine number-theoretic public-key systems (e.g., RSA, traditional finite-field Diffie–Hellman and elliptic-curve schemes). It does **not** mean that AES and cryptographic hashes become automatically useless.

**Post-quantum cryptography** seeks algorithms implementable on conventional computers that resist known classical and quantum attacks. Different designs use lattice-based, code-based or hash-based constructions (with different purposes and security assumptions).

**Why plan ahead?** Attackers may retain encrypted traffic today in hopes of decrypting it later when relevant quantum capabilities exist (**harvest now, decrypt later**). Long-lived confidentiality makes migration planning urgent even without a currently proven ability to break deployed large RSA keys using practical quantum computers.

**Governance checklist:** inventory cryptographic dependencies; identify long-lived sensitive information; plan crypto agility, standards-based replacement, vendor readiness, test interoperability and roll out changes in stages. Avoid claims that any candidate is absolutely 'quantum-proof'.

---

## Summary — distinctions that matter

- System security complements network encryption.
- Hypervisor ≠ OS kernel; VM isolation ≠ container isolation.
- TLS forward secrecy protects **past session secrets** against later long-term-key compromise, not endpoint compromise.
- IDS signatures match known patterns; anomaly detection identifies unusual behavior.
- Symmetric shared secrets ≠ asymmetric public/private keys.
- Certificate authenticity ≠ website trustworthiness.
- Authentication ≠ authorization; OAuth ≠ OIDC.
- RBAC = roles; ABAC = attributes.
- Cyber Kill Chain = broad stages; ATT&CK = tactics/techniques.
- Technical CTI = indicators; operational CTI = TTPs; strategic CTI = objectives.
- AI4Cyber = AI assists defense; Cyber4AI = security of AI systems.
- Quantum risk disproportionately affects classical asymmetric algorithms.

Next: [Independent practice](practice-questions.md) · [Public references](references.md).
