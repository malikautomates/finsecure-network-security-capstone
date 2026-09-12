# Network Security Policy — FinSecure Technologies Inc.

**Policy Version:** 2.0 (rebuilt — renumbered, gaps closed, two new sections added; see changelog at the end)
**Approval Authority:** Chief Information Security Officer (CISO)
**Effective Date:** 2024-11-08
**Annual Review:** Yes — Next Review Date: 2025-11-08

## 1. Purpose

This Network Security Policy exists to protect the confidentiality, integrity, and availability of FinSecure Technologies Inc.'s financial information, with particular attention to its B2B network relationships. It codifies the compliance requirements of SOX, PCI DSS, and GLBA, and establishes controls for FinSecure's digital assets and its dealings with external entities such as GlobalTech Industries.

## 2. Scope

This policy applies to all personnel, agents, and business associates with access to FinSecure's network systems, including Active Directory servers, web servers, PostgreSQL databases, SFTP servers, Redis cache servers, and B2B infrastructure connecting to GlobalTech Industries.

## 3. Information Security Principles

- **Confidentiality** — information is disclosed only to those with a demonstrated business need.
- **Integrity** — data integrity is protected through encryption and routine audits of data-handling procedures.
- **Availability** — authorized users have access to the data they need, when they need it.

## 4. Key Network Security Components

### 4.1 Risk Management and Incident Response
- **Risk assessments**: periodic assessment of vulnerabilities in critical areas such as web servers and authentication (maintained in the [risk register](../risk-assessment/risk-register.md)).
- **Incident Response Team (IRT)**: led by the CISO; handles incidents through predefined processes, documents them in the SIEM, and reviews them monthly.
- **Mitigation and response**: risk mitigation strategies and root-cause analysis, with regular incident-response testing.

### 4.2 Access Control, Password, and Encryption Standards
- **Active Directory & AAA server**: Secure LDAP with a dedicated AAA server centralizing group policy, authentication, authorization, and accounting.
- **Role-Based Access Control (RBAC)**: permissions defined by role, following least privilege, in line with SOX and PCI DSS.
- **VPN for remote access**: MFA required for every remote session (see Section 5).
- **Password requirements**: minimum 12 characters, mixing uppercase, lowercase, numbers, and symbols.
- **Encryption standards**: AES-256 at rest; TLS 1.2 or later in transit; documented key-management practices.

### 4.3 Web and Application Server Security
- **WAF**: formally deployed in front of the DMZ and Web Application Server Zone against SQL injection, XSS, and similar application-layer attacks.
- **SSL/TLS certificates**: all communications encrypted in transit.
- **Data encryption / TDE**: Transparent Data Encryption on PostgreSQL servers.
- **Cloud VPN and cloud database controls**: encryption standards, access controls, and periodic review for any cloud-hosted database or VPN endpoint.

### 4.4 Secure Intranet and VLAN Segmentation
Access between the HR, Finance, and IT VLANs is controlled to prevent cross-VLAN movement in the event of a breach in any one segment.

### 4.5 Monitoring, Logging, and Intrusion Detection
- **Continuous monitoring**: real-time SIEM-based monitoring with automated alerting.
- **IDS/IPS**: detects and blocks unauthorized access attempts.
- **Log audits**: regular, scheduled review of server, network device, and firewall logs.

### 4.6 Secure File Transfer, Synchronization, and Scheduling
- **SFTP**: encrypted transfer with role-based access control lists — key-based authentication required, default credentials prohibited.
- **Data synchronization**: daily between AD and other critical systems; every 4 hours for data servers.
- **Patch management**: critical patches within 48 hours; routine patches weekly.
- **Testing**: semi-annual penetration testing; monthly vulnerability scans.

### 4.7 Physical and Role-Based Access Control
- **Physical access**: restricted to authorized personnel via RFID card access to the Tier-3 data center, with monthly review of access logs.
- **Access reviews**: biannual review to keep permissions aligned with job roles.
- **Access revocation**: within 24 hours of termination or role change.

### 4.8 Reporting and SLAs
- **Incident reporting**: reported to the CISO/IRT within 24 hours; monthly incident summaries to management.
- **SLA resolution times**: high priority within 24 hours, medium within 72 hours, low within a week.
- **Annual review**: the IRT conducts an annual SLA and incident review.

## 5. Remote Access and Removable Media

This section formalizes the remote-access framework already implemented in the [network redesign](../report/02-network-design-and-implementation.md) and [Zero Trust rollout](../report/05-zero-trust-architecture.md).

- **VPN access**: all remote sessions terminate at the NGFW over an encrypted VPN tunnel, routed only to the resources a user's role permits.
- **MFA**: required for every remote/VPN session — no exceptions for administrative accounts.
- **Device posture**: remote-connecting devices are subject to the same AAA-driven behavioral monitoring as on-premises devices; a device whose security posture changes is automatically flagged, quarantined, or access-limited.
- **Removable media and USB ports**: disabled by default on endpoints handling cardholder data or other regulated information; exceptions require CISO approval and are logged.

## 6. Third-Party and Vendor (B2B) Risk Management

This section formalizes the security requirements of FinSecure's B2B relationship with GlobalTech Industries and any future B2B partners, referenced but not previously codified elsewhere in this policy.

- **Onboarding review**: any new B2B or vendor connection is reviewed against this policy's access-control and encryption standards before go-live.
- **Least-privilege B2B access**: partner access is scoped to the specific systems required for the business relationship, via the same RBAC and network-segmentation controls used internally.
- **Shared incident communication**: a joint communication matrix and trouble-ticket process governs incident notification between FinSecure and its B2B partners, consistent with the [risk register](../risk-assessment/risk-register.md)'s service-availability risks.
- **Periodic reassessment**: B2B access is reviewed on the same biannual cadence as internal access (Section 4.7).

## 7. Compliance and Auditing

- **SOX**: access controls and auditing maintain financial data integrity.
- **PCI DSS**: secure storage and transmission of cardholder data, verified through regular testing.
- **GLBA**: confidentiality of nonpublic personal information protected through NDAs and data-privacy policies.

## 8. Business Continuity

- **SLA**: 3-hour response time target; 99.999% availability target.
- **Continuity plan**: tested regularly to minimize interruption.
- **Backup and disaster recovery**: documented plans ensure data availability under adverse conditions.

## 9. Data Classification and Confidentiality

Data is labeled **confidential**, **private**, or **public**, with handling and access requirements set by that classification.

## 10. Training and Policy Awareness

All personnel receive mandatory, regular training on data classification, handling requirements, and this policy's confidentiality expectations.

## 11. Policy on Confidential Information Sharing

No employee may publish, disclose, or label information related to FinSecure Technologies Inc. or its partners, including GlobalTech Industries, without prior clearance.

## 12. Policy Review and Enforcement

This policy is reviewed annually, or immediately upon a material change in technology, regulation, or the threat landscape. Non-compliance may result in disciplinary action for employees or contract revocation for third parties, up to and including further action available under law.

---

### Changelog from the original submitted policy (v1.1)

- Renumbered sections sequentially (the original document's numbering skipped from Section 10 to Section 13, leaving no Sections 11–12).
- Added **Section 5 (Remote Access and Removable Media)** and **Section 6 (Third-Party and Vendor Risk Management)** — both already described narratively elsewhere in the original report but never formalized as governing policy sections.
- Merged the original standalone "Policy Review and Updates" and "Compliance and Enforcement" sections into one (Section 12), since they addressed the same lifecycle concern.
