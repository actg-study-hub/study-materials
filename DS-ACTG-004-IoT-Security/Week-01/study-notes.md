# IoT Security — Week 01: Original Study Notes

> Independently written introduction to general IoT security concepts. Not a lecture transcript or official course guide. See [references](references.md).

## 1. Internet of Things and cyber-physical systems

**IoT** combines physical objects, embedded software, sensing/actuation, and communications. A **sensor** measures a property of the physical world; an **actuator** changes the physical world in response to a command. A connected controller may do both.

Examples: a humidity probe measures soil conditions; an electrically controlled valve regulates irrigation. Cybersecurity must consider both digital information and possible physical consequences.

## 2. Four-layer conceptual architecture

| Layer | Function | Example assets |
| --- | --- | --- |
| **Perception** | Sensing and physical actuation | Sensors, relays, embedded firmware, device secrets |
| **Network** | Transfer data and bridge networks | Radios, gateways, uplinks, session keys |
| **Middleware** | Collect, process and store data | Brokers, registries, databases, cloud APIs |
| **Application** | Provide user services | Dashboards, mobile apps, user sessions |

These layers are an **analytical model**, not an instruction that every implementation must run four independent servers.

### Example flow

A battery-powered sensor reports a reading using a short-range non-IP protocol → a hub bridges it to an IP-based service → backend middleware stores the reading → a mobile dashboard displays it. Commands to an actuator may travel in the opposite direction.

### Assets and trust boundaries

An **asset** is something worth protecting, such as data, credentials, availability, equipment or safety. A **trust boundary** separates components or domains with different authority or exposure.

- Physical device ↔ people who can access its enclosure.
- Trusted local link ↔ outside network.
- Vendor service ↔ other tenants and external clients.
- Authenticated user session ↔ unauthenticated public access.

A sound first analysis identifies components, layers, assets, data flows and boundaries **before** choosing controls or conducting authorized tests.

## 3. IoT versus classical IT

IoT deployments often differ because of **constrained CPUs/memory/batteries**, physical exposure, heterogeneous fleets, long device lifetimes, limited patch support and possible safety consequences. Not every IoT product has these constraints, but all should be considered.

Adding Wi-Fi, a vendor cloud and a mobile app to a previously isolated device creates new dependencies and possible attack paths. Connectivity increases the **attack surface** even when core device functionality is unchanged.

## 4. Interdisciplinary security

IoT security spans hardware interfaces, embedded software, OS security, networking, cryptography, APIs and operations. A device can encrypt its radio link correctly but still leak measurements through an unauthenticated backend API. **Encrypted transport does not substitute for authorization.**

## 5. MQTT and publish/subscribe

MQTT commonly uses a **broker** to route messages from publishers to subscribers using **topics**. Example fictitious topic: `training/greenhouse/temperature`. Topic access must be properly scoped. TCP port **1883** is commonly used for MQTT without TLS, and **8883** for MQTT over TLS; neither port number guarantees good authentication or per-topic authorization.

For a real deployment use mutually appropriate authentication, access-control lists, secure transport and network exposure policies. Do not query unknown or production brokers without permission.

## 6. Mirai and widespread insecure devices

The 2016 **Mirai** botnet demonstrated how exposed IoT devices with factory credentials could be enrolled into massive distributed denial-of-service attacks. General mitigations: eliminate shared default credentials, disable unused remote-management services, restrict network exposure, deploy secure updates, monitor abnormal behavior and manage device inventory.

## 7. NISTIR 8228: organizational IoT risk considerations

[NISTIR 8228](https://csrc.nist.gov/pubs/ir/8228/final) addresses **cybersecurity and privacy risks** introduced by IoT devices in organizations. Think about deployment context, the device's interaction with the physical world, manageability, data flows, operational effects and the overall risk to systems and people.

## 8. NISTIR 8259A: device cybersecurity core baseline

[NISTIR 8259A](https://csrc.nist.gov/pubs/ir/8259/a/final) identifies six general device cybersecurity capabilities:

| Capability | What it supports |
| --- | --- |
| 1. **Device Identification** | Unique logical/physical device identification |
| 2. **Device Configuration** | Authorized modification and restoration of settings |
| 3. **Data Protection** | Protection of stored and transmitted data |
| 4. **Logical Access to Interfaces** | Restricted local and network interfaces |
| 5. **Software Update** | Authorized, authenticated and verified updates |
| 6. **Cybersecurity State Awareness** | Reporting relevant device security state |

The baseline specifies **what capability to provide**, not a single mandated hardware/software implementation. Physical tamper resistance may be valuable but is not a separately named capability in the six-item baseline.

**Distinction:** NISTIR 8228 examines **risk management**; NISTIR 8259A describes **device capabilities** supporting security controls.

## 9. Original scenario: connected greenhouse

A greenhouse monitors temperature and moisture, forwards readings via a gateway to cloud storage and allows staff to operate an irrigation valve in an app.

- Perception: sensors and valve actuator.
- Network: radio links, gateway and IP connectivity.
- Middleware: backend database and control API.
- Application: staff dashboard.
- Sensitive assets: device pairing secrets, account sessions, environmental readings, actuator commands.
- Boundaries: physical equipment/local network/cloud/customer account.

Priority controls might include secure pairing, permission checks on actuator commands, verified firmware updates and monitoring of abnormal control behavior. Availability and physical equipment safety deserve explicit risk analysis.

## 10. Ethics and coursework

Only perform security testing on devices/services you own or are **explicitly authorized** to test. CTFs are a lawful training format when used in the designated environment and rules. Course graded challenges, flags, prompts and solutions should remain private; participants should follow the current institution's individual-work and academic-integrity requirements.

## Recall checklist

- [ ] Distinguish sensor and actuator with your own scenario.
- [ ] Map all four layers and list assets and boundaries.
- [ ] Explain why physical exposure and patching matter in IoT.
- [ ] Describe MQTT publisher, broker, subscriber and topics.
- [ ] Describe Mirai's historical security lesson.
- [ ] Recall all six NISTIR 8259A capabilities.
- [ ] Differentiate NISTIR 8228 from 8259A.
