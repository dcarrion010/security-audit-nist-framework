# Internal IT Security Audit & Regulatory Compliance Assessment

**Target Entity:** Botium Toys Inc.  
**Framework:** National Institute of Standards and Technology Cybersecurity Framework (NIST CSF v1.1)  
**Compliance Standards Evaluated:** PCI DSS v4.0 | GDPR (EU) | SOC 2 (Type I / Type II)  
**Initial Risk Rating:** 8 / 10 (Critical / High Risk)  
**Lead Auditor:** David Carrión Juan  

---

## 1. Executive Summary

Botium Toys is an expanding retail and e-commerce enterprise operating an on-premises headquarters, storefront, and adjacent warehouse, supporting growing operations across the United States and international markets (including the European Union). 

This internal audit evaluated the current technical, physical, and administrative control environment to identify critical operational risks, technical debt, and non-compliance liabilities.

The audit revealed an initial **Risk Score of 8/10**. While baseline physical controls, network firewall filtering, and managed endpoint antivirus are operational, significant deficiencies exist in access management, cryptographic controls, threat detection, and disaster recovery. Critical data assets—including customer Personal Identifiable Information (PII) and Payment Cardholder Data (CHD)—are currently exposed to insider threats and severe regulatory non-compliance penalties.

---

## 2. Audit Scope & Asset Classification

The audit scope covers all enterprise-managed technical infrastructure, data repositories, physical perimeters, and regulatory processes.

### 2.1 Managed Asset Inventory
* **Physical Infrastructure:** Single headquarters facility containing administrative offices, retail storefront, and warehouse inventory.
* **Endpoints:** Workstations, laptops, corporate mobile devices, docking peripherals, and retail POS terminals.
* **Network & Systems:** Internal LAN routing and switching, border firewall, telecommunications, retail database, accounting, and inventory management platforms.
* **Data Repositories:** On-premises relational databases storing customer billing profiles, unencrypted primary account numbers (PAN), and EU user records.
* **Legacy Systems:** Out-of-support business systems requiring manual operational maintenance.

---

## 3. NIST CSF Controls Assessment

Evaluation of administrative, technical, and physical safeguards across the core functions of the NIST Cybersecurity Framework.

| Control Identifier | Domain / Type | Status | Technical Audit Finding |
| :--- | :--- | :---: | :--- |
| **Least Privilege** | Administrative / Preventive | **FAIL** | Universal read/write privileges: all corporate employees possess unrestricted access to internal databases containing sensitive customer and payment records. |
| **Separation of Duties** | Administrative / Preventive | **FAIL** | Operational and administrative functions are not segmented across distinct roles, increasing internal fraud and privilege escalation risks. |
| **Password Policies** | Administrative / Preventive | **PASS (Deficient)** | A baseline policy document exists; however, complexity requirements are nominal (lacking special character enforcement and minimum length standards). |
| **Centralized Password Management** | Technical / Preventive | **FAIL** | No password manager or privileged access management (PAM) solution deployed; password resets and credential tracking are handled manually. |
| **Enterprise Firewall** | Technical / Preventive | **PASS** | State-aware border firewall active with operational filtering rules managing ingress and egress traffic. |
| **Intrusion Detection System (IDS)** | Technical / Detective | **FAIL** | No signature-based or anomaly-based IDS/IPS deployed to monitor internal network segments or DMZ traffic. |
| **Antivirus Protection** | Technical / Corrective | **PASS** | Endpoint antivirus deployed on user machines and actively monitored by internal IT staff. |
| **Data Encryption** | Technical / Deterrent | **FAIL** | Complete absence of cryptographic safeguards: customer credit card numbers and sensitive data are stored, transmitted, and processed in plaintext. |
| **Disaster Recovery & Backups** | Technical / Corrective | **FAIL** | Zero automated or manual backup procedures in place; lack of a formal Disaster Recovery Plan (DRP) leaves operations fully vulnerable to ransomware. |
| **Legacy Systems Maintenance** | Operational / Preventive | **PASS (Deficient)** | End-of-life legacy platforms are monitored manually by staff, but lack structured patching windows, isolation, and standard intervention procedures. |
| **Physical Access Controls** | Physical / Preventive | **PASS** | Physical locks operational across the storefront, corporate offices, and inventory warehouse. |
| **Surveillance (CCTV)** | Physical / Detective | **PASS** | Functional CCTV infrastructure covering physical entryways and internal high-value storage areas. |
| **Fire Detection & Suppression** | Physical / Corrective | **PASS** | Operating smoke detectors and certified sprinkler systems across facilities. |

