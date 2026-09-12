# Incident Response: Application Server Compromise

## Incident Overview

**Date:** October 3, 2024
**System affected:** Web application server
**Data exposed:** Cardholder data, including Personally Identifiable Information (PII) and financial records of high-profile clients, including GlobalTech Industries

The breach was first noticed through anomalous entries in the SIEM. Investigation confirmed the attack chain reconstructed in [Network Security Analysis](03-network-security-analysis.md#attack-path): a SQL injection attack against the web application server over port 80, followed by exploitation of weak SFTP credentials to extract confidential information.

Beyond the immediate data exposure, the incident placed FinSecure in violation of SOX's data-protection requirements — compounding the compliance gap this entire engagement was commissioned to close.

## Response Actions

1. **Containment** — the compromised server was immediately disconnected from the network to stop further exfiltration.
2. **Investigation** — a dedicated incident response team, drawing subject-matter experts from every relevant technical group, conducted a forensic investigation.
3. **Client notification** — affected clients, including GlobalTech Industries, were notified promptly and transparently to preserve trust.
4. **Data recovery and restoration**:
   - Database restored from backup.
   - An additional WAF deployed to prevent recurrence.
   - A dedicated Cardholder Data Environment created, with its own database server behind its own dedicated firewall.
   - A new AAA server with MFA and stricter RBAC introduced.
   - A comprehensive security audit conducted across all systems.
5. **Compliance review** — an independent third-party auditor was engaged to identify any remaining, previously unidentified vulnerabilities.

## Lessons Learned

| Theme | What It Drove |
|---|---|
| **Vulnerability management** | Adoption of a recurring OWASP ZAP / Nmap scanning and patch-management cadence (see [Network Security Policy](../policy/network-security-policy.md)) |
| **Incident response planning** | A documented IR plan and a standing, cross-functional response team, rather than an ad hoc response |
| **Continuous monitoring** | SIEM alert thresholds retuned to catch smaller anomalies earlier |
| **Employee training** | General organization-wide security awareness training, plus specialized training for the IT team on distinguishing false positives from real incidents |
| **Regulatory compliance** | Reaffirmed commitment to SOX, PCI DSS, and GLBA, backed by both in-house and third-party audits going forward |

This incident is the direct justification for every major decision in this report: the [network redesign](02-network-design-and-implementation.md), the [Zero Trust rollout](05-zero-trust-architecture.md), and the hardened [Network Security Policy](../policy/network-security-policy.md) all trace back to the specific failure modes exposed here.
