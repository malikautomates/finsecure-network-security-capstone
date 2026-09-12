# Fortifying B2B Network Security for Regulatory Compliance

A network security capstone case study built around **FinSecure Technologies Inc.**, a fictional financial services firm brought into SOX / PCI DSS / GLBA compliance through a full network redesign and a Zero Trust Architecture rollout, following a simulated SQL-injection breach of its web application server.

> **Disclaimer**: FinSecure Technologies Inc., GlobalTech Industries, and the October 3, 2024 breach are a fictional scenario created for coursework. This is not a real incident disclosure or a real company.

## About This Project

This was a group capstone for **Case Studies, Issues & Capstone Project in Network Security**, University of Winnipeg, Fall 2024, under Prof. Victor Balogun (**Group 3**). The course covered four modules — Cloud Migration, Identity & Access Management, Application Security, and the culminating Network Security capstone — delivered as a network redesign, a Zero Trust implementation, a risk assessment, and a governing security policy.

**This repo is a rebuild of that project's flagship deliverable** — the final capstone report and presentation — done afterward to fix a handful of internal inconsistencies found on review (mismatched pentest evidence, a PCI-DSS wording contradiction, a gap in the policy document's section numbering) and to present the work more professionally. The technical decisions and content are unchanged; what changed is consistency, clarity, and presentation. See [`report/full-report.md`](report/full-report.md) for a changelog-style note on exactly what was fixed and why.

My own contribution to the original group project was the **Network Security Analysis** section — the penetration-testing methodology, tooling, and findings that the incident investigation was built on ([report/03-network-security-analysis.md](report/03-network-security-analysis.md)).

## Repository Structure

| Path | Contents |
|---|---|
| [`report/`](report/) | The full capstone report, split by section, plus a single combined [`full-report.md`](report/full-report.md) and [`full-report.pdf`](report/full-report.pdf) |
| [`policy/network-security-policy.md`](policy/network-security-policy.md) | The standalone Network Security Policy governing FinSecure's controls |
| [`risk-assessment/risk-register.md`](risk-assessment/risk-register.md) | The full asset-by-asset risk register |
| [`diagrams/`](diagrams/) | Redrawn network architecture (before/after), attack-path, and Zero Trust flow diagrams (SVG) |
| [`evidence/`](evidence/) | Real screenshots from the group's own testing: [`pentest/`](evidence/pentest/) (Nmap/OWASP ZAP scans of the live `FinSWebApp` deployment) and [`cloud-migration/`](evidence/cloud-migration/) (Azure portal evidence — VNet, Key Vault, TDE, WAF) |
| [`presentation/`](presentation/) | The rebuilt capstone presentation deck (PPTX) with full speaker notes, plus a [slide-by-slide README walkthrough](presentation/README.md) with images and short explanations |
| [`reference/`](reference/) | Lightly cleaned working notes from the Cloud Migration, IAM, and Application Security modules — supplementary, not fully rewritten |

## Reading Order

1. [Executive Summary](report/00-executive-summary.md)
2. [Introduction and Scope](report/01-introduction-and-scope.md)
3. [Network Design and Implementation](report/02-network-design-and-implementation.md)
4. [Network Security Analysis](report/03-network-security-analysis.md)
5. [Risk Assessment](report/04-risk-assessment.md)
6. [Zero Trust Architecture](report/05-zero-trust-architecture.md)
7. [Incident Response](report/06-incident-response.md)
8. [Recommendations and Conclusion](report/07-recommendations-and-conclusion.md)

Or read it as one document: [`report/full-report.md`](report/full-report.md) / [`report/full-report.pdf`](report/full-report.pdf).

## Technologies & Frameworks Referenced

**Compliance:** SOX · PCI DSS · GLBA · NIST Cybersecurity Framework
**Network security:** NGFW · Web Application Firewall (dual active) · SIEM (primary + backup) · VLAN segmentation · Zero Trust Architecture
**Identity:** Active Directory · AAA (RADIUS-based) · SSO · MFA · RBAC
**Security testing tools:** Nmap · OWASP ZAP · Metasploit · Wireshark
**Cloud (supplementary modules):** Microsoft Azure — VNets/NSGs, Azure AD, Key Vault, Transparent Data Encryption, Azure Security Center

## Credits

**Group 3** — Case Studies, Issues & Capstone Project in Network Security, University of Winnipeg, Fall 2024
**Instructor:** Victor Balogun
**This rebuild:** Muhammed Abdulmalik (network security analysis / penetration-testing section author)
