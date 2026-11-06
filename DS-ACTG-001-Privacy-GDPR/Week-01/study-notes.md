# Week 01 — Privacy, Data Protection & GDPR

> **Original community study notes (not official course material).** Topic coverage was checked against the Week 1 teaching outline and the GDPR. Explanations and scenarios below are independently written. **Updated: 2026-11-06.**

## Learning outcomes

By the end of this guide, be able to (1) distinguish privacy, data protection and information security; (2) identify personal data and GDPR actors; (3) apply the Article 5 principles; (4) choose a justified Article 6 basis; and (5) recognize the additional conditions for sensitive data.

## 1. Privacy vs data protection vs information security

| Concept | Main question | Example |
| --- | --- | --- |
| **Privacy** | How should individuals be protected against unwanted interference? | A student expects private communications not to be examined without justification. |
| **Data protection** | May personal data be collected and used this way, and under which conditions? | A university tells students why grades are recorded and how long records are retained. |
| **Information security** | How do we protect information against unauthorized access, changes and disruption? | Role-based access, backups and tamper-evident logs protect the student system. |

The **CIA triad** means **confidentiality** (authorized access only), **integrity** (accurate and protected against unauthorized modification), and **availability** (accessible when needed). Technical security is necessary, but does not by itself make a processing purpose lawful.

Privacy can involve **territorial privacy** (spaces), **privacy of the person** (freedom from unwanted intrusion) and **informational privacy** (control and safeguards around data use).

## 2. What counts as personal data?

Under [GDPR Article 4](https://eur-lex.europa.eu/eli/reg/2016/679/oj), personal data is information relating to an **identified or identifiable natural person**. Names, student numbers, identifiable images, location records and online identifiers can qualify. Combining several data points may identify someone even where a direct name is absent.

**Processing** includes collecting, recording, viewing, storing, altering, disclosing and deleting data. Keeping a database is processing even if records are rarely opened.

### Who does what?

| Role | Responsibility |
| --- | --- |
| **Data subject** | Person to whom the data relate |
| **Controller** | Determines purposes and essential means of processing |
| **Processor** | Processes on the controller's behalf, following its instructions |
| **Joint controllers** | Jointly determine purposes and means for a particular activity |
| **Supervisory authority** | Independent regulator overseeing compliance |

**Example (original):** A college decides why attendance records are needed and contracts a service provider to host them. The college is normally controller; the hosting provider is normally processor for that activity. Merely accessing data does not automatically create joint controllership.

## 3. Article 5 — key GDPR principles

| Principle | Practical test |
| --- | --- |
| Lawfulness, fairness, transparency | Is there a lawful ground, fair treatment and clear notice? |
| Purpose limitation | Was the purpose specified, and is any new purpose compatible or otherwise lawful? |
| Data minimisation | Are all requested fields actually necessary? |
| Accuracy | Is inaccurate information corrected or erased where appropriate? |
| Storage limitation | Is retention justified and reviewed? |
| Integrity and confidentiality | Are appropriate security measures in place? |
| Accountability | Can the controller **demonstrate** compliance? |

**Example:** If an event registration needs an email address to issue a ticket, collecting home address and continuous location data without a demonstrated need raises a minimisation concern.

Accountability is not merely complying: the controller must be able to evidence that compliance through appropriate documentation and practices.

## 4. Article 6 — the six lawful bases

| Lawful basis | General use case |
| --- | --- |
| Consent | A genuinely optional, specific processing purpose |
| Performance of a contract | Processing objectively needed to carry out a contract with the person |
| Legal obligation | Processing necessary to comply with an applicable legal duty |
| Vital interests | Necessary to protect someone's life in appropriate circumstances |
| Public task / official authority | Necessary for an applicable legally grounded public-interest or official function |
| Legitimate interests | Necessary, subject to a balancing assessment; not available to public authorities carrying out their public tasks |

**Do not default to consent.** The basis depends on the purpose, context and law. A privacy notice does not itself create a lawful basis.

### What makes consent valid?

Consent must be **freely given, specific, informed and unambiguous**; explicit consent is required for certain cases, including some Article 9 exceptions. A user should have a real choice, and withdrawal must be as easy as giving consent. A service should not ordinarily make optional personalized advertising a condition of access if it is not necessary for that service.

## 5. Article 9 — special categories

Examples include data revealing racial or ethnic origin, political opinions, religion or philosophical beliefs, trade-union membership, genetic data, biometric data used **to uniquely identify** a person, health data, and data about sex life or sexual orientation.

Processing these categories is generally prohibited **unless** an Article 9(2) exception applies; an appropriate Article 6 lawful basis is also needed. Possible exceptions depend on strict conditions, for example explicit consent, employment/social-protection law, vital interests, healthcare, substantial public interest, legitimate activities of qualifying not-for-profit bodies, or research/statistical purposes with required safeguards.

**Important distinction:** Having a contract does **not** automatically allow health-data processing. Criminal-conviction/offence data is governed by a separate rule in Article 10, not simply treated as another Article 9 category.

## 6. Scenario decision checklist

For any practical question, ask:

1. **What data?** Personal, special-category, or non-personal?
2. **Who decides why/how?** Controller, processor, or joint controllers?
3. **Why this use?** Defined purpose and appropriate Article 6 basis?
4. **Sensitive data?** If so, what Article 9(2) condition also applies?
5. **Proportional?** Minimise collection and justify retention.
6. **Transparent and secure?** Notice, access restrictions, safeguards.
7. **Demonstrable?** Can the controller document its decisions?

### Original mini-cases

- **Access-control CCTV:** Assess necessity and proportionality, security purpose, signs/notices, retention and a defensible legal basis. Visible signs are transparency, not automatically consent.
- **Public education records:** Depending on the applicable law and task, legal obligation or public task may be relevant. Do not assume that attending a university means students consented to every use.
- **Customer mailing list:** Consent for one purpose is not permission for unrelated advertising. Evaluate the new purpose, lawful basis, electronic marketing rules and transparency.
- **Health research:** Research involving health data may be possible under a valid Article 6 basis and a relevant Article 9 exception, with legal safeguards. Research is not automatically exempt.

## 7. Common misunderstandings

- "Privacy notice = permission" → **No**; transparency and lawful basis are separate.
- "A processor becomes a controller simply by seeing the data" → **No**; roles follow actual decision-making.
- "All biometric data is automatically special-category" → **Not necessarily**; Article 9 specifically addresses biometric processing for uniquely identifying a person.
- "If no one complains, accountability is satisfied" → **No**; demonstrating compliance is required.
- "A contract permits any use of special-category data" → **No**; separate Article 9 conditions apply.

## Self-study

Try the [original practice scenarios](practice-questions.md) **before** opening their explanations.

## Public sources and further reading

- [Official GDPR — Regulation (EU) 2016/679](https://eur-lex.europa.eu/eli/reg/2016/679/oj) — especially Articles 4–10.
- [European Data Protection Board (EDPB) guidelines](https://www.edpb.europa.eu/our-work-tools/general-guidance/guidelines-recommendations-best-practices_en)
- [Hellenic Data Protection Authority](https://www.dpa.gr/en)

This guide is a study aid, not legal advice, and does not reproduce the lecturer's slides or graded assessment.