---

## 4. Regulatory Compliance Evaluation

### 4.1 Payment Card Industry Data Security Standard (PCI DSS)
* **Overall Status: Critical Non-Compliance**
* **Access Control (Req. 7):** Non-compliant. Cardholder data is accessible to unauthorized general employees.
* **Data Protection (Req. 3 & 4):** Non-compliant. Primary Account Numbers (PAN) and authentication details are stored unencrypted in local relational databases and transmitted in plaintext.
* **System Hardening & Credential Hygiene (Req. 8):** Non-compliant. Passwords lack multi-factor authentication (MFA) and enterprise vault enforcement.
* **Risk Exposure:** Statutory merchant fines, increased transaction processing fees, and potential revocation of card processing privileges.

### 4.2 General Data Protection Regulation (GDPR - EU Operations)
* **Overall Status: High Non-Compliance Risk**
* **Confidentiality & Integrity (Art. 5 & 32):** Non-compliant. Personal Identifiable Information (PII) of European customers is stored unencrypted and unprotected from internal privilege abuse.
* **Asset & Data Governance:** Non-compliant. Absence of an official asset classification schema and data flow inventory.
* **Incident Notification Protocol (Art. 33):** **Compliant.** Internal IT has documented and enacted an operational 72-hour breach notification plan for EU data subjects.
* **Risk Exposure:** Administrative fines up to €20M or 4% of global annual turnover under GDPR Article 83.

### 4.3 Service Organization Control (SOC 2 - Type I / II)
* **Trust Services Criteria: Failed (Confidentiality, Privacy & Access)**
* Logical access controls fail trust criteria due to over-permissive user rights and lack of role-based segregation.
* **Data Availability & Integrity:** **Passed.** Infrastructure availability and database integrity validation mechanisms are currently maintained by IT operations.

---

## 5. Strategic Remediation Roadmap

A structured three-phase engineering roadmap designed to remediate high-severity liabilities and lower the organizational risk score from **8/10 to <3/10**.

    [Phase 1: Weeks 1-3] ──> Role-Based Access Control (RBAC) + AES-256 / TLS 1.3 Encryption
            │
    [Phase 2: Weeks 4-8] ──> Automated 3-2-1 Backups + Network Segmentation + IDS Deployment
            │
    [Phase 3: Weeks 9-12] ─> Centralized Identity/MFA + Legacy Isolation + Asset Inventory

### Phase 1: Critical Risk Containment (Weeks 1 - 3)
* **Role-Based Access Control (RBAC):** Restrict database access exclusively to authorized billing and accounting services; revoke general staff database privileges under the principle of least privilege.
* **Cryptographic Controls:** Implement AES-256 encryption for data at rest across all customer and transaction tables. Enforce TLS 1.3 for all in-transit communications and e-commerce transactions.
* **Cardholder Data Environment (CDE) Isolation:** Segment payment processing systems using dedicated virtual local area networks (VLANs) to restrict the scope of PCI DSS audits.

### Phase 2: Resilience & Threat Detection (Weeks 4 - 8)
* **Automated 3-2-1 Backup Implementation:** Establish immutable, encrypted daily backup routines with offsite storage to protect against ransomware and data corruption. Formulate baseline Disaster Recovery (DRP) and Business Continuity runbooks.
* **Network IDS Deployment:** Install a network-based Intrusion Detection System (e.g., Suricata or Snort) at perimeter and internal choke points to detect anomalous traffic, port scans, and unauthorized lateral movement.

### Phase 3: Identity Hygiene & Operational Governance (Weeks 9 - 12)
* **Centralized Identity & Access Management (IAM):** Implement a centralized enterprise credential management solution. Enforce a minimum 12-character alphanumeric complexity policy and mandate Multi-Factor Authentication (MFA) across all administrative and remote access vector points.
* **Legacy Systems Isolation:** Place end-of-life systems behind dedicated firewall rules with strict ingress filtering, scheduling explicit maintenance intervals pending system decommissioning.
* **Asset Identification (NIST CSF - ID.AM):** Execute an automated and physical inventory audit to index all enterprise hardware, software dependencies, and sensitive data flows.

---

## 6. Audit Conclusions

Botium Toys possesses adequate physical protection and perimeter firewalling, but critical software, identity, and cryptographic controls have not kept pace with company growth. 

Immediate remediation of database encryption and privilege segmentation will neutralize the most severe regulatory liabilities under PCI DSS and GDPR, while the deployment of automated backups and IDS monitoring will establish resilient baseline security operations.
