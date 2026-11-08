# Week 02 — Independent Practice Scenarios

> **Original community exercises**, created for general learning. These are **not** quotations, screenshots, reconstructions or answer keys from any course quiz. Try answering before opening the explanations.

## Session 1: Technologies

### 1. A company protects all API traffic with TLS, yet malware on a workstation reads confidential files. Which layer of the security program needs attention?

<details><summary>Reveal explanation</summary>

**Endpoint/system security.** TLS protects the transport channel, not plaintext exposed on a compromised endpoint. Consider patching, endpoint hardening, least privilege, monitoring and incident response.

</details>

### 2. Two separate virtual machines share one physical server. What component is responsible for controlling the virtual hardware and isolation boundaries?

<details><summary>Reveal explanation</summary>

A **hypervisor**. With Type 1 virtualization it runs directly over physical hardware. Isolation depends on the hypervisor, hardware configuration and maintenance.

</details>

### 3. A network monitor alerts when it sees a known malicious sequence of packets; another alerts when upload volume is unusually high for a workstation. Classify each detector.

<details><summary>Reveal explanation</summary>

The first is **signature-based** and the second **anomaly-based**. Either can generate false alarms. Anomalies are not necessarily attacks.

</details>

### 4. A company fears that compromise of a server's certificate private key next year will expose last year's recorded TLS sessions. Which security property is relevant?

<details><summary>Reveal explanation</summary>

**Forward secrecy.** Properly established ephemeral session secrets remain protected against *later compromise of that long-term key alone*. It does not cover already stolen plaintext or compromised session secrets.

</details>

### 5. A development team uses excellent encryption but stores the symmetric key in a public repository. What failed?

<details><summary>Reveal explanation</summary>

**Key management**, particularly protected storage and secret handling. Encryption algorithm strength cannot compensate for disclosure of the decryption key.

</details>

### 6. A browser accepts a correctly issued certificate for a newly registered website. Is the website therefore honest and free of phishing?

<details><summary>Reveal explanation</summary>

**No.** Certificate validation authenticates a binding to the domain under the relevant trust/policy rules. It does not guarantee trustworthy site content or owner behavior.

</details>

### 7. A login requires a password and a security key. Does a username and two passwords provide an equivalent number of authentication factor categories?

<details><summary>Reveal explanation</summary>

**No.** Password + possession of an independent security key crosses two factor categories. Two passwords both represent **knowledge**. The username is an identifier, not an authenticator factor.

</details>

### 8. A company grants access when a person works in Finance, has an active employment record and uses a managed device. Is the decision based only on an assigned role?

<details><summary>Reveal explanation</summary>

This is best described as **ABAC**, because the policy combines several attributes, including device context. **RBAC** instead centers on role assignments and role permissions.

</details>

### 9. An application wants to verify a user's login via an external identity provider. Is generic OAuth authorization alone the same as OpenID Connect authentication?

<details><summary>Reveal explanation</summary>

**No.** OAuth 2.0 is principally an authorization framework. **OIDC** extends it to support standardized identity/authentication responses, often using an ID token.

</details>

## Session 2: Research disciplines

### 10. A defender observes external collection of public contact details, followed later by malicious activity. Which high-level attack framework helps organize the phases?

<details><summary>Reveal explanation</summary>

The **Cyber Kill Chain** organizes conceptual phases including reconnaissance, delivery, exploitation and objectives. It is a simplified model rather than a mandatory sequence for every attack.

</details>

### 11. A SOC analyst maps a phishing behavior to the adversary objective of gaining entry to an environment. In ATT&CK, which is tactic and which is technique?

<details><summary>Reveal explanation</summary>

**Initial Access** is the **tactic** (why the attacker acts), while **phishing** is a **technique** (how the objective is pursued).

</details>

### 12. A threat bulletin contains malware hashes, a write-up of campaign TTPs, and an assessment of an adversary's three-year goals. Sort these by CTI level.

<details><summary>Reveal explanation</summary>

**Hashes → technical CTI; campaign TTPs → operational/tactical CTI; long-term goals → strategic CTI.**

</details>

### 13. A security company labels sensitive threat intelligence TLP:AMBER. Can a recipient freely post it on a public forum?

<details><summary>Reveal explanation</summary>

**No.** TLP:AMBER imposes need-to-know redistribution limits. Check the originator's marking and current FIRST guidance before sharing.

</details>

### 14. An ML intrusion detector starts misclassifying attacks after an attacker secretly altered its training data. Which risk best describes this?

<details><summary>Reveal explanation</summary>

**Training-data poisoning**. The attacker manipulated information used to train or update the model, changing its learned behavior.

</details>

### 15. An engineering team is designing a service that must protect sensitive traffic for 20 years. Why might it adopt quantum-resistant key establishment in advance?

<details><summary>Reveal explanation</summary>

Classical public-key mechanisms may be vulnerable to sufficiently powerful future quantum computing. **Harvest now, decrypt later** makes data with long confidentiality lifetimes especially relevant to early post-quantum migration planning.

</details>

---

## Knowledge checklist

- [ ] Explain why TLS is not an endpoint-security solution.
- [ ] Distinguish signature-based and anomaly-based monitoring.
- [ ] Explain key lifecycle management and certificate trust chains.
- [ ] Distinguish IdP from SP; OAuth from OIDC.
- [ ] Identify RBAC versus ABAC using new scenarios.
- [ ] Recite the seven Kill Chain phases and ATT&CK tactic/technique distinction.
- [ ] Categorize technical, tactical/operational and strategic CTI.
- [ ] Explain training-data poisoning versus inference-time adversarial inputs.
- [ ] Describe why PQC migration matters to long-lived confidentiality.

[Return to study notes](study-notes.md) · [Public references](references.md).
