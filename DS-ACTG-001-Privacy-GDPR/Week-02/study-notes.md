# Week 02 — European Privacy and Data Protection: Legal & Regulatory Framework

> Original student study notes based on the Week 2 **topic outline**, not a reproduction of teaching slides. Study aid, not legal advice. Dates and legal interpretation should be verified against the [primary sources](references.md).

## Learning goals

- Trace the shift from human-rights privacy protections to rules regulating personal-data processing.
- Distinguish **UN**, **Council of Europe**, **EU** and their courts.
- Explain the legal significance of the **EU Charter**, **TFEU** and **GDPR**.
- Identify who **proposes**, **adopts**, **supervises** and **interprets** EU data-protection law.
- Apply the correct framework to actors, purposes and incidents: GDPR, EUDPR, LED, ePrivacy, NIS2, CRA, AI Act, DSA and Data Act.

---

## Part 1 — How European data-protection law developed

### 1. Privacy rights came before modern databases

**Privacy** protects private life and communications against unjustified interference; **data protection** sets concrete safeguards for the processing of information about people.

| Year | Instrument | Legal character / why it matters |
| --- | --- | --- |
| **1948** | **Universal Declaration of Human Rights (UDHR), Article 12** | UN declaration recognizing privacy; not a treaty directly binding as such |
| **1950** | **European Convention on Human Rights (ECHR), Article 8** | Binding Council of Europe treaty safeguarding private/family life, home and correspondence |
| **1980** | **OECD Privacy Guidelines** | Non-binding international principles for privacy and cross-border information flows |
| **1981** | **Convention 108** | Binding Council of Europe treaty specifically for personal-data protection, implemented through domestic law |
| **1995** | **Data Protection Directive 95/46/EC** | Harmonized national data-protection laws via **transposition** |
| **2000 / 2009** | **EU Charter of Fundamental Rights** | Proclaimed in 2000; legally binding with the Lisbon Treaty in 2009 |
| **2016 / 2018** | **GDPR (EU) 2016/679** | Adopted in 2016; applies from **25 May 2018** as a directly applicable EU regulation |

**What problem did harmonization solve?** By the 1970s, organizations could move personal data across borders, while countries imposed differing safeguards. Common standards aimed both to protect people and to avoid regulatory gaps and unnecessary trade barriers.

### 2. OECD principles and Convention 108

The OECD Guidelines introduced a recognizable set of privacy principles:

1. Collection limitation
2. Data quality
3. Purpose specification
4. Use limitation
5. Security safeguards
6. Openness
7. Individual participation
8. Accountability

These influenced the later development of European data-protection law. **OECD = soft law**; **Convention 108 = binding international treaty**. Convention 108 also provided protections relating to sensitive categories of information.

**Convention 108+** is the modernization protocol adopted in 2018; adoption and entry into force are different legal events. Verify its implementation status from the Council of Europe rather than inferring it from the date in a course slide.

### 3. The 1995 Directive vs GDPR

The 1995 Directive sought **protection of fundamental rights** while permitting the **free movement of personal data** in the EU. It addressed lawful processing, defined purposes, individual rights, independent oversight and international transfers.

| | Directive 95/46/EC | GDPR |
| --- | --- | --- |
| Type | EU **Directive** | EU **Regulation** |
| National-law implementation | Requires **transposition** | **Directly applicable**, though allows particular national rules |
| Principles | Lawful grounds, purpose limits, data quality and rights | Retains and develops these principles |
| Later developments | Different national implementation could create fragmentation | Greater accountability, cooperation, rights, breach notification and stronger enforcement |

**Key point:** GDPR did **not** invent lawfulness, purpose limitation, supervisory authorities or free data movement; those already existed in the earlier framework.

### 4. Charter and TFEU — fundamental-rights foundation

| Provision | What it protects / establishes |
| --- | --- |
| **Charter Article 7** | Respect for private and family life, home and communications |
| **Charter Article 8** | Protection of personal data; fair processing for specified purposes and lawful basis; access/rectification; independent supervision |
| **TFEU Article 16** | Right to personal-data protection and legislative basis for EU data-protection rules |
| **Charter Article 51** | Charter binds EU institutions; Member States when **implementing EU law** |
| **Charter Article 52(1)** | Conditions for limitations on Charter rights: lawful, respect the essence, legitimate objective, necessary and proportionate |

