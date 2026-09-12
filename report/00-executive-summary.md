# Executive Summary

FinSecure Technologies Inc., a New York City-headquartered financial services firm, hosts financial services and software-based web applications for a client base of finance firms, e-commerce companies, government agencies, and publicly traded companies. It does not serve the health sector.

This engagement was commissioned after a confirmed security breach of FinSecure's web application server. The objective was twofold: bring the network into compliance with **SOX**, **PCI DSS**, and **GLBA**, and redesign the environment around **Zero Trust Architecture (ZTA)** principles — with particular attention to securing remote employee access and the B2B connection to FinSecure's key client, GlobalTech Industries.

## Key Outcomes

| Area | Outcome |
|---|---|
| Network architecture | Fully re-segmented into DMZ, Web Application, Database, and Internal VLAN zones, each behind dedicated firewalls |
| Perimeter defense | Dual active-mode Web Application Firewalls (WAF) and a Next-Generation Firewall (NGFW) with IPS, VPN, and DLP |
| Identity & access | New AAA server integrated with Active Directory, delivering SSO, MFA, RBAC, and continuous behavioral monitoring |
| Monitoring | Primary and backup SIEM, with NGFW/WAF logs centralized for correlation and alerting |
| Compliance | Network and policy redesign brings FinSecure into alignment with SOX, PCI DSS, GLBA, and the NIST Cybersecurity Framework |

## Scope

The engagement covered:
- A **network security analysis** of the compromised environment (automated scanning, manual penetration testing, and a compliance-focused security audit).
- A **redesigned network architecture** with defense-in-depth segmentation and new perimeter/monitoring infrastructure.
- A **Zero Trust Architecture** implementation, justified against FinSecure's specific regulatory obligations.
- A formal **incident response** record for the breach that triggered this engagement.
- A comprehensive **risk assessment** and an updated **Network Security Policy**.

This report does not cover health-sector compliance (e.g., HIPAA), as FinSecure has no health-sector clients.
