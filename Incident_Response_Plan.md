# Incident Response Plan

## Introduction

This Incident Response Plan (IRP) ensures consistent, effective, and efficient handling of information security events to minimize negative impacts on organizational operations, staff, and stakeholders. Developed by Frank Johnson, it leverages over three years of SOC experience to protect IT infrastructure and deliver client-focused outcomes.

Three guiding principles underpin this plan:  
- **Prove What You Know:** Assert facts based on verifiable evidence (e.g., packet analysis, SIEM logs), avoiding assumptions.  
- **Eliminate Possibilities:** Use failed assertions to narrow down causes, as demonstrated in threat hunting and incident triage.  
- **Seek Simplicity:** Prioritize the simplest, most actionable explanation for rapid resolution.

##### Acknowledgements
Adapted from the Cydea IR Plan template under the Creative Commons Attribution 4.0 International Public License. More details at [https://cydea.tools/ir-plan/](https://cydea.tools/ir-plan/).

## Coordinating Our Response

Coordination occurs primarily via secure communication channels suited for remote SOC operations. For real-time collaboration:  
- **GitHub Issues:** [github.com/FrankJohnson-cyber/incident-response](https://github.com/FrankJohnson-cyber) (placeholder for tracking).  
- **Email:** FRANKJSEC@gmail.com (for updates and stakeholder communication).  
- **Conference Call:** Available upon request via secure VoIP (e.g., Zoom, Teams).  

Alternative methods (e.g., encrypted email, phone) will be used if primary channels are compromised or unavailable. Key contacts are listed in [Key Contacts](#key-contacts).

## Roles and Responsibilities

This IRP assumes a virtual, cross-functional team formed ad-hoc, with roles assigned based on incident needs. Incident response takes priority over routine tasks. Typical roles include:  
- **Senior Management:** Approves critical decisions (e.g., system shutdowns).  
- **Triage Manager (TM):** Frank Johnson—reviews alerts, initiates IR process (aligned with Jr. SOC Analyst triage experience).  
- **Incident Manager (IM):** Frank Johnson—oversees incident lifecycle, coordinates teams, and documents progress (reflecting Help Desk & Security Analyst coordination).  
- **Technical Lead (TL):** Frank Johnson—leads technical analysis and remediation using tools like Wireshark and Sentinel (per resume skills).  
- **Investigators/Analysts:** Support technical tasks (e.g., packet analysis, log review).  
- **IT & Infrastructure:** Executes containment and recovery actions.  
- **Third Parties:** Engaged as needed (e.g., vendors, legal support).  

## Incident Response Process

### Overview

The process follows an OODA loop (Observe, Orient, Decide, Act) for flexibility across scenarios:  
![OODA Loop](https://github.com/cydea/ir-plan/raw/master/ooda-incident-response-process.png)

Stages: [Triage](#triage), [Observe](#observe), [Orient](#orient), [Decide](#decide), [Act](#act), [Recover](#recover), [Review](#review).

#### Playbooks
Tailored playbooks for common incidents include:  
- **Malware Detection and Removal:** Steps for identifying and eradicating malware using Defender and Wireshark.  
- **Network Breach Response:** Procedures for analyzing packet captures and isolating threats (from resume projects).  

### Triage

**Triage Manager (Frank Johnson)** assesses alerts to determine if an event warrants full IR mobilization.  
- Log all events in a tracking system (e.g., ServiceNow, GitHub Issues).  
- Use tools like Microsoft Sentinel and Wireshark to validate alerts.  
- Assign severity (S1–S4) and category per [Severity Matrix](#severity-matrix) and [Incident Categorisation](#incident-categorisation).  
- Escalate S1/S2 incidents to Senior Management.

#### Triage Checklist
- [ ] Log the incident  
- [ ] Record alert source (e.g., Sentinel, IDS/IPS)  
- [ ] Document initial findings (e.g., affected systems, timestamps)  
- [ ] Form a hypothesis (e.g., malware vs. misconfiguration)  
- [ ] Assign severity and category  
- [ ] Escalate if S1/S2  
- [ ] Mobilize Virtual IR Team  

### Observe

**Technical Lead (Frank Johnson)** gathers data using tools like Wireshark, Sentinel, and Defender.  
- Capture network traffic (e.g., PCAP files) and correlate with SIEM logs.  
- Example: Analyzed outbound traffic for C2 patterns during threat hunting.

#### Observe Checklist
- [ ] Identify required data (e.g., packet captures, AD logs)  
- [ ] Record hypothesis in incident log  
- [ ] Gather data from [Data Sources](#data-sources)  
- [ ] Collate external intelligence (e.g., OSINT)  

### Orient

**Incident Manager (Frank Johnson)** and Technical Lead analyze data to form a provable hypothesis.  
- Use Wireshark filters (e.g., `tcp.port == 4444`) to pinpoint anomalies.  
- Apply Analysis of Competing Hypotheses (ACH) for structured evaluation.

#### Orient Checklist
- [ ] Analyze data to understand the incident  
- [ ] Form testable hypotheses (e.g., phishing vs. insider threat)  
- [ ] Test hypotheses with observations  
- [ ] Record results in incident log  

### Decide

**Incident Manager** escalates to Senior Management for S1/S2 decisions.  
- Document decisions (e.g., isolate system, reset credentials) and rationale.

#### Decide Checklist
- [ ] Report facts in plain English  
- [ ] Confirm severity/category  
- [ ] Record decisions in log  

### Act

**Technical Lead** executes containment/remediation.  
- Actions: Block IPs via firewalls, isolate hosts, reset AD credentials.  
- Log all actions for cause/effect tracking.

#### Act Checklist
- [ ] Plan containment steps  
- [ ] Communicate to stakeholders  
- [ ] Execute and document actions  

### Recover

**Incident Manager** oversees return to BAU once Technical Lead confirms containment.  
- Restore systems using clean backups, apply patches.

#### Recover Checklist
- [ ] Confirm containment  
- [ ] Plan and implement recovery  
- [ ] Verify clean state  

### Review

**Incident Manager** conducts a blame-free post-incident review.  
- Assess response effectiveness and update playbooks.

#### Review Checklist
- [ ] Schedule review with team  
- [ ] Discuss lessons learned  
- [ ] Update knowledge base  

## Annexes

### Key Contacts
- **Incident Manager/Technical Lead:** Frank Johnson (FRANKJSEC@gmail.com, 404-388-8602)  
- **GitHub:** [github.com/FrankJohnson-cyber](https://github.com/FrankJohnson-cyber)  

### Severity Matrix
| Severity | Definition | Escalation |
|----------|------------|------------|
| S1       | Critical data breach, >80% systems down | Notify Senior Management within 1 hour |
| S2       | Partial outage, potential data risk | Notify within 4 hours |
| S3       | Minor team impact | Notify within 1 day |
| S4       | Minimal impact | No escalation |

### Incident Categorisation
- **Malware:** Ransomware, spyware  
- **System Intrusion:** Exploits, credential misuse  
- **Information Breach:** Unauthorized access  

### Data Sources
- **Network Traffic:** Wireshark PCAPs, firewalls, IDS/IPS  
- **SIEM Logs:** Microsoft Sentinel  
- **Endpoint Logs:** Defender, AD logs  

### Analysis of Competing Hypotheses
#### Hypotheses
| ID | Description |
|----|-------------|
| H1 | Malware infection via phishing |
| H2 | Insider data exfiltration |

#### ACH Table
| ID | Evidence | H1 | H2 |
|----|----------|----|----|
| 1  | Unusual outbound traffic | C  | C  |
| 2  | Phishing email detected | C  | I  |