**Do not conflate the courts:** The **ECtHR in Strasbourg** decides ECHR cases concerning **States**. The **CJEU in Luxembourg** interprets EU law and can rule EU acts invalid.

**Proportionality illustration:** Even where a communications-surveillance measure pursues serious-crime prevention, indiscriminate retention and inadequate access safeguards may exceed what is necessary. This was central to **Digital Rights Ireland (2014)**, where the CJEU invalidated the EU Data Retention Directive. The ECHR case **S. and Marper v UK (2008)** also illustrates why indiscriminate retention of biometric information concerning people not convicted of offences can be disproportionate.

---

## Part 2 — Who makes, enforces and interprets the law?

### 5. EU institutions and the legislative process

**Ordinary legislative procedure:**

**European Commission proposes → European Parliament and Council of the EU jointly adopt → CJEU interprets and reviews legality.**

| Actor | Role |
| --- | --- |
| European Commission | Legislative proposals; monitors Member State compliance with EU law; adopts adequacy decisions |
| European Parliament | Directly elected co-legislator |
| Council of the **European Union** | Ministers representing Member State governments; co-legislator |
| **European Council** | Heads of state or government; sets broad political direction, **not** a co-legislator |
| **Council of Europe** | Separate international organization, **not an EU institution**; ECHR and Convention 108 |
| CJEU | Authoritative EU-law interpretation and review of EU acts |

### 6. Supervisory bodies — DPA vs EDPB vs EDPS

- **National Data Protection Authorities (DPAs)** receive complaints, investigate, issue corrective orders and may impose administrative fines within their powers (GDPR Articles **57–58**). Example: the Hellenic Data Protection Authority.
- **European Data Protection Board (EDPB)** promotes consistent interpretation and can adopt binding decisions to settle qualifying disagreements between authorities (Article **65**). Its general guidelines are not legislation.
- **European Data Protection Supervisor (EDPS)** supervises personal-data processing by **EU institutions and bodies**, generally under **Regulation (EU) 2018/1725**; it is not the routine GDPR regulator for private companies.

**Important:** The **Commission does not impose GDPR administrative fines on ordinary companies**; competent DPAs do. A DPA does not ordinarily award damages to individuals: compensation is pursued through the relevant courts under GDPR Article **82**, requiring infringement, damage and a causal link.

### 7. Cross-border GDPR cases: the one-stop-shop mechanism

Where applicable, the authority associated with an organization's **main EU establishment** acts as **Lead Supervisory Authority**, working with other concerned DPAs (Articles **56, 60**). A person can still complain to their local competent DPA (Article **77**). Where a dispute meets the Article 65 conditions, the **EDPB** may settle it through a binding decision.

A **preliminary reference** under **TFEU Article 267** is a legal question from a national court to the CJEU, **not an appeal**. The CJEU answers the EU-law interpretation/validity issue; the national court resolves the underlying case. National courts cannot themselves declare EU acts invalid.

**Schrems I (2015)** is a useful example: a complaint about EU–US transfers was considered through an Irish DPA, a national court and a preliminary ruling; the CJEU invalidated the then-existing **Safe Harbour** adequacy decision. This is historical case law, **not a statement that Safe Harbour is the current transfer framework**.

---

## Part 3 — GDPR within the broader EU legal landscape

### 8. Which regime governs which personal-data processing?

| Instrument | Typical activity | Relationship to GDPR |
| --- | --- | --- |
| **GDPR** | Most covered public/private personal-data processing | General framework |
| **EUDPR** — Regulation (EU) 2018/1725 | EU institutions and bodies processing personal data | Separate regime **instead of GDPR** for that processing |
| **Law Enforcement Directive (LED)** — Directive (EU) 2016/680 | Competent authorities processing for covered criminal-law purposes | Separate regime **instead of GDPR** for those purposes |
| **ePrivacy Directive** | Communications confidentiality, device access/cookies, electronic marketing | More specific rules **alongside GDPR**, as relevant |

**Purpose matters:** A police department investigating a criminal offence may process under the LED; its ordinary employee-payroll processing generally falls under the GDPR. An EU institution's staff records generally fall under the EUDPR.

**Cookies nuance:** Consent is generally required for non-essential storage/access to terminal-equipment information, subject to particular ePrivacy exceptions; this rule is not limited to information that qualifies as personal data.

### 9. Cybersecurity, products, AI and platform regulation

| Instrument | Focus | Example |
| --- | --- | --- |
| **NIS2** — Directive (EU) 2022/2555 | Cybersecurity governance, risk management and significant-incident reporting for covered **organizations** | Cloud provider or health-sector entity meeting scope criteria |
| **Cyber Resilience Act (CRA)** — Regulation (EU) 2024/2847 | Security requirements for covered **products with digital elements** and mainly manufacturers' responsibilities | Connected device manufacturer manages vulnerabilities |
| **AI Act** — Regulation (EU) 2024/1689 | Development, placing on the market and deployment of AI systems in scope | Obligations depend on system classification and actor's role |
| **Digital Services Act (DSA)** — Regulation (EU) 2022/2065 | Due-diligence duties of online intermediaries and platforms | Marketplace transparency and platform responsibilities |
| **Data Act** — Regulation (EU) 2023/2854 | Data access and sharing for connected products and related services; cloud switching | A product user requests sharing of relevant diagnostics with a third party |

**NIS2 ≠ GDPR:** An incident can trigger cybersecurity reporting **and** a separate GDPR personal-data-breach assessment. The triggers, authorities and timeframes differ. Under GDPR Article **33**, a controller generally reports a personal-data breach unless the risk to people's rights and freedoms is unlikely; notification is without undue delay and, where feasible, within 72 hours. NIS2 Article **23** has its own phased notification requirements for significant incidents.

**CRA ≠ NIS2:** CRA focuses on covered digital products and their economic operators; NIS2 focuses on covered organizations/sectors. Some CRA notification requirements apply from September 2026, while many main product requirements apply from December 2027; check current legal applicability in any real case.

**Parallel application example (independently authored):** An EU-based logistics business operates a connected cold-chain sensor network and uses a cloud provider. Depending on the facts, GDPR may govern employee location logs, the manufacturer may face CRA obligations for the sensor product, and a sufficiently covered cloud provider may face NIS2 duties. One legal framework does **not** erase the others.

### 10. Four-question checklist for any scenario

1. **Scope:** Is the applicable personal-data regime GDPR, LED or EUDPR?
2. **Specific rules:** Does ePrivacy, for example, add special communications rules?
3. **Parallel duties:** Do NIS2, CRA, AI Act, DSA or Data Act create additional obligations?
4. **Relationship clauses:** How do the relevant acts resolve overlap or conflicts?

Apply each law only after identifying **the actor, the activity, the data, the legal scope and the event triggering obligations**.

---

## Quick distinctions for revision

- **UDHR**: non-binding declaration as such. **ECHR**: binding Council of Europe treaty.
- **OECD**: non-binding principles. **Convention 108**: binding international data-protection treaty.
- **Directive**: national transposition. **Regulation**: direct applicability.
- **Charter Art 7**: privacy. **Charter Art 8**: data protection.
- **CJEU**: EU law (Luxembourg). **ECtHR**: ECHR (Strasbourg).
- **Commission**: proposes EU law. **Parliament + Council of the EU**: co-legislate.
- **DPA**: investigates and can fine. **EDPB**: consistency and certain disputes. **EDPS**: EU institutions.
- **NIS2**: organizations. **CRA**: digital products.
- **GDPR** protects personal data; **ePrivacy** may add communication-specific rules.
- **EUDPR and LED** may apply **instead of GDPR** for particular processing activities.

## Further learning

See [original self-check scenarios](practice-questions.md) and [official legislation and case law](references.md).

> Important academic-integrity note: this guide does not publish course slides or any assessed question, assessment answer key or instructor-created case exercise.
